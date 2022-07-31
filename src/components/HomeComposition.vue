<template>
  <div>{{ text }}</div>
  <div>{{ counter }}</div>
  <div>{{ obj.counter2 }}</div>
</template>

<script>
import { onMounted, ref, reactive, watch } from "vue";
export default {
  setup() {
    const text = ref("Hello Vue");
    const counter = ref(0);
    const obj = reactive({ counter2: 10 });

    setInterval(() => {
      counter.value++;
      obj.counter2++;
    }, 500);

    watch(
      // hay que bindear el this de la funcion
      () => obj.counter2,
      (valor, anterior) => {
        valor;
        anterior;
        // console.log("watch", valor, anterior);
      }
    );

    onMounted(() => {
      console.log("mounted!");
    });

    return {
      text,
      counter,
      obj,
    };
  },
};
</script>
