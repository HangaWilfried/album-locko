<template>
  <div class=" bg-gray-50 h-full top-0 fixed w-full p-5">
    <h1 class="flex flex-col items-center gap-2 mb-10 mt-10">
      <span class="text-2xl font-medium text-gray-400">Nouvel Album</span>
      <span class="text-2xl font-thin text-pink-400">Locko</span>
    </h1>

    <div class="flex flex-col place-content-start">
      <div class="flex flex-col gap-7 mb-5">
        <input type="text" v-model="phoneNumber"  class="pl-3 text-gray-600 rounded border border-gray-200 h-12 focus:shadow-xl focus:outline-none focus:border-gray-600 sm:w-full" placeholder="Entrez votre numero">
        <button @click="checkValidation" class="w-full border border-blue-400 h-12 rounded bg-blue-400 text-white text-lg hover:bg-blue-500 hover:border-blue-500">Soumettre</button>
      </div>
      <template v-if="!isCorrect">
        <ul>
          <li v-for="(error, index) in errors" :key="index" class="mt-5 ml-4 text-base list-disc text-pink-600 mb-2">{{error}}</li>
        </ul>
      </template>
    </div>
  </div>

</template>

<script lang="ts">
import {computed, ref, reactive, defineComponent} from 'vue'
export default defineComponent({
  name: "App",
  setup(){
    let isCorrect = ref<boolean>(true)
    let errors = reactive<string[]>([])
    const phoneNumber = ref<string>('')

    const checkValidation = () => {
      errors.length = 0
      const letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'x', 'y', 'z', 'w', 'u', 'v']
      const conditions = ['ne doit pas contenir de lettres','ne doit pas contenir d\'espaces', 'doit etre egale a 9 caracteres', 'doit commencer par 6']
      const splitPhoneNumber: string[] = [...phoneNumber.value]
      if (letters.map(item => splitPhoneNumber.includes(item)).includes(true)){
        isCorrect.value = false
        errors.push(conditions[0])
      }
      if(splitPhoneNumber.includes(' ')){
        isCorrect.value = false
        errors.push(conditions[1])
      }
      if (phoneNumber.value.length !== 9) {
        isCorrect.value = false
        errors.push(conditions[2])
      }
      if (splitPhoneNumber[0] !== '6') {
        isCorrect.value = false
        errors.push(conditions[3])
      }
      if(isCorrect.value) alert('good job')
    }
    return{
      isCorrect, phoneNumber, checkValidation, errors
    }
  }
})
</script>

<style scoped>
.show{
  display: block;
  color: red;
  font-size: 15px;
}
</style>
