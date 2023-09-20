<template>
  <div class="container">
    <main class="py-4" style="margin-left: 2% !important">
      <div class="row justify-content-center col-12">
        <div class="col-md-10">
          <h1 class="">Libros</h1>
          
          <form @submit.prevent="editItem(itemE)" v-if="modeEdit">
            <div class="form-group col-6">
              <label for="">ID User</label>
              <input type="number" class="form-control mb-2"
                v-model="itemE.userId">
            </div>
            <div class="form-group form-group col-6">
              <label for="">ID</label>
              <input type="number" class="form-control mb-2"
            v-model="itemE.id"></div>
            <div class="form-group form-group col-12">
              <label for="">Title</label>
              <input type="text" class="form-control mb-2"
            v-model="itemE.title"></div>
            <div class="form-group form-group col-6">
              <label for="">Completed</label>
              
                <select class="form-select" v-model="itemE.completed">
                <option selected>[Seleccione]</option>
                <option value="false">false</option>
                <option value="true">true</option>
              </select>
              
              
            </div> 
            <button class="btn btn-warning m-1" type="submit">Editar</button>
            <button class="btn btn-danger" type="submit"
                @click="cancelEdit">Cancelar</button>
                        
        </form>   
          <table class="table table-bordered">
              <thead>
                  <tr>
                      <th scope="col">#</th>
                      <th scope="col">ID User</th>
                      <th scope="col">ID</th>
                      <th scope="col">Title</th>
                      <th scope="col">Completed</th>
                      <th scope="col">Acciones</th>
                  </tr>
              </thead>
              <tbody>
                  <tr v-for="(item, index) in items">
                      <th scope="row">{{ index+1 }}</th>
                      <td>{{ item.userId }}</td>
                      <td>{{ item.id }}</td>
                      <td>{{ item.title }}</td>
                      <td>{{ item.completed }}</td>            
                      <td class="text-center">
                        <button class="btn btn-warning btn-sm m-1"
                          data-toggle="tooltip" data-placement="left" title="Editar"
                          @click="editForm(item, index)"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-gear" viewBox="0 0 16 16">
                          <path d="M8 4.754a3.246 3.246 0 1 0 0 6.492 3.246 3.246 0 0 0 0-6.492zM5.754 8a2.246 2.246 0 1 1 4.492 0 2.246 2.246 0 0 1-4.492 0z"/>
                          <path d="M9.796 1.343c-.527-1.79-3.065-1.79-3.592 0l-.094.319a.873.873 0 0 1-1.255.52l-.292-.16c-1.64-.892-3.433.902-2.54 2.541l.159.292a.873.873 0 0 1-.52 1.255l-.319.094c-1.79.527-1.79 3.065 0 3.592l.319.094a.873.873 0 0 1 .52 1.255l-.16.292c-.892 1.64.901 3.434 2.541 2.54l.292-.159a.873.873 0 0 1 1.255.52l.094.319c.527 1.79 3.065 1.79 3.592 0l.094-.319a.873.873 0 0 1 1.255-.52l.292.16c1.64.893 3.434-.902 2.54-2.541l-.159-.292a.873.873 0 0 1 .52-1.255l.319-.094c1.79-.527 1.79-3.065 0-3.592l-.319-.094a.873.873 0 0 1-.52-1.255l.16-.292c.893-1.64-.902-3.433-2.541-2.54l-.292.159a.873.873 0 0 1-1.255-.52l-.094-.319zm-2.633.283c.246-.835 1.428-.835 1.674 0l.094.319a1.873 1.873 0 0 0 2.693 1.115l.291-.16c.764-.415 1.6.42 1.184 1.185l-.159.292a1.873 1.873 0 0 0 1.116 2.692l.318.094c.835.246.835 1.428 0 1.674l-.319.094a1.873 1.873 0 0 0-1.115 2.693l.16.291c.415.764-.42 1.6-1.185 1.184l-.291-.159a1.873 1.873 0 0 0-2.693 1.116l-.094.318c-.246.835-1.428.835-1.674 0l-.094-.319a1.873 1.873 0 0 0-2.692-1.115l-.292.16c-.764.415-1.6-.42-1.184-1.185l.159-.291A1.873 1.873 0 0 0 1.945 8.93l-.319-.094c-.835-.246-.835-1.428 0-1.674l.319-.094A1.873 1.873 0 0 0 3.06 4.377l-.16-.292c-.415-.764.42-1.6 1.185-1.184l.292.159a1.873 1.873 0 0 0 2.692-1.115l.094-.319z"/>
                          </svg></button>
                          <button class="btn btn-danger btn-sm"
                          data-toggle="tooltip" data-placement="left" title="Eliminar"
                          @click="eliminateItem(item, index)"
                          >
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash" viewBox="0 0 16 16">
                            <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5Zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5Zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6Z"/>
                            <path d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1ZM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118ZM2.5 3h11V2h-11v1Z"/>
                            </svg>
                          </button>
                    </td>            
                  </tr>
              </tbody>
          </table>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios';
    export default {
        data() {
            return {
                items: [],
                itemE: {
                    index : 0,
                    userId: 0,
                    id: '',
                    title: '',
                    completed: false,
                },
                modeEdit: false,
                columnDefs: [
                  { headerName: "UserId", field: "userId" },
                  { headerName: "id", field: "id" },
                  { headerName: "Title", field: "title" },
                  { headerName: "Completed", field: "completed" },
                ],
                rowData: [
                  { make: "Toyota", model: "Celica", price: 35000 },
                  { make: "Ford", model: "Mondeo", price: 32000 },
                  { make: "Porsche", model: "Boxster", price: 72000 },
                ]
            }
        },
        methods:{
          editForm(item, index){
                this.itemE.index = index;
                this.itemE.userId = item.userId;
                this.itemE.id = item.id;
                this.itemE.title = item.title;
                this.itemE.completed = item.completed;
                this.modeEdit = true;
            },
            editItem(itemE){
              const dataOld = JSON.parse(localStorage.getItem('data'))
              dataOld.data[itemE.index].userId = itemE.userId
              dataOld.data[itemE.index].id = itemE.id
              dataOld.data[itemE.index].title = itemE.title
              dataOld.data[itemE.index].completed = itemE.completed
              this.modeEdit = false;
              localStorage.setItem("data", JSON.stringify(dataOld));
              this.items = dataOld.data
            },
            cancelEdit(){
                this.modeEdit = false;
            },
            eliminateItem(item, index){ 
              const confirmacion = confirm(`Eliminar item ${item.id}`);
              if(confirmacion){
                const dataOld = JSON.parse(localStorage.getItem('data')) 
                dataOld.data.splice(index, 1) 
                localStorage.setItem("data", JSON.stringify(dataOld));
                this.items = dataOld.data
              }
            }
        },
        mounted() {
            axios.get('https://jsonplaceholder.typicode.com/todos/')
                    .then(
                        res =>{
                            this.items = res.data;
                            localStorage.setItem("data", JSON.stringify(res));
                            })
        }
    }
</script>
