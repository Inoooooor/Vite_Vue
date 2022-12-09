<template>
  <div class="todo_list">
    <ol>
      <li @click="colorChange(itemCount)" 
          :class="{ listColorGreen: itemCount.completed }" 
          v-for="(itemCount, index) in todoList">{{ itemCount.item }} 
          <button class="deleteButton" @click='removeItem(index)'>X</button>
      </li>
    </ol>
  </div>
  <form action="" class="input_div" @click.prevent>
    <label for="item_input">New list item
      <input v-model="newListItem" 
        required 
        type="text" 
        name="" 
        id="item_input" 
        placeholder="Ведро воды"
      ></label>
      <select
      v-model="completed" 
      name="colorSelect" 
      id="colorSelectId"
      placeholder=""
      required>
      <option value="">Not done</option>
      <option value="true">Done</option>
    </select>
    <button @click="addItem">Add</button>
    <button @click="clearAll">Clear all</button>
    <button @click="clearCompleted">Clear completed</button>  
  </form>
  <div class="list_templates">
    <button @click="plovRecipe" class="plov_template">Plov recipe</button>
    <button @click="antonQuote" class="anton">Anton's quote</button>
    <button @click="dailyList" class="regular_template">Daily list</button>
  </div>
</template>

<script>

export default {
  data() {
    return { todoList: [],
    newListItem: '',        /*Variable for putting value to list's array*/
    completed: false ,          /*Variable for putting color to list's item*/
    }
  },
  methods: {
    addItem() {
      if(this.newListItem) {
        this.todoList.push({item: this.newListItem, completed: this.completed});
        this.updateList();
        this.inputClear();
      }
    },
    colorChange(object) {
      object.completed = !object.completed;
    },
    inputClear() {
      this.newListItem = '';
    },
    removeItem(index) {
      this.todoList.splice(index, 1);
      this.updateList();
    },
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
    }
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

.todo_list {
  grid-area: 2 / 2 / 10 / -2;
  background-color: rgb(255, 153, 0);
  border-radius: 3%;
}

.input_div {
  grid-area: 10 / 2 / 13 / -2;
  display: flex;
  flex-direction: column;
}

label {
  color: white;
  display: block;
}

input {
  /* display: block; */
  font-size: 1em;
  flex-grow: 1;
  width: 100%;
}

ol {
  padding: 5%;
}

li {
  background-color: yellow;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
}

.listColorGreen {
  background-color: green;
}

button {
  font-size: 0.7em;
  font-weight: bold;
  flex-grow: 1;
  /* display: block; */
}
select {
  /* font-size: 1em; */
  flex-grow: 1;
}

.deleteButton {
  /* padding-right: 2%; */
  width: 7%;
  cursor: pointer;
  background-color: rgb(255, 50, 50);
  color: white;
  flex-grow: 0;
}

.list_templates {
  grid-area: 1 / 1 / 2 / 4;
}

.list_templates button {
  width: calc(100% / 3);
}
</style>
