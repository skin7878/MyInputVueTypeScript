<script setup lang="ts">
  import { reactive } from 'vue'
  import MyInput from './components/MyInput.vue'
  import type { IInput } from './types'    
  
  const inputData = reactive<IInput[]>([
    { id: "username",  label: "User Name", type: "text", placeholder: "add username", value: '' },
    { id: "email", label: "Email", type: "email", placeholder: "add email", value: '' },
    { id: "password", label: "Password", type: "password", placeholder: "add password", value: '' } 
  ])

  interface IUser {
    userName: string;
    email: string;
    password: string;
  }

  const userData = reactive<IUser>({
    userName: '',
    email: '',
    password: ''
  })

  const addData = (): void => {

    const isEmpty: boolean = Object.values(inputData).every(item => item.value === '') 

    if(isEmpty) return 

    inputData.forEach((item: IInput) => {
      switch(item.id) {
        case 'username':
          userData.userName = item.value
          break        
        case 'email': 
          userData.email = item.value
          break        
        case 'password': 
          userData.password = item.value
          break                   
      }
      item.value = ''      
    })
    console.log(userData)    
  }

  
</script>

<template>
  <form class="form" @submit.prevent="addData">
    <template v-for="item in inputData" :key="item.id">
      <MyInput v-model="item.value" :item="item" />      
    </template>
    <button class="btn" type="submit">Add</button>
  </form>
</template>

<style scoped>
  .form {    
    width: min(100%, 40rem);      
  }
  .btn {
    padding: .7rem 2rem;
    cursor: pointer;
    background-color: #abf9de;
    color: #221719;
    border: none;
    border-radius: .3rem;
  }
  
</style>

