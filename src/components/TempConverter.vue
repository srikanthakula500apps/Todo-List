<script>
import {ref} from 'vue'
export default{
    setup(){
        const c=ref('')
        const f=ref('')
    }
}

</script>

<template>
<input type="number" :value='c' @change='setC'>Celsius
<input type="number" :value='f' @change='setF'>Fareinshheat

</template>