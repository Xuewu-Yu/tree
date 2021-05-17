<template>
  <div class="home">
      <Tree :list="list" :showCheck="true" />
  </div>
</template>

<script>
import Tree from './Tree'
export default {
  data(){
    return {
      list: [
        {
          name: "root",
          checked: false,
          show:false,
          child: [
            {
              name: "1",
              checked: false,
              show:false,
              child: [
                {
                  name: "1-1",
                  checked: false,
                  show:false,
                  child: [
                    {
                      name: "1-1-1",
                      checked: false,
                      show:false,
                      child: [],
                    },
                  ],
                },
                {
                  name: "1-2",
                  checked: false,
                  show:false,
                  child: [],
                },
              ],
            },
            {
              name: "2",
              checked: false,
              show:false,
              child: [
                {
                  name: "2-1",
                  checked: true,
                  show:false,
                  child: [],
                },
              ],
            },
          ],
        },
      ],
    }
  },
  components:{
    Tree,
  },
  mounted(){
    
  }
}
</script>
