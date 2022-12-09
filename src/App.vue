<template>
  <div class="todo_list">
    <ol>
      <li @click="colorChange(itemCount)" 
          :class="{ listColorGreen: itemCount.completed }" 
          v-for="(itemCount, index) in todoList">{{ itemCount.item }} 
          <button class="deleteButton" 
          @click='removeItem(index)'>X</button>
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
      <option value="false">Not done</option>
      <option value="true">Done</option>
    </select>
    <button @click="addItem">Add</button>
  </form>
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
        localStorage.setItem('todoList', JSON.stringify(this.todoList));
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
    },
  },
  mounted() {
    // localStorage.setItem('todoList', JSON.stringify(this.todoList));
    if (localStorage.getItem('todoList')) {
      console.log(JSON.parse(localStorage.getItem('todoList')));
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
}

label {
  color: white;
  display: block;
}

input {
  display: block;
  font-size: 1em;
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
  font-size: 1em;
  display: block;
}
select {
  font-size: 1em;
}

.deleteButton {
  /* padding-right: 2%; */
  width: 7%;
  cursor: pointer;
  background-color: rgb(255, 50, 50);
  color: white;
}
</style>
