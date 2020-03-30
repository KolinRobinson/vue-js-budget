<template>
  <div id="app">
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list"
                @deleteItem="onDeleteItem"/>

  </div>
</template>

<script>
import BudgetList from "./components/BudgetList/BudgetList";
import TotalBalance from './components/TotalBalance/TotalBalance'
import Form from './components/Form/Form'

export default {
  name: 'app',
  components: {
    Form,
    TotalBalance,
    BudgetList
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 5200,
        comments: 'Зарплата',
        id: 1
      },
      2: {
        type: 'OUTCOME',
        value: -150,
        comments: 'Пополнение счета',
        id: 2
      }
    }
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce(
              (acc, item) => acc+item.value,
              0
      );
    },
  },
  methods: {
    onDeleteItem(id){
      this.$delete(this.list, id);
    },
    onFormSubmit(data){
      let newObj = {
        ...data,
        id: Object.keys(this.list).length * Math.random()*1000
      };

      this.$set(this.list, newObj.id, newObj);
    }
  }
};
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
