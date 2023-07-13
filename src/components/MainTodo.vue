<script setup>
import { ref } from 'vue';
const todoRef = ref('');
const todoListRef = ref([]);
const addTodo = ()=>{
  console.log(todoRef.value); //script内でリアクティブな変数の値を得る場合、 .value　を付ける必要がある
  //ミリ秒を簡易的なIDとして登録する
  const id = new Date().getTime();
  //入力したToDoを配列に格納
  todoListRef.value.push({id: id, task: todoRef.value});
  //ローカルストレージに登録
  localStorage.todoList = JSON.stringify(todoListRef.value);

  //登録後は入力欄を空にする
  todoRef.value = '';
}
</script>

<template>
  <div class="box_input">
    <input type="text" class="todo_input" v-model="todoRef" placeholder="+ ToDoを入力">
    <button class="btn" @click="addTodo">追加</button>
  </div>
  {{ todoRef }}
</template>

<style scoped>
.box_input {
  margin-top: 20px;
}

.todo_input {
  width: 300px;
  margin-right: 8px;
  padding: 8px;
  font-size: 18px;
  border: 1px solid #aaa;
  border-radius: 6px;
}

.btn {
  padding: 8px;
  background-color: #03a9f4;
  border-radius: 6px;
  color: #fff;
  text-align: center;
  font-size: 14px;
}
</style>