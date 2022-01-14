<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-pink-3">
      <q-input 
      @keyup.enter="addTask"
       class = "col bg-white q-pa-sm" 
        outlined v-model="newTask"
         placeholder="Add Text" 
         dense>
        <template v-slot:append>
          <q-btn 
          @click="addTask"
          round 
          dense 
          flat 
          icon="add" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-white"
    separator
    bordered>

      <q-item 
      v-for = "(task, index) in tasks"
      :key="task.title" 
      @click = "task.done = !task.done"
      :class=" {'done bg-pink-1': task.done} "
      clickable
      v-ripple>
        <q-item-section avatar>
          <q-checkbox v-model="task.done"
           class = "no-pointer-events"
           val="teal" color="pink-9" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>

        <q-item-section
        v-if = "task.done"
        side>
        <q-btn 
        @click.stop=deleteTask(index)
        dense
        flat round color="red"
         icon="delete" />
           
        </q-item-section>
      </q-item>

    </q-list>

    <div 
    v-if = "!tasks.length"
    class = "no-tasks absolute-center">
      <q-icon
      name = "check"
      size="100px"
      color = "grey">
         
      </q-icon>
        <div class="text-h5 text-grey text-center dense">
            No Tasks
        </div>
    </div>
  </q-page>
</template>

<script>


export default {
  data(){
     return {
       newTask: '',
       tasks: [
        //  {
        //    title: 'Get bananas',
        //    done: false
        //  },
        //  {
        //    title: 'Eat bananas',
        //    done: false
        //  },
        //  {
        //    title: 'Drink water',
        //    done: false
        //  },
       ]
     }
  },
  methods: {
    deleteTask(index){
        this.$q.dialog({
        title: 'Confirm',
        message: 'Completed task will be deleted permanently',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
         this.$q.notify('Task deleted')
      }).onCancel(() => {
        console.log('>>>> Cancel')
      })
      
    },
    addTask(){
      this.tasks.push({
        title: this.newTask,
        done: false
      })
       this.$q.notify('New task added')
      this.newTask = ""
    }
  }
   
}
</script>

<style lang="scss">
   .done{
     .q-item__label {
       text-decoration: line-through;
       color: #bbb;
     }
   }

   .no-tasks{
     opacity: 0.5;
   }
</style>