<template>
    <div class="real-app">
        <input class="add-input" type="text" placeholder="想要做的事: " @keyup.enter='wantToDo'>

        <APP_items :todo='todo' v-for='todo in filterComputed' :key='todo.id' @del='deleteItem'></APP_items>

        <APP_tab :fliter='fliter' :todos='todos' @toggle='toggle' @clearAll='clearAll'> </APP_tab>
    </div>

  
</template>
<script>
import APP_items from './items.vue'
import APP_tab from './tab.vue'
let id = 0
export default {
    data() {
        return {
            todos: [],
            fliter: '全部'
        }
    },
    components: {
        APP_items,
        APP_tab
    },
    methods: {
        wantToDo(e) {
           if(e.target.value.trim()) {
                this.todos.unshift({
                id: id++,
                content: e.target.value.trim(),
                completed: false
            })
            e.target.value = ''
           }else {
               alert('想做啥子')
           }
        },
         toggle(site) {
            this.fliter = site
            
        },
        deleteItem(id) {
            this.todos.splice(this.todos.findIndex(todo => todo.id == id), 1)
        },
        clearAll() {
            this.todos = []
        }
    },
    computed: {
        filterComputed() {
            if(this.fliter == '全部') {
                // this.todos.fliter(todo, todo.computed === this.filter)
                return this.todos

            }
           const completed = this.fliter == '已完成'
           return this.todos.filter(todo => todo.completed == completed)

        }
       
    }
    
}
</script>

<style lang="stylus" scoped>
    .real-app {
        width 600px
        margin 0 auto
        box-shadow 0 0 5px #666
    }
    .add-input {
        position: relative;
        margin: 0;
        width: 100%;
        font-size: 24px;
        font-family: inherit;
        font-weight: inherit;
        line-height: 1.4em;
        border: 0;
        outline: none;
        color: inherit;
        box-sizing: border-box;
        font-smoothing: antialiased;
        padding: 16px 16px 16px 36px;
        border: none;
        box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
    }
</style>