<template>
    <div class="setting">
        <Navbar v-slot:default>
            账户设置
        </Navbar>
        <div class="userInfo-box">
            <ul class="userInfo-list">
                <li>
                    <span>头像</span>
                    <img :src="userinfo.avatar_url">
                    <van-icon name="arrow" />
                </li>
                <li @click="ChangeName">
                    <span>昵称</span>
                    <span class="Info">{{ userinfo.name }}</span>
                    <van-icon name="arrow" />
                </li>
                <li @click="ChangeEmail">
                    <span>邮箱</span>
                    <span class="Info">{{ userinfo.email }}</span>
                    <van-icon name="arrow" />
                </li>
                <li @click="BindPhone">
                    <span>手机号</span>
                    <span class="Info">{{ userinfo.phone }}</span>
                    <van-icon name="arrow" />
                </li>
                <li @click="ChangePassword">
                    <span>修改密码</span>
                    <van-icon name="arrow" />
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import Navbar from "@/components/common/navbar/Navbar";
import {onMounted, reactive, ref, toRefs} from "vue";
import {getUser} from "@/network/user";
import {useRouter} from "vue-router";

export default {
    name: "Setting",
    components:{
        Navbar
    },
    setup(){
        const state = reactive({
            userinfo:{}
        })
        const router = useRouter()
        const ChangeName = () => {
            router.push({path:'/changename'})
        }
        const ChangeEmail = () => {
            router.push({path:'/changeemail'})
        }
        const BindPhone = () => {
            router.push({path:'/bindphone'})
        }
        const ChangePassword = () => {
            router.push({path:'/changepassword'})
        }
        onMounted(()=>{
            getUser().then(res=>{
                state.userinfo = res
                console.log(res)
            })
        })

        return{
            ...toRefs(state),
            ChangeName,
            ChangeEmail,
            BindPhone,
            ChangePassword
        }

    }
}
</script>

<style scoped lang="scss">
    .userInfo-box{
        width: 95%;
        margin: 50px auto auto;
        border-radius: 5px;
        box-shadow: 2px 2px #f9f9f9;
        .userInfo-list{
            text-align: left;
            li{
                border-bottom: 3px solid #f9f9f9;
                padding-left:8px;
                padding-right:5px;
                height: 50px;
                justify-content: space-between;
                padding-top: 18px;
                font-size: 14px;
                img{
                    float: right;
                    width: 45px;
                    height: 45px;
                    margin-top: -17px;
                    //border: 1px solid red;
                }
                .Info{
                    float: right;
                }
                .van-icon-arrow {
                    margin: auto;
                    //float: right;
                    font-weight: bold;
                }


                margin: 20px 0 !important;
                background: #FFFFFF;
                border-radius: 3px;

            }
        }
    }

</style>
