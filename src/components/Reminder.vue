<template>
    <div class="container">
        <input 
            placeholder="some text" 
            autofocus 
            @keyup.enter="add"
            v-model="message"
        />
        <button @click="add">Add</button>
        <button @click="remove">Remove</button>
        <div class="reminder-container">
            <div class="item-wrapper">
                <transition-group name="reminder-list">
                    <div
                        v-for="(item,index) in items"
                        v-bind:key="item"
                        class="reminder-list-item"
                        @click="clickToRemove(index)"
                    >
                        {{item}}
                    </div>
                </transition-group>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                items:[1,2,3,4,5,6,7,8,9],
                message: undefined,
            }
        },
        methods:{
            add: function () {
                if(this.message != undefined){
                    const positionInList = 0
                    const howManyItemsToRemove = 0

                    this.items.splice(positionInList, howManyItemsToRemove, this.message)

                    this.message = undefined   
                }
            },
            remove: function () {
                const positionInList = 0
                this.items.splice(positionInList, 1)
            },
            clickToRemove: function(index) {
                console.log(index);
                this.items.splice(index, 1)

            }
        }
    }
</script>

<style scoped>

    .container{
        width:90%;
        background: blue;
    }


    .reminder-container{
        justify-content: center;
        display: flex;
    }

    .item-wrapper{
        position: relative;
        background: green;
        width: 60%;
        margin: 10px;
    }

    .reminder-list-item{
        transition: all 1s;
        background: red;
        width: 100%;
        border-bottom: 2px solid black;
        padding: 20px 0px 20px 10px;
    }

    .reminder-list-item:last-of-type{
        border:none;
    }

    .reminder-list-enter{
        opacity: 0;
        transform: translateX(-300px); 
    }

    .reminder-list-leave-to{
        opacity: 0;
        transform: translateX(300px);
    }

    .reminder-list-leave-active {
        position: absolute;
    }

</style>