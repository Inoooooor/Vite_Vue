<template>
  <div class="todo_list">
    <ol>
        <transition-group name="fade">
          <li @click="colorChange(itemCount)" 
              :key="Math.random"
              :class="{ listColorGreen: itemCount.completed }" 
              v-for="(itemCount, index) in todoList">{{ itemCount.item }} 
              <button class="deleteButton" @click.stop='removeItem(index)'>X</button>
          </li>
        </transition-group>
    </ol>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0
    }
  }
}
</script>
