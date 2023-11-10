<script setup></script>
<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "EssentialLink",
  props: {
    title: {
      type: String,
      required: true,
    },
    propValue: {
      type: String,
      required: true,
    },
    mask: {
      type: String,
    },
  },
  data() {
    return {
      internalValue: this.propValue,
      currentMask: this.mask,
    };
  },
});
</script>

<template>
  <q-item clickable tag="a" target="_blank">
    <q-item-section>
      <q-item-label class="title">{{ title }}</q-item-label>
      <q-input
        filled
        :mask="currentMask"
        class="input"
        :name="internalValue"
        :v-model="internalValue"
        fill-mask=""
      />
    </q-item-section>
  </q-item>
</template>

<style>
.title {
  font-size: 18px;
  font-weight: 700;
}

.input {
  padding: 5px;
}
</style>
