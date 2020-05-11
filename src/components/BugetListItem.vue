<template>
<div>
  <div class="sortButtons">
   <el-button type="success" id="0" icon="el-icon-top" plain size="mini" @click="sortItemID(id)"></el-button>
   <el-button type="danger" id="1" icon="el-icon-bottom" plain size="mini" @click="sortItemID(id)"></el-button>
   <el-button type="primary" id="2" icon="el-icon-check" plain size="mini" @click="sortItemID(id)">All</el-button>
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
    buttonValue: Number,
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
    sortItems(id, event) {
      console.log(event.target.id, this.sortItemID);
      (this.$emit("sortItems", id));  
    },
    sortItemsID(){
      console.log(555);
      this.sortItemCounter += 1;
      this.$emit("onChangeSortItemCounter", this.sortItemCounter);
    },
    sortItemID(id){
      this.buttonValue = event.target.id;
      // console.log(event.target.id, this.buttonValue);
      this.$emit("onChangeCounter", id);
    }    
  },
  computed: {
    // sortItemID: function() {
    // // return console.log(this.sortItemID = event.target.id);  
    //   // this.sortItemID =  event.target.id;
    //   // return if (event.target!==this.sortItemID) {  
    //     return console.log(this.buttonValue);
      
        
  
    
    //   //  (this.sortItemsID);     
    // },
    
    // textStyleNumber: function() { 
    //  return Object.values(this.list).map((list)=> {
    //     if ( list.type == "OUTCOME" ) {
    //       return 'text-red';
    //     } else {
    //       return 'text-green';
    //       }
    //    });
    // }
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