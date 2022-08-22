<template>
    <div class="add-item">
        <input type="text" v-model="item.name" placeholder="Tâche à ajouter..." @keyup.enter="addItem()"/>
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            :class="[item.name ? 'active' : 'inactive', 'plus']"
        />
    </div>

</template>

<script>
import axios from 'axios';

export default{
    data: function() {
        return{
            item:{
                name: ""
            }
        }
    },
    methods:{
        addItem(){
            if(this.item.name == ''){
                return;
            }

            axios.post('api/item/store', {
                item: this.item
            })
            .then(response => {
                if(response.status == 201){
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            })
            .catch(error => {
                console.log(error)
            })
        }
    }
}

</script>

<style scoped>
.add-item{
    display: flex;
    justify-content: center;
    align-items: center;
}

input{
    border: 0;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
}

.plus{
    font-size: 24px;
}

.plus.active{
    color: #fff;
    transition: scale .2s;
}

.plus.active:hover{
    scale: 1.2;
    cursor: pointer;
}

.plus.inactive{
    color: #0d3526;
}

</style>