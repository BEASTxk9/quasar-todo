<template>
  <q-page class="bg-grey-3 column">
    <!-- add task -->
    <div class="row q-pa-sm bg-primary">

      <q-input
      filled
      bottom-slots
      v-model="newTask"
      @keyup.enter="addTask"
      class="col"
      square
      placeholder="Add Task"
      bg-colors="white"
      dense
      >

<template v-slot:append>
<q-btn @click="addTask" rounded dense flat icon="add" />
</template>

      </q-input>

    </div>

    <q-list class="bg-white" seperator bordered>
      <q-item v-for="(task, index) in tasks" :key="task.title" @click="task.done = !task.done"
        :class="{ 'done bg-blue-1' : task.done }" clickable v-ripple>
        <!-- checkboc -->
        <q-item-section avatar>
          <q-checkbox v-model="task.done" class="no-pointer-events" color="primary" />
        </q-item-section>
        <!-- data -->
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <!-- delete btn -->
        <q-item-section v-if="task.done" side>
          <q-btn
          @click.stop="confirm = true" flat round color="primary" icon="delete" />



        </q-item-section>
      </q-item>

    </q-list>
    <!-- no  tasks -->
    <div v-if="!tasks.length" class="no-tasks absolute-center">
      <q-icon name="check" size="100px" color="primary" />
      <div class="text-h5 text-primary text-center">
        No Tasks
      </div>
    </div>

  </q-page>

  <!-- confirm -->
  <q-dialog v-model="confirm" persistent>
      <q-card>
        <q-card-section class="row items-center">
          <q-avatar icon="delete" color="primary" text-color="white" />
          <span class="q-ml-sm">You are currently not connected to any network.</span>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="Cancel" color="primary" v-close-popup />
          <q-btn flat @click="deleteTask(index)" label="Confirm" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
</template>

<script>
import { colors } from 'quasar';
import { defineComponent } from 'vue';

export default defineComponent({
  data() {
    return {
      newTask: '',
      tasks: [
        // {
        //   title: 'Get food',
        //   done: false
        // },
        // {
        //   title: 'Make food',
        //   done: false
        // },
        // {
        //   title: 'Sleep',
        //   done: false
        // },
      ],
      confirm: false
    }
  },
  methods: {
    deleteTask(index){

    this.tasks.splice(index, 1),
    this.$q.notify('Task Deleted')

    },
    addTask(){
     this.tasks.push({
      title: this.newTask,
      done: false
     })
     this.newTask = ''
    }
  }
})
</script>

<style lang="scss">
.done {
  .q-item_label {
    text-decoration: line-through 1px solid black;
  }

  color: #bbb;
}

.no-tasks {
opacity: 0.5;
}
</style>
