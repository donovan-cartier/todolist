<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <list-item
                :item="item"
                class="item"
                v-on:itemchanged="$emit('reloadlist')"
            />
        </div>
    </div>

</template>


<script>
import listItem from "./listItem";

export default{
    props: ['items'],
    components:{
        listItem
    }
}
</script>

<style scoped>
.item{
    padding: 10px;
    border-top: 2px dashed #2c664f;
}
</style>