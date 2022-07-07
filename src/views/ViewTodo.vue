<template>
  <div class="home">
    <v-text-field
        v-model="newTaskTitle"
        class="pa-3"
        outlined
        label="Add Task"
        append-icon="mdi-plus"
        clearable
        @click:append="addTask"
    ></v-text-field>

    <v-list
        v-if="tasks.length"
        flat
        class="pt-0"
    >
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
            :class="{'green lighten-5':task.done}"
            @click="doneTask(task)"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                  :input-value="task.done"
                  color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                  :class="{'text-decoration-line-through':task.done}"
              >{{ task.todo }}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action
                @click.stop="deleteTask(task.id)"
            >
              <v-btn icon>
                <v-icon color="grey lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
    <div
        v-else
        class="no-tasks"
    >
      <v-icon
          size="100"
          color="primary"
      >
        mdi-check
      </v-icon>
      <div
      class="text-h5"
      >
        No Task
      </div>

    </div>
  </div>
</template>

<script>

export default {
  name: 'ViewTodo',
  data() {
    return {
      newTaskTitle: '',
      tasks: [
        {id: 1, todo: 'Wake up', done: false},
        {id: 2, todo: 'Do nothing', done: true},
        {id: 3, todo: 'Eat', done: true},
        {id: 4, todo: 'Enough for today', done: false},
      ]
    }
  },
  methods: {
    doneTask(e) {
      e.done = !e.done
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(t => t.id !== id)
    },
    addTask(e) {
      if (this.newTaskTitle.length === 0) return
      this.tasks.unshift({
        id: Date.now(),
        todo: this.newTaskTitle,
        done: false
      })
      this.newTaskTitle = ''
    }

  }

}
</script>

<style lang="sass">
  .no-tasks
    position: absolute
    top: 50%
    left: 50%
    transform:translate(-50%,-50%)
    opacity: 50%
    text-align: center

</style>
