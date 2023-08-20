<template>
  <form
    @submit.prevent="FormHandler"
    v-bind:style="{ background: borderVar.border }"
  >
    <input type="text" placeholder="Title" v-model="formData.desc" />
    <input type="number" placeholder="Value" v-model="formData.value" />
    <input type="date" placeholder="Date..." v-model="formData.date" />
    <input type="submit" value="Add Income" />
  </form>
</template>

<script>
import { computed, reactive } from "vue";
export default {
  props: {
    state: Object,
  },
  setup(props, { emit }) {
    const formData = reactive({
      desc: null,
      value: null,
      date: null,
    });
    let borderVar = reactive({
      border: "none",
    });
    function formIsValid() {
      return (
        formData.desc !== null &&
        formData.value !== null &&
        formData.date !== null
      );
    }

    const borderStyling = computed(() => {
      if (!formIsValid()) {
        return "red";
      } else {
        return "none";
      }
    });

    function FormHandler() {
      if (!formIsValid()) {
        console.log("Form Invalid");
        borderVar.border = "rgba(239,69,101,0.5)";
        return;
      } else {
        borderVar.border = "none";
        emit("add-income", {
          desc: formData.desc,
          value: formData.value,
          date: formData.date,
        });
        console.log(formData);

        formData.desc = null;
        formData.value = null;
        formData.date = null;
      }
    }
    return { formData, FormHandler, borderStyling, borderVar };
  },
};
</script>

<style lang="scss" scoped>
@import "./AddForm.scss";
</style>
