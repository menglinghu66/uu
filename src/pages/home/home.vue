<template>
  <div>
    <div class="box" id="main"></div>
  </div>
</template>
<script>
import { mapGetters, mapActions } from "vuex";
import echarts from "echarts";
export default {
  computed: {
    ...mapGetters({
      list: "cate/list"
    })
  },
  methods: {
    ...mapActions({
      reqList: "cate/reqList"
    })
  },
  watch: {
    list: {
      handler() {
        if (this.list.length > 0) {
          //制图表
          let myChart = echarts.init(document.getElementById("main"));
          // 图表的配置项和数据
          var option = {
            title: {
              text: "数量"
            },
            tooltip: {},
            legend: {
              data: ["子分类数量"]
            },
            xAxis: {
              data: this.list.map(item=>item.catename),
            },
            yAxis: {
               type: 'value'
            },
            //series数据
            series: [
              {
                name: "子分类数量",
                type: "line",
                data:this.list.map(item=>item.children?item.children.length:0)
              },
            ]
          };

          myChart.setOption(option);
        }
      },
      deep: true
    }
  },
  mounted() {
    this.reqList();
  }
};
</script>
<style scoped>
.box {
  width: 80%;
  margin: 20px auto;
  height: 500px;
}
</style>