<template>
    <div class="item">
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
            true-value="1"
            false-value="0"
        />
        <span :class="[item.completed ? 'completed' : '', 'itemText']">{{item.name}} - Crée le {{formatDate(item.created_at)}} </span>
        <button @click="removeItem()" class="trashcan">
            <font-awesome-icon icon="trash"/>
        </button>
    </div>

</template>


<script>
import axios from 'axios';

export default{
    props: ['item'],
    methods:{
        updateCheck(){
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then(response => {
                if(response.status == 200){
                    console.log('emit itemchanged')
                    this.$emit('itemchanged');
                }
            })
            .catch(error => {
                console.log(error)
            })
        },
        removeItem(){
            axios.delete('api/item/' + this.item.id)
            .then(response => {
                if(response.status == 200){
                    this.$emit('itemchanged');
                }
            })
            .catch(error => {
                console.log(error)
            })
        },
        formatDate(datestr) {
            let date = new Date(datestr);
            return new Intl.DateTimeFormat('fr').format(date);
        }
    }
}
</script>

<style scoped>
.completed{
    text-decoration: line-through;
    color: #999999
}

.itemText{
    width: 100%;
    margin-left: 5px;
}

.item{
    display: flex;
    justify-content: center;
    align-items: center;
}

.trashcan{
    background-color: #fff;
    border: 0;
    padding: 6px 10px;
    border-radius: 8px;
    color: #10221B;
    outline: none;
    transition: scale .2s;
}

.trashcan:hover{
    cursor: pointer;
    scale: 1.2;
}
</style>