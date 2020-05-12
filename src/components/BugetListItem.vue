<template>
<div>
  <div class="sortButtons">
   <el-button type="success" id="2" icon="el-icon-top" plain size="mini" @click="sortItemID"></el-button>
   <el-button type="danger" id="3" icon="el-icon-bottom" plain size="mini" @click="sortItemID"></el-button>
   <el-button type="primary" id="1" icon="el-icon-check" plain size="mini" @click="sortItemID">All</el-button>
  </div>
  <div class="list-item" v-for="(item, prop) in list" :key="prop">
      <span :class="elIconBottom" v-if="item.type==='OUTCOME'"> </span>
      <span :class="elIconTop" v-else> </span>
      <span class="budget-comment">  {{ item.comment }} </span>
      <span class="budget-value" :class="[item.type==='INCOME' ? activeColor : 'text-red']" >  {{ item.value }} </span>   
      <el-button type="danger"  size="mini" @click="varId=item.id, dialogVisible = true">Delete</el-button> 
      <el-dialog
        :visible.sync="dialogVisible"
        width="30%"
        >
        <span>Are you sure you want to delete this item?</span>
        <span slot="footer" class="dialog-footer">
          <el-button @click="dialogVisible = false" >Cancel</el-button>
          <el-button type="primary" @click="dialogVisible = false, deleteItem(varId)">Delete</el-button>
        </span>
      </el-dialog>
    </div>
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
  props: {
    buttonValue: [Number, String],
    list: {
      type: [Object, Array],
      default: () => ({     
      })
    }
  },
  data: () => ({
      dialogVisible: false,
      elIconBottom:"el-icon-bottom",
      elIconTop:"el-icon-top",
      activeColor: 'text-green',
      typeValue: 'INCOME',
      sortButtonValue: '',
      sortItemCounter: 0,
  }),
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);  
    },       
    deleteItemHendler(id) {
      this.$emit("deleteItemHendler", id);  
    },   
    sortItemID(id){
      this.$emit("onChangeCounter", id);
    }    
  },
  computed: {
  },
}
</script>

<style scoped>

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
.text-red {
  color:red;
}
.text-green {
  color:green;
}
.sortButtons{
  text-align: right;
  padding: 0 15px 20px 15px;
}

</style>

<style>
.el-icon-bottom:before, 
.el-icon-check:before,
.el-icon-top:before,
.el-icon-bottom, 
.el-icon-check,
.el-icon-top,
[class*=" el-icon-"], [class^=el-icon-] {
    pointer-events: none!important;
  }

</style>