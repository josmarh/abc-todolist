<template>
    <div class="add-item">
        <input type="text" v-model="item.name"/> 
        <button :class="[ item.name ? 'active': 'inactive', 'plus']" @click="addItem()">Save</button>
        <font-awesome-icon
            icon="plus-square" 
        />
    </div>
</template>

<script>
export default {
    data: function (){
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        addItem(){
            if (this.item.name == ''){
                return;
            }
            axios.post('api/item/store', {
                item: this.item.name
            })
            .then( response => {
                if (response.status == 201){
                    this.item.name = "";
                    this.$emit('reloadlist')
                }
            })
            .catch( error => {
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
    background: #f7f7f7;
    border: 0px;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
}
.plus {
    cursor: pointer;
    font-size: 20px;
}
.active {
    color: #00ce25
}
.inactive {
    color: #999999
}
</style>