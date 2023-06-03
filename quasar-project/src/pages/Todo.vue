<template>
  <q-page class="bg-grey-4 column">
    <input @keyup.enter="addTask" class="todo_input" placeholder="Добавить задачу" v-model="newTask">
    <button :disabled="!newTask" @click="addTask" class="todo_input_btn">Добавить задачу</button>



    <q-list separator bordered>
        <q-item
          @click="task.done = !task.done"
          clickable
          :class="{ done: task.done }"
          v-for="(task, index) in tasks" :key="task.title" v-ripple>
            <q-item-section avatar>
              <q-checkbox class="no-pointer-events" v-model="task.done" val="teal" color="primary" />
            </q-item-section>
            <q-item-section>
              <q-item-label class="task_title">{{ task.title }}</q-item-label>
            </q-item-section>
            <q-item-section @click.stop="deleteTask(index)" v-if="task.done" side> <q-btn  flat round color="negative" icon="delete" /></q-item-section>
          </q-item>
      </q-list>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [
        ]
      }
  },
  methods: {
    deleteTask(index) {
      this.$q.dialog({
        title: 'Предупреждение',
        message: 'Вы точно хотите удалить задачу?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1),
          this.$q.notify({
            message: 'Задача удалена!',
            color: 'primary',
          })
        })
    },
    addTask() {
      // if (this.newTask == 0) {
      //   disabled
      // }else
      this.tasks.push({
        title: this.newTask,
        done: false,
      });
      this.newTask = ''
      }
    }
  }

</script>


<style lang="scss">
.done{
  background-color: blueviolet;
  .q-item__label{
    text-decoration: line-through;
    color: rgb(86, 181, 30);
  }
}
.task_title{
  font-size: 20px;
}
.todo_input{
  width: 100%;
  font-size: 20px;
  color: #fff;
  padding: 5px 10px;
  background-color: $primary;
  margin-right: 20px;
}
.todo_input_btn{
  font-size: 26px;
  text-align: center;
  color: #fff;
  background-color: green;
  padding: 20px 0;
  cursor: pointer;
}


</style>