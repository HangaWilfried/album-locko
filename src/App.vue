<template>
  <div class=" bg-gray-50 h-full top-0 fixed w-full flex flex-col gap-5 place-items-center">
    <div class="pt-20">
      <h1 class="flex flex-col gap-7 items-center">
        <span class="text-6xl font-medium text-gray-400">Nouvel Album</span>
        <span class="text-9xl font-thin text-pink-400">Locko</span>
      </h1>
    </div>
    <div class="flex gap-5 py-20 place-content-center">
      <div class="flex flex-col gap-5 place-items-center">
        <input type="text" v-model="phoneNumber" placeholder="Entrez votre numero" class="text-gray-600 rounded border border-gray-200 h-12 px-7 focus:shadow-xl focus:outline-none focus:border-gray-600">
        <div class="show" v-if="!isCorrect">
          <ul v-for="(error, index) in errors" :key="index">
            <li class="text-base list-disc text-pink-600">{{error}}</li>
          </ul>
        </div>
      </div>
      <button @click="checkValidation" class="border border-blue-400 h-12 px-10 rounded bg-blue-400 text-white text-lg hover:bg-blue-500 hover:border-blue-500">Soumettre</button>
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
