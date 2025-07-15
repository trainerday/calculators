<script setup>
import { ref, computed, watch } from 'vue';

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
        },
        multiplier: {
            required: false,
        },
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
                return next ;
            }

            v = next ;
        }
        return v ; // best estimate if no convergance
    }

    // vv does not need looping function vv
    // const compute_me_first = computed(() => {
    //     return  props.drag * props.frontal_area * air_density ;
    // }) 

    // const a = computed(() => {
    //     return .5 * compute_me_first.value ;
    // })

    // const b = computed(() => {
    //     return props.headwind * compute_me_first.value ;
    // })

    // const c = computed(() => {
    //     return grav * props.mass * rolling_resistance + ( a.value * (props.headwind ** 2)) ;
    // })

    // const d = computed(() => {
    //     return 0 - (1 - drivetrain_loss) * props.power ;
    // })

    // const Q = computed(() => {
    //     return (3*a.value*c.value - b.value**2) / (9*(a.value**2)) ;
    // })

    // const R = computed(() => {
    //     return (9*a.value*b.value*c.value - 27*d.value*(a.value**2) - 2*(b.value**3)) / (54*(a.value**3))
    // })

    // const S = computed(() => {
    //     return Math.cbrt( R.value + Math.sqrt((Q.value**3 + R.value**2)) )
    // })

    // const T = computed(() => {
    //     return Math.cbrt( R.value - Math.sqrt((Q.value**3 + R.value**2)) )
    // })

    // function find_speed2() {
    //     return S.value + T.value - (b.value / (3*a.value))
    // }

    // const calculated_speed2 = ref(find_speed2()) ;
    const calculated_speed = ref(find_speed()) ;

    watch(
        () => [props.power, props.mass, props.drag, props.frontal_area, props.headwind],
        () => {
            calculated_speed.value = find_speed();
            // calculated_speed2.value = find_speed2();
        },
        { immediate: true }
    );
</script>

<template>
    <div>
        <!-- {{ A }} {{ B }} {{ C }} -->
        Estimated Speed
        {{ (props.headwind == 0) ? "" : "(" + props.headwind + props.unit +" wind)" }} <br>
        {{ (calculated_speed * props.multiplier * 3.6).toFixed(2) }} {{ " " + props.unit }}
        
    </div>
</template>

<style scoped>
    div {
        text-align: center;
    }
</style>