<template>
  <div>{{ text }}</div>
  <div>{{ counter }}</div>
  <div>{{ obj.counter2 }}</div>
  <div>{{ firstName }} {{ lastName }}</div>
  <div>{{ fullName }}</div>
  <div>Month Birth:{{ monthBirth }} Year Birth:{{ yearBirth }}</div>
</template>

<script>
import { toRefs, onMounted, ref, reactive, watch, computed } from "vue";
export default {
  props: {
    yearBirth: {
      type: String,
    },
    monthBirth: {
      type: String,
    },
  },
  setup(props) {
    const { yearBirth, monthBirth } = toRefs(props);
    const firstName = ref("Carlos");
    const lastName = ref("Ferrer");

    const text = ref("Hello Vue");
    const counter = ref(0);
    const obj = reactive({ counter2: 10 });

    const fullName = computed(() => {
      return `${firstName.value} ${lastName.value}`;
    });

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
      firstName,
      lastName,
      fullName,
      // eslint-disable-next-line vue/no-dupe-keys
      yearBirth,
      // eslint-disable-next-line vue/no-dupe-keys
      monthBirth,
    };
  },
};
</script>
