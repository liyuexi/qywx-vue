<template>
<div class="page">
    <div class="page__hd">
        <h1 class="page__title">授权登录回调</h1>
        <p class="page__desc">授权登录回调获取code,通过code获取用户信息,可获取信息后自动跳转</p>
        <p class="page__desc">当前url: {{ url}}</p>
    </div>
    <div class="page__bd page__bd_spacing">
       
        <div class="weui-flex">
            <div class="weui-flex__item">
              <div class="placeholder">
                <a href="javascript:" class="weui-btn weui-btn_mini weui-btn_primary" @click="getOauthUser">通过code获取用户</a>
             </div>
            </div>
             <div class="weui-flex__item">
              <div class="placeholder">
                <a href="javascript:" >文档</a>
             </div>
            </div>
        </div>
       
    </div>
</div>
 </template>

 <script>
import { mapGetters, mapActions } from 'vuex'
import { oauthAdminUser } from '../api/user'
import { queryString } from '../utils/index'

export default {
  name: 'AdminCallback',
  created() {
    
  },
  computed: {
    ...mapGetters([
    'userToken',
    ]),
    url(){
      return window.location.href
    }
  },
   methods: {
     ...mapActions([
      'saveUser', 
     ]),
     getOauthUser(){
       
       let params = {'code': this.$route.query.code}
        oauthAdminUser(params).then((res)=>{
          console.log(res)
          //进行存储
            this.saveUser(res.data)
            alert(  JSON.stringify(res)  )
            this.$router.push("/user");
          // window.lorcation.href = res.data.oauth_url
        });
     }
   },
}
</script>