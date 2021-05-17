<template>
  <div id="tree">
    <div class="col-3">
      <tree-item :list="list" :showCheck="showCheck" />
    </div>
    <div class="col-3">
      <div v-for="x,y in selectData" :key="y">{{x.name}}</div>
    </div>
  </div>
</template>
 <script>
// import json from '@/mock/json.json'
// import $ from "jquery";
import TreeItem from "./tree-item";
export default {
  props:{
    // 树数据
    list:{
      type:Array,
      default:()=>{
        return [];
      }
    },
    // 默认是否展开
    showChild:{
      type:Boolean,
      default:true
    },
    // 复选框
    showCheck:{
      type:Boolean,
      default:true
    }
  },
  data() {
    return {
      selected:[],
    };
  },
  components: {
    TreeItem,
  },
  mounted() {
    this.$nextTick(()=>{
      this.initData()
    })
  },
  updated(){
    this.initData();
  },
  watch:{
    
  },
  computed:{
    selectData(){
      let arr = [];
      let fn = (data) => {
        data.map(item=>{
          if(item.checked){
            arr.push(item)
          }
          if(item.child && item.child.length){
            fn(item.child);
          }
        })
      }
      fn(this.list);
      return arr.filter(item=>item.name != 'root');
    }
  },
  methods: {
    initData(){
      let func = (data) => {
        data.map(item=>{
          item.show = this.showChild;
          if(item.child&&item.child.length){
            func(item.child)
          }
        })
      }
      func(this.list);
    },
    // render(data) {
    //   for (let i = 0; i < data.length; i++) {
    //     let str = "";
    //     str = `<input type="checkbox"></input><li><a>${data[i].name}</a><ul>`;
    //     this.html += str;
    //     if (data[i].child && data[i].child.length > 0) {
    //       this.render(data[i].child);
    //       // console.log(data[i])
    //     }
    //     this.html += `</ul></li>`;
    //     // console.log(this.html);
    //   }
    //   this.el.innerHTML = this.html;
    // },
    // addListener() {
    //   let show = true,
    //     that = this;
    //   $("span").on("click", function () {
    //     show = !show;
    //     if (show) {
    //       // $(this).parent().hide(200, "linear");
    //     } else {
    //       // $(this).parent().show(200, "linear");
    //     }
    //   });

    //   $("input").on("click", function () {
    //     // console.log($(this).attr('class'))
    //     let show = $(this).prop("checked");
    //     console.log(show);
    //     if ($(this).attr("class") == "allcheck") {
    //       // if (show) {
    //       $("input").prop("checked", show);
    //       // $('.all').children().show(200,'linear')
    //       // } else {
    //       // $("input").prop("checked", show);
    //       // setTimeout(() => {
    //       // $('.all').children().hide()
    //       // }, 100);
    //       // }
    //     } else {
    //       $(this).prop("checked", show);
    //     }
    //     that.select();
    //   });
    // },
    // select() {
    //   let arr = $("input");
    //   // let arr1 = []
    //   let arr1 = Array.from(arr).filter((item, index) => {
    //     return index > 0 && item.checked;
    //   });
    //   let arr2 = arr1.map((item) => {
    //     return item.nextElementSibling.children[0].innerText;
    //   });
    //   console.log(arr, arr1, arr2);
    // },
  },
};
</script>
<style scoped>
* {
  margin: 0;
  padding: 0;
}
.col-3{
  width: 20%;
  float: left;
}
</style>