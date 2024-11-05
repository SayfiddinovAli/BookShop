<template>
  <div>
    <ul>
     <li v-for="item ,index of menu"
     :class="{active: page == index}"
     @click="page = index">
    {{ item }}</li>
    </ul>
    <addBook
     @createBook="createBook"
    :toggle="toggle"
    @closeModal="changeToggle"/>


    <div v-if="page == 0">
      <h1>Kitoblar ro'yhati
      <button @click="changeToggle(true)">Yangi kitob</button>
    </h1>
    <ListBooks :data="books"
    @removeBook="removeBook"/>

    </div>

    <div v-if="page == 1">
      <storeBooks/>
    </div>
  </div>
</template>
<script>
import ListBooks from '@/components/listBooks.vue'
import addBook from '@/components/addBook.vue'
import storeBooks from '@/components/storeBooks.vue';
import axios from 'axios'
export default {
  components:{
  ListBooks,
  addBook,
  storeBooks,
  },
  data() {
    return {
      menu:["Kitoblar ro'yxati" ,"Do'kon"],
      page:'books',
      toggle:false,
      books: [],
      url:'http://localhost:3000/Books'
    }
  },
  methods:{
    createBook(value){
      axios.post(this.url,value)
      .then((res)=>{
        this.books =[res.data , this.books];
      
        
      });
    },
    removeBook(id){
      axios.delete(`${this.url}/${id}`).then
      (()=>{
        this.books=this.books.filter((book)=>book.id !==id);
      });
    },
    getBooks(){
      axios.get(this.url).then((res)=>{
        this.books =[...res.data];
      });
    },
    changeToggle(value){
      this.toggle=value
    }
   
  },
  mounted() {
      this.getBooks();

    },
};
</script scoped>
<style>
  ul{
    display: flex;
    justify-content: center;
    gap: 10px;
    list-style-type: none;
  }
  ul li{
    text-decoration: underline;
    cursor: pointer;
  }
  ul li.active{
    color: red;
  }
</style>