<template>
  <div class="buget-list-wrap">
    <el-card :header="header">
      <template v-if="!isEmpty">
        <BudgetListItem @onChangeCounter="sortItemID1" :buttonValue="buttonValue" :list="list" @deleteItem="onDeleteItem"/>
      </template>   
      <el-alert v-else type ="info" :title="emptyTitle" :closable="false" />   
    </el-card>
  </div>
</template>

<script>

import BudgetListItem from '@/components/BugetListItem';

export default {
  name: "BudgetList",
  components: {
    BudgetListItem
  },
  props: {
    buttonValue: Number,
    list: {
      type: [Object, Array],
      default: () => ({})
    }
  },
  data: () => ({
    header: "Buget List",
    emptyTitle: "Empty List",
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id)
    },
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    sortItemID1(){
      this.$emit("onChangeCounter1", event.target.id);
    },
  }
};
</script>

<style scoped>
.buget-list-wrap {
  max-width: 500px;
  margin: auto;
}

.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}

.budget-value{
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px; 

}

</style>