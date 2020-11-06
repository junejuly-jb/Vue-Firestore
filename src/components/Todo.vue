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
            ></v-text-field>
            <v-btn
              class="mx-1"
              fab
              color="info"
            >
              <v-icon dark>
                mdi-plus
              </v-icon>
            </v-btn>
          </div>
          <div class="mytodolist">
            <div class="perTodo">
              <v-row>
                <v-col cols="2" class="text-center">icons</v-col>
                <v-col>Todo</v-col>
                <v-col cols="3">Actions</v-col>
              </v-row>
            </div>
          </div>
        </div>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
     
    }),
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
  }
</style>