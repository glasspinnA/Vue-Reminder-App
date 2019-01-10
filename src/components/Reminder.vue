<template>
    <div class="containe">
        <button @click="add">Add</button>
        <button @click="remove">Remove</button>
        <transition-group name="reminder-list" tag="ul">
            <li 
                v-for="item in items"
                v-bind:key="item"
                class="reminder-list-item"
            >
                {{item}}
            </li>
        </transition-group>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                items:[1,2,3,4,5,6,7,8,9],
                nextNum: 10
            }
        },
        methods:{
            add: function () {
                const topOfList = 0
                const howManyItemsToRemove = 0
                this.items.splice(topOfList, howManyItemsToRemove, this.nextNum++)
            },
            remove: function () {
                const topOfList = 0
                this.items.splice(topOfList, 1)
            },
        }
    }
</script>

<style scoped>
    .reminder-list-item{
          transition: all 1s;
    }

    .reminder-list-enter, .reminder-list-leave-to{
        opacity: 0;
        transform: translateY(30px);
    }
    
    .reminder-list-leave-active {
        position: absolute;
    }
</style>