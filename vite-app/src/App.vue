<script setup lang="ts">
import { Ref, ref, isRef, shallowRef, triggerRef, customRef } from "@vue/reactivity";

let message: Ref<string> = ref("小满")
let notRef: number = 1
const changeMsg = () => {
  message.value = 'change msg'
  console.log(message);
  console.log('isRef', isRef(message)); // true
  console.log('isRef', isRef(notRef));  // false
}

let h_ShallowRef  = shallowRef({
  name: "小满"
})
const changeShallowRef = () => {
  //  响应式改变
  // h_ShallowRef.value = {name:"大满"}
  h_ShallowRef.value.name = "大满"
  triggerRef(h_ShallowRef)
}

// 自定义Ref
function MyRef<T>(value: T) {
  return customRef((trank,trigger) => {
    return {
      get() {
          trank()
          return value
      },
      set(newVal: T) {
          value = newVal
          trigger()
      }
    }
  })
}
let message2 = MyRef<string>("小满")
const changeMsg2 = () => {
  message2.value = "大满"
}
</script>

<!--  -->
<template>
  <div>
    {{message}}
    <button @click="changeMsg">改变</button>
    {{h_ShallowRef}}
    <button @click="changeShallowRef">shallowRef</button>
  </div>
</template>

<style scoped>

</style>
