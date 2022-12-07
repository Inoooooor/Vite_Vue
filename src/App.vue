<template>
  <div class="todo_list">
    <ol>
      <li v-for="itemCount in todoList">{{ itemCount.item }}</li>
    </ol>
  </div>
  <form action="" class="input_div" @click.prevent>
    <label for="item_input">New list item<input v-model="newListItem" 
      required 
      type="text" 
      name="" 
      id="item_input" 
      placeholder="Ведро воды"
      ></label>
    <button v-on:click="addItem">Add</button>
  </form>
</template>

<script>

export default {
  data() {
    return { todoList: [
      { item: 'Укроп' },
      { item: 'Кошачий жоп' },
      { item: '25 картошек' },
      { item: '17 мандавошек' },
    ],
    newListItem: ''
    }
  },
  methods: {
    addItem() {
      if(this.newListItem) {
        this.todoList.push({item: this.newListItem});
      }
      this.newListItem = ''
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

button {
  font-size: 1em;
}
</style>
