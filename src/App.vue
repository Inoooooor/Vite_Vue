<template>
  <div class="todo_list">
    <ol>
      <li :class="{listColorYellow: notDone, listColorGreen: done }" v-for="itemCount in todoList">{{ itemCount.item }}</li>
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
      v-model="itemColor" 
      name="colorSelect" 
      id="colorSelectId"
      placeholder=""
      required>
      <option value="yellow">Not done</option>
      <option value="green">Done</option>
    </select>
    <button @click="addItem">Add</button>
  </form>
</template>

<script>

export default {
  data() {
    return { todoList: [
      { item: 'Укроп', color: 'yellow' },
      { item: 'Кошачий жоп', color: 'yellow' },
      { item: '25 картошек', color: 'yellow' },
      { item: '17 мандавошек', color: 'yellow' },
    ],
    newListItem: '',        /*Variable for putting value to list's array*/
    itemColor: '' ,          /*Variable for putting color to list's item*/
    notDone: true,
    done: false
    }
  },
  methods: {
    addItem() {
      if(this.newListItem && this.itemColor) {
        this.todoList.push({item: this.newListItem, color: this.itemColor});
      } else {
        console.log(this.itemColor)
        this.newListItem = '';
        this.itemColor = '';
        alert('Enter both');
      }
    },
    colorChoice() {
      if (this.itemColor = "yellow")
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

.listColorYellow {
  background-color: yellow;
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
