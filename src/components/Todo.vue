<template>
  <v-app>
    <v-container>
      <v-card>
        <div class="text-center header">
          <!-- VueJS + FireStore -->
          <img src="./../assets/vuefire.png" alt="" width="250">
        </div>
        <div class="todo-container">
          <div class="d-flex">
            <v-text-field
            label="Add Todo"
            v-model="newTodo.todo"
            ></v-text-field>
            <v-btn
              class="mx-1"
              fab
              color="info"
              @click="onAddTodo"
            >
              <v-icon dark>
                mdi-plus
              </v-icon>
            </v-btn>
          </div>
          <div class="mytodolist" transition="scroll-y-transition">
            <div v-for="(todos, i) in myTodos" :key="i">
              <v-row class="perTodo" v-if="todos.status == 'incomplete'">
                <v-col cols="1" class="text-center">
                  <v-tooltip left>
                    <template v-slot:activator="{ on, attrs }">
                    <svg @click="toggleTodo(todos, i)" v-bind="attrs" v-on="on" xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-circle-dashed" width="24" height="24" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2196F3" fill="none" stroke-linecap="round" stroke-linejoin="round">
                      <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                      <path d="M8.56 3.69a9 9 0 0 0 -2.92 1.95" />
                      <path d="M3.69 8.56a9 9 0 0 0 -.69 3.44" />
                      <path d="M3.69 15.44a9 9 0 0 0 1.95 2.92" />
                      <path d="M8.56 20.31a9 9 0 0 0 3.44 .69" />
                      <path d="M15.44 20.31a9 9 0 0 0 2.92 -1.95" />
                      <path d="M20.31 15.44a9 9 0 0 0 .69 -3.44" />
                      <path d="M20.31 8.56a9 9 0 0 0 -1.95 -2.92" />
                      <path d="M15.44 3.69a9 9 0 0 0 -3.44 -.69" />
                    </svg>
                    </template>
                    <span>Mark as complete</span>
                  </v-tooltip>
                </v-col>
                <v-col>{{todos.todo}}</v-col>
                <v-col cols="3">
                  <span class="px-2">
                    <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-pencil point_me" width="24" height="24" viewBox="0 0 24 24" stroke-width="1.5" stroke="#009688" fill="none" stroke-linecap="round" stroke-linejoin="round">
                      <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                      <path d="M4 20h4l10.5 -10.5a1.5 1.5 0 0 0 -4 -4l-10.5 10.5v4" />
                      <line x1="13.5" y1="6.5" x2="17.5" y2="10.5" />
                    </svg>
                  </span>
                  <span class="px-2" @click="onClickDeleteTodo(i, todos)">
                    <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-trash point_me" width="24" height="24" viewBox="0 0 24 24" stroke-width="1.5" stroke="#F44336" fill="none" stroke-linecap="round" stroke-linejoin="round">
                      <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                      <line x1="4" y1="7" x2="20" y2="7" />
                      <line x1="10" y1="11" x2="10" y2="17" />
                      <line x1="14" y1="11" x2="14" y2="17" />
                      <path d="M5 7l1 12a2 2 0 0 0 2 2h8a2 2 0 0 0 2 -2l1 -12" />
                      <path d="M9 7v-3a1 1 0 0 1 1 -1h4a1 1 0 0 1 1 1v3" />
                    </svg>
                  </span>
                </v-col>
              </v-row>

              <v-row class="perTodo" v-else>
                <v-col cols="1" class="text-center">
                  <v-tooltip left>
                    <template v-slot:activator="{ on, attrs }">
                      <svg @click="toggleTodo(todos, i)" v-bind="attrs" v-on="on" xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-circle-check" width="24" height="24" viewBox="0 0 24 24" stroke-width="1.5" stroke="#9E9E9E" fill="none" stroke-linecap="round" stroke-linejoin="round">
                        <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                        <circle cx="12" cy="12" r="9" />
                        <path d="M9 12l2 2l4 -4" />
                      </svg>
                    </template>
                    <span>Mark as incomplete</span>
                  </v-tooltip>
                </v-col>
                <v-col><s style="color: gray">{{todos.todo}}</s></v-col>
                <v-col cols="3">
                  <span class="px-2">
                    <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-pencil point_me" width="24" height="24" viewBox="0 0 24 24" stroke-width="1.5" stroke="#009688" fill="none" stroke-linecap="round" stroke-linejoin="round">
                      <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                      <path d="M4 20h4l10.5 -10.5a1.5 1.5 0 0 0 -4 -4l-10.5 10.5v4" />
                      <line x1="13.5" y1="6.5" x2="17.5" y2="10.5" />
                    </svg>
                  </span>
                  <span class="px-2" @click="onClickDeleteTodo(i, todos)">
                    <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-trash point_me" width="24" height="24" viewBox="0 0 24 24" stroke-width="1.5" stroke="#F44336" fill="none" stroke-linecap="round" stroke-linejoin="round">
                      <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                      <line x1="4" y1="7" x2="20" y2="7" />
                      <line x1="10" y1="11" x2="10" y2="17" />
                      <line x1="14" y1="11" x2="14" y2="17" />
                      <path d="M5 7l1 12a2 2 0 0 0 2 2h8a2 2 0 0 0 2 -2l1 -12" />
                      <path d="M9 7v-3a1 1 0 0 1 1 -1h4a1 1 0 0 1 1 1v3" />
                    </svg>
                  </span>
                </v-col>
              </v-row>
            </div>
          </div>
        </div>
      </v-card>
    </v-container>

    <!-- snackbar -->
    <v-snackbar
      v-model="snackbar"
    >
      {{ message }}

      <template v-slot:action="{ attrs }">
        <v-btn
          color="pink"
          text
          v-bind="attrs"
          @click="snackbar = false"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </v-app>
</template>

<script>
import db from './../firebaseInit'
  export default {
    data: () => ({
      snackbar : false,
      message: '',
      myTodos: [],
      newTodo: {
        todo: '',
        status: 'incomplete',
      },
      toPush: {
        id: '',
        todo: '',
        status: 'incomplete',
      }
    }),
    created () {
      this.getMyTodos()
    },
    methods: {
      async getMyTodos(){
        await db.collection('todos').get()
        .then((querySnapshot) => {
          querySnapshot.forEach((fire) => {
            const data = {
              'id': fire.id,
              'todo': fire.data().todo,
              'status': fire.data().status,
            }
            this.myTodos.push(data)
          })
        })
      },
      async onAddTodo () {
        this.toPush.todo = this.newTodo.todo

        await db.collection('todos').add({
          todo: this.newTodo.todo,
          status: this.newTodo.status
        })
        .then((docRef) => {
          this.toPush.id = docRef.id
          this.myTodos.push(this.toPush)
          this.snackbar = true,
          this.message = 'Todo added'
        })
        .finally(() => {
          this.newTodo.todo = ''
        })
      },

      async onClickDeleteTodo(i, todo){
        console.log(i, todo.id)
        await db.collection('todos').doc(todo.id).delete()
        .then(() => {
          this.snackbar = true
          this.message = "todo deleted"
          this.myTodos.splice(i, 1)
        })
      },


      async watcher(){
        await db.collection('todos').querySnapshot((querySnapshot) => {
          this.myTodos = []
          if(querySnapshot){
            querySnapshot.forEach((doc) => {
              this.myTodos.push(doc)
            })
          }
        })
      },


      async toggleTodo(todos, i){
        if(todos.status == 'incomplete'){
          await db.collection('todos').doc(todos.id).update({
            status: 'complete'
          })
          .then(() => {
            this.myTodos = []
            this.getMyTodos()
          })
        }
        else{
          await db.collection('todos').doc(todos.id).update({
            status: 'incomplete'
          })
          .then(() => {
            this.myTodos = []
            this.getMyTodos()
          })
        }
        
        console.log(i)
      }
    }
  }
</script>
<style scoped>
  .header{
    font-size: 30px;
    padding: 10px 0px;
  }
  .todo-container{
    padding: 15px 0px;
    margin: auto;
    width: 70%;
  }
  .mytodolist{
    padding: 15px 0px;
  }
  .perTodo{
    background-color: #121212;
    border-radius: 10px;
    margin-bottom: 5px;
  }
  .point_me{
    cursor: pointer;
  }
</style>