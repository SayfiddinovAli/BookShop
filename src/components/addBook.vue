<template >
    <div class="modal"
    :class="{
        active:toggle,
        
    }"
    @click.self="closeModal" >
        <form @submit.prevent="addBook()">
            <h5>Yangi kitob</h5>
              <input type="text" v-model="book.name" placeholder="Kitob nomi">
              <input type="number" v-model="book.price" placeholder ="Kitob narxi">
              <input type="number" v-model="book.count" placeholder="Kitob soni">
              <button type="submit">Kiritish</button>
        </form>
    </div>
</template>
<script>
export default {
 props:["toggle"],
    data() {
        return {
            book:{},
        };
    },
    methods: {
        addBook(){
         this.$emit("createBook" , this.book);
         this.book={};
        this.closeModal();
        },
        closeModal(){
         this.$emit("closeModal",false);
        },
       
    }
}
</script>
<style scoped>
    .modal{
        position: fixed;
        width: 100vw;
        height: 100vh;
        background-color: rgb(0, 0, 0,0.5);
        align-items: center;
        justify-content: center;
        display: none;
    }
    .modal form{
      background-color: #fff;
      padding: 10px;
      display: flex;
      flex-direction: column;
      gap: 10;

    }
    .modal.active{
        display: flex;
    }
    h5{
        margin: 0;
        text-align: center;
    }
</style>