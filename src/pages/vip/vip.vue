<template>
  <div>
    <el-button type="primary" @click="willAdd">添加</el-button>
    <v-list :list="list"></v-list>
    <v-form ></v-form>
  </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import vForm from "./components/form.vue"
import vList from "./components/list.vue"
export default {
  components:{
    vList,
    vForm
  },
  data(){
    return {
      info:{
        isshow:false,
        title:"添加会员"
      },
      list:[]
    }
  },
  computed: {
    ...mapGetters({})
  },
  methods: {
    ...mapActions({}),
    willAdd(){
      this.info={
        isshow:true,
        title:"添加会员"
      }
    },
    edit(id){
      this.info={
        isshow:true,
        title:"编辑商品"
      }
      this.$refs.form.getOne(id)
    }
  },
  mounted() {}
};
</script>
<style scoped>
</style>