<template>
  <q-page class="bg-grey-3 column q-pa-lg">
    <q-list separator bordered>
      <q-item @click="task.done = !task.done" clickable :class="{ 'done bg-yellow-3': task.done }" v-for="(task, index) in tasks" :key="task.title" tag="label" v-ripple>
        <q-item-section avatar>
          <q-checkbox class="no-pointer-events" v-model="task.done" val="teal" color="$primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn @click.stop="deleteTask(index)" flat round color="primary" icon="delete" />
        </q-item-section>
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
.done {
  .q-item__label {
    text-decoration: line-through;
    color: grey;
  }

}
</style>
