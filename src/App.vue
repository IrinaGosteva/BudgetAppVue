<template>
  <div id="app">
    <Form @submitForm="onFormSubmit" />
    <TotalBalance :total="totalBalance" />
    <BugetList :buttonValue="buttonValue" :list="sortList" @deleteItem="onDeleteItem"  @change="onChange($event)" @onChangeCounter1="changebuttonValue"/>

  </div>
  
</template>

<script>
import BugetList from '@/components/BugetList';
import TotalBalance from '@/components/TotalBalance';
import Form from '@/components/Form';


export default {
  name: 'App',
  components: {
    BugetList,
    TotalBalance,
    Form,

  },
  data: () => ({
    buttonValue: 1,
    list: {
      1: {
        type: 'INCOME',
        value: 136,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: 24,
        comment: 'Some outcome comment',
        id: 2,
      },
      3: {
        type: 'INCOME',
        value: 24,
        comment: 'Some comment',
        id: 3,
      }
    }
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => {
        return(item.type == 'INCOME') ? acc += item.value : acc -= item.value;
         },0);
    },
    sortList() {
      if (this.buttonValue==2) {      
       return (Object.values(this.list).filter((list)=> list.type == 'INCOME'));
       } else  if (this.buttonValue==1) {   
            return (Object.values(this.list).filter((list)=> list.type));
          } else { return (Object.values(this.list).filter((list)=> list.type == 'OUTCOME'));
         }
    }
  },

  methods: {
    changebuttonValue(value){
      this.buttonValue=+value;
      // console.log(value, this.buttonValue);
    },
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj);
    },
    // onSortItems(id) {
    //   this.$set(this.buttonValue=id);
    // },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
