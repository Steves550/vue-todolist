<template>
<div class="task-container">
    <h4>{{ currentDay }}</h4>
    <h5>{{ date }}</h5>
   <div class="input-group mb-3" id="input-task">
     <input type="text" class="form-control" placeholder="Add Task..."   v-model="title"  @keyup.enter="taskAdd">
        <div class="input-group-append">
         <button v-on:click="taskAdd" class="btn btn-outline-primary" type="button" id="button-task">Add</button>
        </div>
   </div>
   <div class="list-group">
       <a  v-for="task in tasks" v-bind:key="task.id" href="#" class="list-group-item list-group-item-action">
          <input type="checkbox" v-model="task.complete">
            <span id="task-text" :class="{ completed : task.complete }">{{ task.title }}</span> 
             <button v-on:click="removeTask(task)" id="remove-btn" type="button" class="btn btn-outline-danger"><i class="fas fa-trash-alt"></i></button>
       </a>
       <div class="buttons-group">
       <button v-on:click="clearCompleted(task)" id="completed-btn" type="button" class="btn btn-outline-success clearChecked-btn">Clear Completed</button>
       <button v-on:click="clearAll(task)" id="remove-btn" type="button" class="btn btn-outline-danger remove-all">Clear All</button>
       </div>
   </div>
   
</div>
</template>

<script>
    export default {
        name: 'AddTask',
        data() {
            return {
                tasks: [],
                title: "",
                id: 0,
                date: '',
                currentDay: []
            }     
        },
        methods : {

            getDate() {
                this.date = new Date().toJSON().slice(0,10).replace(/-/g,'/');
               
            },

            getTheDay(){
                let theDate = new Date();

                let weekDay = ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];

                this.currentDay = weekDay[theDate.getDay()]
            },

            taskAdd() {
            if(this.title === '') {
                alert('Please add a task')
             } else {
              this.tasks.push({
                 id: this.id,
                 title: this.title,
                 complete: false
               })
               
              this.title = ''
              this.id++
             }
            },
            
            removeTask(task) {
                const index = this.tasks.indexOf(task);
                this.tasks.splice(index, 1);
            },

            clearAll() {
                this.tasks = [];
            },

            clearCompleted() {
                this.tasks = this.tasks.filter(this.notCompleted);
            },

            notCompleted(task) {
                return ! this.isCompleted(task)
            },

            isCompleted(tasks) {
                return tasks.complete;
            }
        },

        mounted(){
            this.getDate();
            this.getTheDay();
        }
      }

</script>

<style>
.task-container {
height: auto;
 margin: auto;
 width: 500px;
 padding: 25px;
 background-color: #f7f7f7;
}

 h5 {
     padding-bottom: 10px;
 }

 ul {
     list-style: none;
 }

 #task-text {
     
     margin-left: 20px;
     font-size: 18px;
 }

.completed {
    text-decoration: line-through;
}

 #remove-btn {
     float: right;
 }

 .clearChecked-btn {
    width: 200px;
    margin-left: 10px;
 }

 .remove-all {
     width: 200px;
     margin-right: 10px;
 }

 .buttons-group {
     margin-top: 20px;
 }

 @media (max-width: 468px) {
   .task-container {
       width: 300px;
   }
}

@media (max-width: 580px) {
    .clearChecked-btn {
        margin-left: 25px;
    }
}

@media (max-width: 580px) {
    .remove-all {
        margin-right: 25px;
        margin-top: 8px;
    }
}
</style>