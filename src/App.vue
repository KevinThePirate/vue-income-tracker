<template>
  <MyHeader :totalIncome="state.totalIncome" />
  <AddForm :state="state" @add-income="AddIncome" />
  <IncomeList :state="state" @remove-item="removeItem" />
</template>

<script>
import { reactive, computed } from "vue";
import MyHeader from "./components/MyHeader";
import AddForm from "./components/AddForm";
import IncomeList from "./components/IncomeList.vue";
export default {
  components: {
    MyHeader,
    AddForm,
    IncomeList,
  },
  setup() {
    const state = reactive({
      income: [],
      totalIncome: computed(() => {
        let temp = 0;
        if (state.income.length > 0) {
          for (let i = 0; i < state.income.length; i++) {
            temp += state.income[i].value;
          }
        }
        return temp;
      }),
    });
    function AddIncome(data) {
      let d = data.date.split("-");
      let newD = new Date(d[0], d[1], d[2]);
      state.income = [
        ...state.income,
        {
          id: newD.getTime(),
          desc: data.desc,
          value: data.value,
          date: newD.getTime(),
        },
      ];
      console.log(state.income);
    }

    function removeItem(id) {
      state.income = state.income.filter((v) => v.id != id);
    }

    return { state, AddIncome, removeItem };
  },
  watch: {
    state: {
      handler() {
        console.log("state changed");
        console.log(this.state.income);
        let temp = [];

        temp = this.state.income.sort(function (a, b) {
          return b.date - a.date;
        });

        this.state.income = temp;
      },
      deep: true,
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Code", "Fira Sans", sans-serif;
}
body {
  background: white;
}
</style>
