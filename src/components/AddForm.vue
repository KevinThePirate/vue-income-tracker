<template>
  <form
    @submit.prevent="FormHandler"
    v-bind:style="{ background: borderVar.border }"
  >
    <input type="text" placeholder="description" v-model="formData.desc" />
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

<style scoped>
form {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

form input {
  color: #888;
  border: none;
  outline: none;
  font-size: 20px;
  background: none;
}

form input::placeholder {
  color: #aaa;
}

form input:not([type="submit"]) {
  display: block;
  border: none;
  outline: none;
  padding: 5px 15px;
}

form input[type="submit"] {
  display: block;
  background: none;
  border: none;
  outline: none;

  color: #fff;
  font-weight: 500;
  text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  padding: 5px 15px;
  background-color: #ffce00;

  cursor: pointer;
}

form input:first-of-type {
  border-radius: 8px 0px 0px 8px;
}

form input:last-of-type {
  border-radius: 0px 8px 8px 0px;
}
</style>
