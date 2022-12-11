<template>
  <div class="todo_list">
    <ol>
        <transition-group name="fade">
          <li @click="colorChange(itemCount)" 
              :key="Math.random"
              :class="{ listColorGreen: itemCount.completed }" 
              v-for="(itemCount, index) in array">{{ itemCount.item }} 
              <button class="deleteButton" @click.stop='removeItem(index)'>X</button>
          </li>
        </transition-group>
    </ol>
  </div>
</template>

<script>
export default {
  props: {
    array: Array,               /* variable to get from parent */
  },
  methods: {
    removeItem(index) {
      this.array.splice(index, 1);
      this.updateList();
    },
    updateList() {
      localStorage.setItem('todoList', JSON.stringify(this.array));
    },
    colorChange(object) {
      object.completed = !object.completed;
      this.updateList();
    },
  }
}
</script>
<style scoped>
.todo_list {
  grid-area: 2 / 2 / 10 / -2;
  background-color: rgb(255, 153, 0);
  border-radius: 3%;
}
.listColorGreen {
  background-color: green;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s ease, background-color .5s;
}

.fade-enter-from, .fade-leave-active{
  opacity: 0;
}

.deleteButton {
  width: 7%;
  cursor: pointer;
  background-color: rgb(255, 50, 50);
  color: white;
  flex-grow: 0;
}

li {
  background-color: yellow;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
}

ol {
  padding: 5%;
}

button {
  font-size: 0.7em;
  font-weight: bold;
  flex-grow: 1;
}
</style>