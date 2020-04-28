<template>
  <div>
    <div style="margin:0px 0px 20px 0px;width: 20%;padding: 0px 40%;">
      <el-autocomplete
        class="inline-input"
        v-model="state1"
        :fetch-suggestions="querySearch"
        placeholder="请输入账号"
        @select="handleSelect"
      ></el-autocomplete>
    </div>
    <div style="margin:0px 0px 20px 0px;width: 20%;padding: 0px 40%;">
      <el-input placeholder="请输入密码" v-model="input" show-password></el-input>
    </div>
    <div style="display:flex;padding: 0px 40%;">
      <el-button type="primary" disabled>登录</el-button>
       <el-button type="primary" disabled>注册</el-button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      restaurants: [],
      state1: "",
      input: ""
    };
  },
  methods: {
    querySearch(queryString, cb) {
      var restaurants = this.restaurants;
      var results = queryString
        ? restaurants.filter(this.createFilter(queryString))
        : restaurants;
      // 调用 callback 返回建议列表的数据
      cb(results);
    },
    createFilter(queryString) {
      return restaurant => {
        return (
          restaurant.value.toLowerCase().indexOf(queryString.toLowerCase()) ===
          0
        );
      };
    },
    loadAll() {
      return [
        { value: "陈佳人", address: "长宁区新渔路144号" },
        {
          value: "柳基基",
          address: "上海市长宁区淞虹路661号"
        },
        {
          value: "死gaiba",
          address: "上海市普陀区真北路988号创邑金沙谷6号楼113"
        }
      ];
    },
    handleSelect(item) {
      console.log(item);
    }
  },
  mounted() {
    this.restaurants = this.loadAll();
  }
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
