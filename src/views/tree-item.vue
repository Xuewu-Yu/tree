<template>
    <div class="my_tree" v-if="treeData.length">
        <div class="item" v-for="x,y in treeData" :key="y">
            <div class="item_title">
                <i v-if="x.child.length" :class="x.show?'el-icon-caret-bottom':'el-icon-caret-right'" @click.stop="handleIcon(x)"></i>
                <input type="checkbox" v-if="showCheck" @change="change(x,$event)" v-model="x.checked" />
                <span>{{x.name}}</span>
            </div>
            <div v-if="x.child.length && x.show" class="item_children">
                <tree-item :list="x.child" :showCheck="showCheck"></tree-item>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name:'TreeItem',
    props:{
        list:{
            type:Array,
            default:()=>{
                return []
            }
        },
        showCheck:{
            type:Boolean,
            default:true
        }
    },
    data(){
        return {
           treeData:[],
        }
    },
    mounted(){
        this.treeData = [...this.list]
    },
    methods:{
        change(a,event){
            let checked = event.target.checked;
            let fn = (data)=>{
                data.map(item=>{
                    item.checked = checked;
                    if(item.child && item.child.length){
                        fn(item.child)
                    }
                });
            }
            fn([a])
        },
        handleIcon(x){
            x.show = !x.show;
        }
    }
}
</script>
<style lang="scss" scoped>
.my_tree{
    .item{
        .item_title{
            margin: 10px 0;
            span{
                margin-left: 10px;
            }
        }
        .item_children{
            padding-left: 40px;
        }
    }
}
</style>