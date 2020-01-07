<template>
  <briup-fulllayout title="常用地址">
    <van-list>
      <van-cell
        v-for="item in addresses"
        :key="item.id"
        :title="item.province+''+item.city+''+item.area+''+item.address"
      />
    </van-list>
    <van-button block type="default" @click="toAddressEditHandle">添加</van-button>
    <van-button block type="default" @click="toAddressAlterHandle">修改</van-button>
  </briup-fulllayout>
</template>
<script>
import { get } from "../../../http/axios";
import { mapState } from "vuex";
export default {
  data() {
    return {
      addresses: []
    };
  },
  computed: {
    //计算属性
    //将状态机中的user对象中的info对象获取到
    ...mapState("user", ["info"])
  },
  created() {
    this.loadAddress();
  },
  methods: {
    loadAddress() {
      let id = this.info.id;
      let url = "/address/findByCustomerId?id=" + id;
      get(url).then(response => {
        this.addresses = response.data;
      });
    },
    //跳转到地址编辑页面的处理函数
    toAddressEditHandle() {
      //编程跳转
      this.$router.push("/manager/address_edit");
    },
    toAddressAlterHandle() {
      this.$router.push("/manager/address_alter");
    }
  }
};
</script>