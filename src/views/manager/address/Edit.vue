<template>
    <briup-fulllayout litle="新增地址">
    {{form}}
    <div>
        <van-cell-group>
            <van-field v-model="form.telephone" placeholder="请输入手机号" />
        </van-cell-group>
        <van-cell-group>
            <van-field v-model="form.province" placeholder="省" />
        </van-cell-group>
        <van-cell-group>
            <van-field v-model="form.city" placeholder="市" />
        </van-cell-group>
        <van-cell-group>
            <van-field v-model="form.area" placeholder="区" />
        </van-cell-group>
        <van-cell-group>
            <van-field v-model="form.address" placeholder="详细地址" />
        </van-cell-group>
    <van-button block type="primary" @click="submitHandler()">保存</van-button>
    </div>
    </briup-fulllayout>
</template>
<script>
import {post} from '../../../http/axios'
import { mapState } from 'vuex';
export default {
    data(){
        return{
            form:{}
        }
    },
    methods:{
        submitHandler(){
            let url ="/address/saveOrUpdate"
            //再提交前将当前登陆者的id作为顾客id
            this.form.customerId=this.info.id;
            post(url,this.form).then((response)=>{
                this.$router.go(-1);
                //轻提示，提示成功消息
                this.$toast.success(response.message)
            })
        }
    },
    computed:{
        ...mapState('user',['info'])
    }
}
</script>