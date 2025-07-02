<script setup>
  import {ref,computed,onMounted,watch} from 'vue';
  const name = ref('');
  const surname = ref(''); 
  const emailname = ref('');
  const fullname = computed(() =>  `${name.value} ${surname.value}`);

  const isLoading = ref(false);
  const isUpdated = ref(false);

  const updateProfile = async() =>{
    isLoading.value = true;
    await new Promise(resolve => setTimeout(resolve, 2000));
    isLoading.value = false;
    isUpdated.value = true;

    console.log("Profile updated:", {
      name: name.value,
      surname: surname.value,
      email: emailname.value
    });
  }

  const isValid = ref(true);
  const error = ref({});

  const validateName = (name) =>{
    const re = /\d/;
    return !re.test(name);

  }
  
  const validateEmail = (email) =>{
    return email.includes("@");
  }

  watch([name, surname, emailname], () => {
    isValid.value = true;
    isUpdated.value = false;
    error.value = {};

    if(!validateName(name.value)){
      isValid.value = false;
      error.value.name = "ชื่อจริงไม่ถูกต้อง";
    }

    if(!validateName(surname.value)){
      isValid.value = false;
      error.value.surname = "นามสกุลไม่ถูกต้อง";
    }

    if(!validateEmail(emailname.value)){
      isValid.value = false;
      error.value.email = "อีเมลไม่ถูกต้อง";
    }
  })
  
  onMounted(() =>{
    name.value = "test";
    surname.value ="oiiao";
    emailname.value = "test123@gmail.com";
  })
  

</script>
<template>
  <div class="container">
    <div class="profile">
      <div>
        fullname: {{ fullname }}
      </div>
      <div>
        email: {{ emailname }}
      </div>
      
    </div>
    <div>
      ชื่อจริง: <input type="text" v-model="name">
      <div class="error">
        {{ error.name }}
      </div>
    </div>
    <div>
      นามสกุล: <input type="text" v-model="surname">
      <div class="error">
        {{ error.surname }}
      </div>
    </div>
    <div>
      email: <input type="text" v-model="emailname">
      <div class="error">
        {{ error.email }}
      </div>
    </div>
    <div v-if="isLoading">
      Loading...
    </div>
    <div v-if="isUpdated">
      Updated Successfully!
    </div>
    <div>
      <button :disabled="!isValid" @click="updateProfile" >Update Profile</button>
    </div>
      
    
  </div>
</template>
<style>
  .container{
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .error{
    color: red;
  }
</style>