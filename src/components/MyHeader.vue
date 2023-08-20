<template>
  <header>
    <h1>Expense Log</h1>
  </header>
  <div id="total">
    <h2>Total Spent:</h2>
    <div class="total-income">€{{ totalIncome }}</div>
  </div>
</template>

<script>
export default {
  props: {
    totalIncome: {
      type: Number,
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./variables.scss";

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 30px;
  background-color: $headline;

  h1 {
    color: $background;
    font-size: 28px;
  }
}
#total {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-content: baseline;
  padding-top: 50px;

  h2 {
    align-self: center;
  }
  .total-income {
    font-family: "Fira Code", "Fira Sans", sans-serif;
    background-color: $button;
    color: #fff;
    font-size: 20px;
    font-weight: 900;
    padding: 5px 10px;
    width: 100px;
    text-align: center;
    border-radius: 8px;
    box-shadow: inset 0px 0px 6px rgba(0, 0, 0, 0.25);
    text-shadow: 0px 3px 3px rgba(0, 0, 0, 0.25);
    margin-left: 30px;
  }
}
</style>
