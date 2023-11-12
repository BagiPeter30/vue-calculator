<script setup>
import { ref } from 'vue'
const calculatorTopValue = ref('')
const calculateDesk = ref(['C', '*', '/', "-", 7,8,9, '+', 4,5,6, '10%', 1,2,3, '=', 0, '.'])
const operator = ref(null)
const prev = ref('')
function action(element)
{
  if(!isNaN(element) || element === ".")
  {
    this.calculatorTopValue += element + ''
  }
  else if(element === 'C')
  {
    this.calculatorTopValue = ''
  }
  else if(element === '10%')
  {
    this.calculatorTopValue = this.calculatorTopValue / 100
  }
  else if(['+', '-', '*', '/'].includes(element))
  {
    this.operator = element
    this.prev = this.calculatorTopValue
    this.calculatorTopValue = ''
  }
  else if(element === '=')
  {
    this.calculatorTopValue = eval(
      this.prev + this.operator + this.calculatorTopValue
    )
    this.operator = null
  this.prev = ''
  }


};

</script>

<template>
  
  <div class="bg-[#234] max-w-[650px] p-6 mx-auto mt-4 shadow-s shadow-slate-600 text-white font-bold text-xl">
    Matek Doga!
  </div>

  
<div class="bg-[#234] max-w-[450px] p-6 mx-auto mt-4 shadow-md shadow-slate-900">
  <div class="w-full bg-slate-800 p-3 shadow-md shadow-slate-800 text-right text-white font-bold text-xl">
    {{ calculatorTopValue || 0 }}
  </div>
  <div class="grid grid-cols-4 gap-3">
    <div class="" v-for="element in calculateDesk" :key="element">
      <div class="p-5 mt-2 bg-slate-950 hover:bg-slate-700
       transition-all duration-200 text-white text-bold 
       cursor-pointer"
       :class="{'bg-red-400' : ['+','=','-','*','/','C'].includes(element)}"
        @click="action(element)">
        {{ element }}
      </div>
    </div>
  </div>
</div>
</template>
