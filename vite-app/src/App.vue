<template>
  <div>
    <div>arr {{message}}</div>
    <div>obj: {{obj}}</div>
    <div>person: {{person}}</div>
  </div>
</template>

<script setup lang="ts">
import { reactive } from "@vue/reactivity";

let message = reactive([])
let obj = reactive({
  name:"sm"
})

type Person = {
  list ?: number []
}
let person = reactive<Person>({
  list: []
})
setTimeout(() => {
  person.list = [1,2,3]
  console.log(person);
  
}, 1000)
</script>

<style>

</style>