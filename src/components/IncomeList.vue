<template>
  <div class="income-list">
    <div class="income-item">
      <IncomeItem
        v-for="obj in state.income"
        :key="obj.id"
        :income="obj"
        @remove-item="removeItem"
      />
    </div>
  </div>
</template>

<script>
import IncomeItem from "./IncomeItem.vue";
export default {
  components: { IncomeItem },
  props: {
    state: Object,
  },
  setup(props, { emit }) {
    function removeItem(id) {
      emit("remove-item", id);
    }
    return { IncomeItem, removeItem };
  },
};
</script>

<style>
.income-list {
  margin-top: 30px;
  padding: 15px;
}
</style>
