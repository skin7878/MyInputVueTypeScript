<template>      
  <label :for="item.id" class="my-label">{{ item.label }}</label>
  <input
    class="my-input"
    :id="item.id" 
    :type="item.type"      
    :placeholder="item.placeholder"
    :value="modelValue"
    @input="updateValue"
  >  
</template>

<script setup lang="ts">
import type { IInput } from '../types' 

const emit = defineEmits<{
  (e: 'update:modelValue', value: string | number): void
}>()

const updateValue = (e: Event) => emit('update:modelValue', (e.target as HTMLInputElement).value)

type InputData = Omit<IInput, 'value'>;

interface IProps {
  item: InputData;
  modelValue: string;
}

defineProps<IProps>()

</script>

<style scoped>
  .my-label {
    display: block;
    margin-bottom: .5rem;    
  }

  .my-input {
    padding: 1rem;
    margin-bottom: 1rem;
    border: .1rem solid #D3D3D3;
    border-radius: .3rem;    
    width: 100%;
  }

  .my-input:focus {
    outline: .1rem solid silver;    
  }  
  
</style>