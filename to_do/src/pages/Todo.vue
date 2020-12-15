<template>
  <q-page class="bg-grey-3 coloumn">
    <div class="row q-pa-sm bg-primary">
     <q-input
      placeholder="Add Task" 
      class="col"
      @keyup.enter="addTask"
      filled
      square 
      bg-color="white"
      v-model="newTask" 
 
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
   <q-list 
   class="bg-white"
   separator
   bordered>
      <q-item 
       v-for="(task,index) in tasks"
       :key="task.titles"
       @click="task.done=!task.done"
       :class="{'done bg-blue-1':task.done}"
       clickable
       v-ripple>
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-event"
            color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.titles}}</q-item-label>
        </q-item-section>
        <q-item-section 
        v-if="task.done"
        side>
        <q-btn 
        @click.stop="deleteTask(index)"
        flat
        round 
        dense
        color="negative" 
        icon="delete" />

        </q-item-section>
      </q-item>


    </q-list>
    <div 
      v-if="!tasks.length"
      class="no-tasks absolute-center">
      <q-icon 
      name ="check"
      size="100px"
      color="primary"/>
      <div class="text-h5 text-primary text-center">
        No Task
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks:[

      ]
    }
  },
  methods: {
    deleteTask(index){
        this.$q.dialog({
        title: 'Confirm',
        message: 'Really Delete the Task ?',
        cancel: true,
        persistent: true
        }).onOk(()=>{
        this.tasks.splice(index,1)
        this.$q.notify('Task Deleted !')
        })

    },
    addTask(){
      this.tasks.push({
        titles:this.newTask,
        done:false
      })
      this.newTask=''
    }

  },
  


}
</script>
<style lang="scss">
  .done{
    .q-item__label{
      text-decoration: line-through;
      color: rgb(168, 166, 166);
    }
  }
.no-tasks{
  opacity: 0.5;
}
</style>