<template>
  <q-page class="bg-grey-4 column">
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
          <q-item-section @click.stop="deleteTask(index)" v-if="task.done" side> <q-btn flat round color="negative" icon="delete" /></q-item-section>
        </q-item>
      </q-list>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        {
          title: 'hello 1',
            done: false
        },
          {
          title: 'hello 2',
          done: false
        },
        {
          title: 'hello 3',
          done: false
        }
        ]
      }
  },
  methods: {
    deleteTask(index) {
      this.tasks.splice(index, 1)
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
</style>