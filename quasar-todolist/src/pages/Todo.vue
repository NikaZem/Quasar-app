<template>
  <q-page class="bg-grey-3 column q-pa-lg">
    <div class="row q-pa-sm bg-positive">
      <q-input @keyup.enter="addTask" bg-color="white" class="col" square filled v-model="newTask" label="Todo" placeholder="Add some task" dense >
        <template v-slot:append> 
          <q-btn @click="addTask" color="primary" round dense flat icon="send" />
        </template>
      </q-input>
    </div>
    <q-list separator bordered>
      <q-item @click="task.done = !task.done" :class="{ 'done bg-blue-2': task.done }" v-for="(task, index) in tasks" :key="task.title" tag="label" v-ripple>
        <q-item-section avatar>
          <q-checkbox v-model="task.done" val="teal" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn @click.stop="deleteTask(index)" flat round color="primary" icon="delete" />
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="!tasks.length" class="no-tasks absolute-center">
      <q-icon name="check" size="150px" color="positive"/>
      <div class="text-h4 text-positive text-center">Yeti completed all tasks</div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [
       /*  {
          id: 1,
          title: 'hello', 
          done: true
        },
        {
          id: 2,
          title: 'hello2', 
          done: false
        },
        {
          id: 3,
          title: 'hello3', 
          done: false
        } */
      ]
    }
  },
  methods: {
    deleteTask(index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Do you really want to delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify({
          message: 'Yeti deleted your todo.',
          color:'accent',
          avatar: 'https://img.freepik.com/free-photo/purple-yeti-cartoon-on-bicycle_23-2150248730.jpg?w=996&t=st=1685908119~exp=1685908719~hmac=11c91ff45b4a8ce515d67169390831ba79ab2d04af5aead9af9d3eb0c47c7275'
        })
      })   
    },
    addTask() {
      this.tasks.push(
        {
          title: this.newTask, 
          done: false
        }
      )
      this.newTask = ''
    }
  }
}
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: grey;
  }
}
.no-tasks {
  opacity: 0.5;
}
</style>
