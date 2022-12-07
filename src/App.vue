<template>
  <div class="todo_list">
    <ol>
      <li @click="changeColor()" :class="{ listColorGreen: itemCount.completed }" v-for="itemCount in todoList">{{ itemCount.item }} {{ itemCount.completed }}</li>
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
    return { todoList: [
      { item: 'Укроп', completed: true },
      { item: 'Кошачий жоп', completed: true },
      { item: '25 картошек', completed: false },
      { item: '17 мандавошек', completed: false },
    ],
    newListItem: '',        /*Variable for putting value to list's array*/
    completed: '' ,          /*Variable for putting color to list's item*/
    }
  },
  methods: {
    addItem() {
      if(this.newListItem && this.completed == 'false') {
        this.todoList.push({item: this.newListItem, completed: false});
        this.newListItem = '';
        this.completed = '';
      } else if (this.newListItem && this.completed == 'true') {
        this.todoList.push({item: this.newListItem, completed: true});
        this.newListItem = '';
        this.completed = '';
      }
       else {
        this.newListItem = '';
        this.completed = '';
        alert('Enter both');
      }
    },
    changeColor(itemIndex) {
      this.todoList[0].completed = (this.todoList[0].completed ? false : true);
      console.log(itemIndex)
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
  grid-area: 10 / 2 / 12 / -2;
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
</style>
