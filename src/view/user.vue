<template>
    <transition name='fade'>
        <div id="user">
            <div class="user-container" :style="{backgroundImage:avatarUrl}" @dblclick.prevent.self="changeBg()">
                <div class="user-info">
                    <ul>
                        <li>
                            <i class='sm margin iconfont icon-nickname margin'></i>
                            <span>昵称</span>
                            <input type="text" spellcheck="false" v-model="user.nickname" :placeholder="nickname"/>
                        </li>
                        <li>
                            <i class='sm margin iconfont icon-sign margin'></i>
                            <span>签名</span>
                            <input type="text" spellcheck="false" v-model="user.sign" :placeholder="sign"/>
                        </li>
                    </ul>
                    <button class="save" type='button' @click="sumbit()">保存</button>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        name: 'user',
        data() {
            return {
                change:false,
                user:{
                    avatar:'zhenji',
                    nickname:'',
                    sign:'',
                }
            }
        },
        components: {
        },
        computed: {
            nickname(){
                return this.$storage.get('nickname');
            },
            sign(){
                return this.$storage.get('sign');
            },
            avatar(){
                return this.$storage.get('avatar');
            },
            avatarUrl(){
                if(this.avatar&&!this.change) return 'url(./img/player/'+this.avatar+'.png)';
                else return 'url(./img/player/'+this.user.avatar+'.png)';
            }
        },
        methods: {
            changeBg(){
                var list=['zhenji','lingju','xiahoushi'];
                var item=list.findNext(this.user.avatar);
                this.change=true;
                this.$set(this.user,'avatar',item);
            },
            sumbit(){
                this.$storage.set(['nickname','sign','avatar'],[this.user.nickname,this.user.sign,this.user.avatar]);
                this.$router.replace('gallery');
            }
        }
    }
</script>

<style lang="scss" scoped>
    #user{
        width: 100%;
        height: 100%;
        position: relative;
        .user-container{
            @include cc(4.2rem,6rem);
            border-radius: .3rem;
            background-size: cover;
            box-shadow:.04rem .08rem .3rem .02rem rgba(0,0,0,.4),
             0 0 4rem .5rem black inset;
            border:.1rem solid $border;
            transition: all .75s;
            .user-info{
                position: absolute;
                bottom: 0;
                // width: 100%;
                // background: rgba(0,0,0,0.5);
                @include rect-m(100%,auto);
                // border: none
                ul{
                    margin: 0 0 .8rem 0;
                    li {
                        height: .8rem;
                        // color: rgba(255,255,255,0.8);
                        font-size: .36rem;
                        line-height: .8rem;
                        transition: all 0.3s ease-out;
                        transform: translateX(0);
                        // background:$darkHover;
                        input{
                            // outline: none;
                            // width:2.5rem;
                            width: 60%;
                            float: right;
                            // color: rgba(255,255,255,0.8);
                        }
                    }
                }
                .save{
                    position: absolute;
                    width: 100%;
                    bottom: 0;
                }
            }
        }
        
    }
</style>