<template>
  <div>
    <button @click="toggle">Modal</button>
    <teleport to="body">
      <div v-show="show" class="modal">
        <h1>Titulo</h1>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Rem voluptate
          nam neque autem est praesentium, voluptatem, pariatur saepe asperiores
          beatae sit. Unde molestiae quas harum saepe commodi esse reiciendis
          magni?
        </p>
        <button @click="toggle">X</button>
      </div>
    </teleport>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: "Hello World",
      show: false,
    };
  },
  methods: {
    toggle() {
      console.log("haciendo toggle");
      this.show = !this.show;
    },
  },
};
</script>
