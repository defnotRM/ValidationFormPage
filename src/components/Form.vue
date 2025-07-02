<script setup>
  import {ref,computed,watch} from 'vue';
  const priceUSD = ref(1);
  const exchangeRate = 35;
  

  // const priceTHB = computed({
  //   get: () => priceUSD.value * exchangeRate,
  //   set: (newValue) => {
  //     priceUSD.value = newValue / exchangeRate;
  //   }
  // })

  const name = ref('');
  const surname = ref('');
  const fullname = ref('');

  watch([name, surname],(newFullname,oldFullname) =>{
    fullname.value = `${newFullname[0]} ${newFullname[1]}`.toUpperCase();
    
  })

  
</script>
<template>
  <div>
    <div>
    ชื่อเต็ม: {{fullname}}
    </div>
    ชื่อ {{name}}
    <div>
    <input type="text" v-model="name">
    </div>
    นามสกุล {{ surname }}
    <div>
    <input type="text" v-model="surname">
    </div>
  </div>
</template>
<style>
</style>