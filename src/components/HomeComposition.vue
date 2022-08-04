<template>
  <div>{{ text }}</div>
  <div>{{ counter }}</div>
  <div>{{ obj.counter2 }}</div>
  <div>{{ firstName }} {{ lastName }}</div>
  <div>{{ fullName }}</div>
  <div>{{ username }}</div>
  <div>Month Birth:{{ monthBirth }} Year Birth:{{ yearBirth }}</div>
  <button ref="btn">Click</button>
</template>

<script>
import { toRefs, onMounted, ref, reactive, watch, computed, inject } from "vue";
export default {
  props: {
    yearBirth: {
      type: String,
    },
    monthBirth: {
      type: String,
    },
  },
  setup(props, context) {
    // attrs  (non reactive object, equivalent to $attrs)
    console.log("attrs context", context.attrs);

    // Slots (Non-reactive object, equivalent to $slots)
    console.log("slots context", context.slots);

    // Emit events (Function, equivalent to $emit)
    console.log("emit context", context.emit);

    // Expose public properties (Function)
    console.log("expose context", context.expose);

    // ref with composition api
    const btn = ref(null);

    const { yearBirth, monthBirth } = toRefs(props);
    const firstName = ref("Carlos");
    const lastName = ref("Ferrer");

    const text = ref("Hello Vue");
    const counter = ref(0);
    const obj = reactive({ counter2: 10 });

    // inject from app
    const username = inject("username");

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
      },
      btn,
      (value) => {
        btn;
        console.log("watch btn", value);
      }
    );

    onMounted(() => {
      console.log("mounted!");
      console.log(btn.value);
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
      // Inject a value from the parent component
      username,
      btn,
    };
  },
};
</script>
