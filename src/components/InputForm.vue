<template>
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
</template>

<script>
export default {
  props: {
    array: Array,
    // newListItem: String,
    // completed: Boolean,
  },
  data() {
    return {
      newListItem: '',        /*Variable for putting value to list's array*/
      completed: false,
    }
  },
  methods: {
    addItem() {
      if(this.newListItem) {
        this.array.push({item: this.newListItem, completed: this.completed});
        this.updateList();
        this.inputClear();
      }
    },
    updateList() {
      localStorage.setItem('todoList', JSON.stringify(this.array));
    },
    // colorChange(object) {
    //   object.completed = !object.completed;
    // },
    inputClear() {
      this.newListItem = '';
    },
    clearAll() {
      this.array = [];
      this.updateList();
    },
    clearCompleted(){
      this.array = this.array.filter(item => !item.completed);
      this.updateList();
    },
  }
}
</script>
<style scoped>
.input_div {
  grid-area: 10 / 2 / 13 / -2;
  display: flex;
  flex-direction: column;
}

button {
  font-size: 0.7em;
  font-weight: bold;
  flex-grow: 1;
}

select {
  flex-grow: 1;
}


</style>