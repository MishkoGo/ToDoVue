<script setup>
import { ref, onMounted } from 'vue'
// реактивное состояние
const count = ref(0)
// функции, изменяющие состояние и запускающие обновление
function increment(){
  count.value++
}
// хуки жизненного цикла
onMounted(() => {
  console.log(`Начальный счет: ${count.value}.`)
})
</script>

<template>
  <button @click = "increment">Счетчик: {{ count }}</button>
</template>


<!-- Опциональный API -->
<!-- <script>
// import { createApp, ref } from 'vue'

export default{
  // Свойства, возвращенные из data(), переходят в реактивное состояние
  // и отправляются в this
  data(){
    return {
      count: 0
    }
  },
  // Методы – это функции, которые изменяют состояние и инициируют обновление.
  // Их можно привязать как обработчики событий в шаблонах.
  methods: {
    increment(){
      this.count++
    }
  },

  // Хуки жизненного цикла вызываются на разных этапах
  // жизненный цикл компонента
  // Эта функция будет вызвана при монтаже компонента.

  mounted(){
    console.log(`начальный счет: ${this.count}.`)
  }
}
// let count = ref(0);
</script>

<template>
  <button @click="increment">Счетчик: {{ count }}</button>

  <div id="app">
  <button @click="count++">
    Рахунок: {{ count }}
  </button>
</div> -->
<!--   
</template>

<style scoped>

</style> --> 
