<script setup>
import { ref, computed, watch, onMounted } from 'vue';

    const props = defineProps({
        unit: {
            type: String,
            required: true,
        },
        power: {
            required: true,
        },
        mass: {
            required: true,
        },
        drag: {
            required: true,
        },
        frontal_area: {
            required: true,
        },
        headwind: {
            required: true,
        }
    });
    const grav = 9.80665;
    const rolling_resistance = 0.005;
    const air_density = 1.225;
    const drivetrain_loss = 0.03;

    const A = computed(() => {
        return 0.5 * air_density * props.frontal_area * props.drag ;
    });

    const B = computed(() => {
        return grav * rolling_resistance * props.mass ;
    });

    const C = computed(() => {
        return (1 - drivetrain_loss) * props.power ;
    });

    /**
     * Uses the newton_raphson method to find a close guess to the actual value.
     */
    function find_speed(v0 = 5.0, tolerance = 0.0001, max_depth = 100) {
        let v = v0 ;

        for ( let i = 0 ; i < max_depth ; i++ ) {
            const relative_wind = props.headwind + v ;
            // console.log("values: ", A, B, C);
            // console.log(A.value * relative_wind**2 * v + B.value * v - C.value)
            const f = A.value * relative_wind**2 * v + B.value * v - C.value ;
            const df = 3 * A.value * relative_wind**2 + B.value ;

            if (df == 0) {
                break ;
            }

            const next = v - ( f / df ) ;
            
            if (Math.abs(next - v) < tolerance) {
                return next.toFixed(2) ;
            }

            v = next ;
        }
        return v.toFixed(2) ; // best estimate if no convergance
    }

    const calculated_speed = ref(find_speed()) ;

    watch(
        () => [props.power, props.mass, props.drag, props.frontal_area, props.headwind],
        () => {
            calculated_speed.value = find_speed();
        },
        { immediate: true }
    );

</script>

<template>
    <p>
        <!-- {{ A }} {{ B }} {{ C }} -->
        Estimated Speed
        {{ (props.headwind == 0) ? "" : "(" + props.headwind + props.unit +" wind)" }} <br>
        {{ calculated_speed }} {{ " " + props.unit }}
    </p>
</template>