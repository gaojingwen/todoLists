<template>
    <div class='helper'>
        <span class="left">{{unFinishedTodoLength}}任务遗留</span>
        <span class="tabs">
            <span @click="stutasChange(site)" v-for='site in status' :key="site" :class="fliter === site?'actived':''">{{site}}</span>
        </span>
        <span class="clear" @click='clearAll'>clearAll</span>
    </div>
</template>

<script>
export default {
    data() {
        return {
            status: ['全部','没完成','已完成']
        }
    },
    props: {
        fliter: {
            type: String,
            require: true   
        },
        todos: {
            type: Array,
            require: true
        }
    },
    computed: {
        unFinishedTodoLength() {
            return this.todos.filter(todo => !todo.completed).length;
        }
    },
    methods: {
        stutasChange(site) {
            this.$emit('toggle', site)
        },
        clearAll() {
            this.$emit('clearAll')
        }
    }
}
</script>

<style lang="stylus" scoped>
    .helper {
        font-weight 100
        display flex
        justify-content space-between
        padding 5px 0
        line-height 30px
        background-color #ffffff
        font-size 14px
        font-smoothing: antialiased;
    }

    .left, .clear, .tabs {
        padding 0 10px
        box-sizing border-box
    }

    .left, .clear {
        width 150px
    }

    .left {
        text-align left
    }

    .clear {
        text-align: right
        cursor pointer
    }

    .tabs {
        width 200px
        display flex
        justify-content space-around
        * {
            display inline-block
            padding 0 10px
            cursor pointer
            border 1px solid rgba(175, 47, 47, 0)
            &.actived {
                border-color rgba(175, 47, 47, 0.4)
                border-radius 5px
            }
        }
    }

</style>