<template>
    <div class="page">
       <p class="text-primary">我是页面二</p>
       <div>
           <p class="text-warning" v-for="(user , index) in users" :key="index">
               {{user.name}} 
               -- 
               <button type="button" class="btn btn-info" @click = "detailPush(user.id)" title="可以返回到当前页面">查看详情【push】</button>
               -- 
               <button type="button" class="btn btn-warning"  @click = "detailReplace(user.id)" title="replace不可返回到当前页面">查看详情【replace】</button>
            </p>
       </div>
       <button type="button" class="btn btn-success" @click="goBack">返回</button>
       <p></p>
       <!-- 用来显示当前路由组件页面（详情） -->
       <router-view></router-view>
    </div>
</template>
<script>
export default {
    props:['name','age'],
    data(){
        return{
            users:[]
        }
    },
    mounted(){
        // 模拟数据来自后台
        setTimeout(()=>{
            this.users = [
                {id:1,name:'哈哈'},
                {id:2,name:'滴滴'},
                {id:3,name:'库库'},
            ]
        },100)
        console.log('在路由中，如果 props 被设置为 true，this.$route.params 将会被设置为组件属性',this.name)
        // console.log('在路由中，如果 props 被设置为 true，this.$route.params 将会被设置为组件属性',this.age)
    },
    methods:{
        // 编程式路由导航
        detailPush(id){
            //console.log(this.$router)
           // console.log(this.$route)
            // this.$router.push(`/routerApp/page2/${this.name}/details/${id}`) // 路径需完整，不然会报错
            // 命名路由方式跳转
            this.$router.push({
                name:'details',
                params:{
                    id
                },
                query:{
                    q:'query参数'
                }
            })

        },
        detailReplace(id){
             this.$router.replace(`/routerApp/page2/${this.name}/details/${id}`)
        },
        goBack(){
            // this.$router.back();
            this.$router.go(-1)
        }
    }
}
</script>
<style>

</style>