<template>
    <div class="todolist-container">
        <div class="heading">
            <h2 id="title">Exercice - Todo-List !</h2>
            <add-item-form 
            v-on:reloadlist="getList()"/>
        </div>
        <list-view
        :items="items"
        v-on:reloadlist="getList()"/>
    </div>
</template>

<script>
import axios from 'axios';
import addItemForm from './addItemForm';
import ListView from './listView.vue';

export default{
    components: {
        addItemForm,
        ListView
    },
    data: function(){
        return {
            items: []
        }
    },
    methods: {
        getList() {
            axios.get('api/items')
            .then(response => {
                console.log("get list was called!")
                this.items = response.data
            })
            .catch(error => {
                console.log(error)
            })
        }
    },
    created(){
        this.getList();
    }
}

</script>


<style scoped>
.todolist-container{
    width: 50vw;
    margin: auto;
    background-color: rgb(34, 155, 110);
    border-radius: 8px;
}

.heading{
    padding: 10px;
}

#title{
    text-align: center;
}
</style>


<!-- Font handling, this way was the quickest to put together for me, but there are better ways :) --Donovan -->
<style>
.heading, span{
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    color: white;
}

input{
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

</style>