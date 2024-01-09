
<template>
  <div>
    <ul>
      <li
        :class="{ active: modelValue === 'poor' }"
        @click="selectButtonPressed('poor')"
      >
        <button type="button">Poor</button>
      </li>
      <li
        :class="{ active: modelValue === 'average' }"
        @click="selectButtonPressed('average')"
      >
        <button type="button">Average</button>
      </li>
      <li
        :class="{ active: modelValue === 'good' }"
        @click="selectButtonPressed('good')"
      >
        <button type="button">Good</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  props: ["modelValue"],
  emits: ["update:modelValue"],
  setup(props, {emit}) {
    const buttonPressed = ref(props.modelValue);

    const selectButtonPressed = (rating: string) => {
      buttonPressed.value = rating;
      emit('update:modelValue', rating)
    };

    return { buttonPressed, selectButtonPressed };
  },
});
</script>

<style scoped>
ul {
  list-style: none;
  margin: 1rem 0;
  padding: 0;
  display: flex;
  justify-content: space-around;
}
li {
  margin: 0 1rem;
  border: 1px solid #ccc;
  padding: 1rem;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
button {
  font: inherit;
  border: none;
  background-color: transparent;
}

.active {
  border-color: blue;
}
</style>