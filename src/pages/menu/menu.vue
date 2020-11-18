<template>
  <div>
    <!-- 添加按钮 -->
    <el-button type="primary" @click="willAdd">添加</el-button>

    <!-- table -->
    <!-- 将list传递给list.vue 组件 -->
    <!-- 绑定自定义事件init -->
    <!-- 绑定自定义事件edit -->
    <v-list :list="list" @init="init" @edit="edit($event)"></v-list>

    <!-- 弹框 -->
    <!-- 将info传递给form  -->
    <!-- 将list传递给form  -->
    <!-- 绑定自定义事件init -->
    <v-form :info="info" :list="list" @init="init" ref="form"></v-form>
  </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import vList from "./components/list.vue";
import vForm from "./components/form.vue";
import { reqMenuList } from "../../utils/http";
export default {
  data() {
    return {
      info: {
        isshow: false,
        title: "添加菜单",
      },
      //列表数据
      list: [],
    };
  },
  computed: {
    ...mapGetters({}),
  },
  methods: {
    ...mapActions({}),
    willAdd() {
      this.info.isshow = true;
      this.info.title = "添加菜单";
    },
    init() {
      reqMenuList().then((res) => {
        this.list = res.data.list;
      });
    },
    //处理编辑
    edit(id) {
      this.info.isshow = true;
      //给info补了一个字段，用来判断是添加还是编辑打开的弹框
      this.info.title = "编辑菜单";
      //父组件调用子组件 form.vue 的getOne()
      this.$refs.form.getOne(id);
    },
  },
  mounted() {
    //一进来就要请求数据
    this.init();
  },
  components: {
    vList,
    vForm,
  },
};
</script>
<style scoped>
</style>