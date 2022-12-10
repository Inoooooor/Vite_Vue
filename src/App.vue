<template>
  <List 
    :array="todoList">
  </List>
  <InputForm
  :array="todoList"
   @clear-all="clearAll"
   @clear-completed="clearCompleted"
   ></InputForm>
  <ListTemplates
    @anton-quote="antonQuote"
    @plov-recipe="plovRecipe"
    @daily-list="dailyList">
  </ListTemplates>
</template>

<script>
import List from './components/List.vue'
import InputForm from './components/InputForm.vue'
import ListTemplates from './components/ListTemplates.vue'
export default {
  components: {
    List,
    InputForm,
    ListTemplates,
  },
  data() {
    return { 
    todoList: [],
    }
  },
  methods: {
    updateList() {
      localStorage.setItem('todoList', JSON.stringify(this.todoList));
    },
    clearAll() {
      this.todoList = [];
      this.updateList();
    },
    clearCompleted(){
      this.todoList = this.todoList.filter(item => !item.completed);
      this.updateList();
    },
    antonQuote() {
      this.todoList = [
        {item: 'Ты', completed: false},
        {item: 'Бы', completed: false},
        {item: 'И', completed: false},
        {item: 'В', completed: false},
        {item: 'Рот', completed: false},
        {item: 'Взял', completed: false},
      ];
      this.updateList();
    },
    plovRecipe() {
      this.todoList = [
        {item: 'Укроп', completed: false},
        {item: 'Кошачий жоп', completed: false},
        {item: '25 картошек', completed: false},
        {item: '17 мондовошек', completed: false},
        {item: 'Ведро воды', completed: false},
        {item: 'Хуй туды', completed: false},
        {item: 'Охапку дров', completed: false},
        {item: 'Плов готов', completed: false},
      ]
      this.updateList();
    },
    dailyList() {
      this.todoList = [
        {item: 'Eggs', completed: false},
        {item: 'Milk', completed: false},
        {item: 'Water', completed: false},
        {item: 'Bread', completed: false},
        {item: 'Butter', completed: false},
        {item: 'Whiskey', completed: false},
        {item: 'Cundoms', completed: false},
        {item: 'Lottery ticket', completed: false},
      ]
      this.updateList();
    },
  },
  mounted() {
    if (localStorage.getItem('todoList')) {
      const listContent = JSON.parse(localStorage.getItem('todoList'));
      this.todoList = listContent;
    }
  }
}

</script>

<style>
* {
  margin: 0;
  padding: 0;
  overflow: hidden;
}

body {
  font-size: 2rem;
  height: 100vh;
  width: 100vw;
  display: grid;
  grid-template: repeat(12, 1fr) / 1fr 600px 1fr;
}

#app {
  grid-area: 2 / 2 / -2 / 3;
  background-color: rgb(121, 38, 0);
  display: grid;
  grid-template: 5% repeat(10, 1fr) 5% / 1fr 90% 1fr;
}

.list_templates {
  grid-area: 1 / 1 / 2 / 4;
}

.list_templates button {
  width: calc(100% / 3);
}
</style>
