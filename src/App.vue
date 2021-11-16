<template>

  <div class="container mt-5">
    <h1 class="text-center">To-Do List</h1>
    <div class="row">
      <div class="col form-inline">
        <b-form-input v-model="newTask" placeholder="enter" @keyup.enter="add"></b-form-input>
        <b-button class="ml-3" variant="primary" @click="add">add</b-button> 
      </div>
    </div>

    <div class="row mt-5">
      <div class="col-md-3">
        <div class="p-2 first">
          <span contenteditable="true" class="title">Enter name</span>

          <draggable class="list-group column" :list="arrBacklog" group="tasks">
            <div class="list-group-item" v-for="(element, index) in arrBacklog" :key="index">
              {{element.name}}
              <div class="btn-trash" @click="deleteTask1(index)"><span class="fa fa-trash"></span></div>
             
            </div>
          </draggable>
          
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 second">
          <span contenteditable="true" class="title">Enter name</span>
          <draggable class="list-group column" :list="arrInProgress" group="tasks">
            <div class="list-group-item" v-for="(element, index) in arrInProgress" :key="index">
              {{element.name}}
              <div class="btn-trash" @click="deleteTask2(index)"><span class="fa fa-trash"></span></div>
             
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 third">
          <span contenteditable="true" class="title">Enter name</span>
          <draggable class="list-group column" :list="arrDone" group="tasks">
            <div class="list-group-item" v-for="(element, index) in arrDone" :key="index">
              {{element.name}}
              <div class="btn-trash" @click="deleteTask(index)"><span class="fa fa-trash"></span></div>
             
            </div>
          </draggable>
        </div>
      </div>


    </div> 
   <div class="button">Add board</div>
  </div>
  
</template>

<script>

  import draggable from "vuedraggable";
  

  export default {
    name: 'App',
    components: {
      draggable
    },
    data() {
      return {
        task: '',
        newTask: "",
        arrBacklog: [
          {name:"cleaning"},
          {name:"laundry"},
          {name:"reading"},
          {name:"music"},
        ],
        arrInProgress: [],
        arrDone: []
      }
    },
    methods:{
      add() {
        if(this.newTask) {
          this.arrBacklog.push({name: this.newTask});
          this.newTask="";
        }
      },
      deleteTask(index){
        this.arrDone.splice(index, 1);
      },
      deleteTask2(index){
        this.arrInProgress.splice(index, 1);
      },
      deleteTask1(index){
        this.arrBacklog.splice(index, 1);
      }
    }
  }
 

  
</script>

<style>


.column{
  min-height: 200px;
  text-align: center;
  cursor: pointer;
  margin: 10px 0;
}

.text{
  text-align: center;
}

.container{
  margin: 200px;
  padding-top: 0px;
}

.p-2 {
  border-radius: 15px;
  margin-bottom: 15px;
}
.title{
  padding: 5px;
  margin: 5px;

}
.title:hover{
  outline: 1px solid rgba(168,168, 168, .45);
}


.first{
  background-color: #fcd5ce;
  margin-bottom: 15px;
}

.second{
  background-color: #d8e2dc;
  margin-bottom: 15px;
}

.third{
  background-color: #ffd7ba;
}

.ml-3{
  background-color: #fec89a;
  border: none;

}
.ml-3:hover{
  background-color: darksalmon;
  border: none;
}

.button{
  height: 36px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #fcd5ce;
  border: none;
  width: 150px;
  cursor: pointer;
  position: absolute;
  bottom: 50px;
  left: 50%;
  transform: translate(-50%);
  color: white;
  border-radius: 3px;
  font-size: 20px;
}
.btn-trash{
  background-color: white;
  border: none;
  cursor: pointer;
  display: inline-block;
  transform: translate(50%);
}

</style>
