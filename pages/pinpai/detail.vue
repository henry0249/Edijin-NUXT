<template>
    <div class="pp_detail">
        <Headersub/>
        <div class="banner_pic">
            <img :src="soilPaging.list[10].picture" class="banner_pic">
            <div class="sup">
                <div class="sub">
                    <img :src="FindFinancingDetailed.financingPicture" alt="">
                    <span>{{ FindFinancingDetailed.financingName }}</span>
                    <p><b>简介：</b>{{ FindFinancingDetailed.microProfile }}</p>
                    <button>推荐项目</button>
                </div>
            </div>
        </div>
        <div class="main">
            <div class="con">
                <div class="left">
                    <div class="markdown">
                        <div class="t_h">
                            <i></i>
                            公司介绍
                        </div>
                        <p class="introduce" v-html="FindFinancingDetailed.introduce"></p>
                    </div>
                    <div class="l">
                        <div class="t_h">
                            <i></i>
                            项目需求
                        </div>
                    </div>
                    <!-- <div class="l_item">
                         <button>推荐项目</button>
                         <p>
                             <span>严选</span>
                             <b>山东某企业出资5000万寻金矿企业山东某企业出资5000万寻金山东北</b>
                             <i>2018-03-12</i>
                         </p>
                         <div class="info">
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                         </div>
                    </div>
                    <div class="l_item">
                         <button>推荐项目</button>
                         <p>
                             <span>严选</span>
                             <b>山东某企业出资5000万寻金矿企业山东某企业出资5000万寻金山东北</b>
                             <i>2018-03-12</i>
                         </p>
                         <div class="info">
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                         </div>
                    </div>
                    <div class="l_item">
                         <button>推荐项目</button>
                         <p>
                             <span>严选</span>
                             <b>山东某企业出资5000万寻金矿企业山东某企业出资5000万寻金山东北</b>
                             <i>2018-03-12</i>
                         </p>
                         <div class="info">
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                         </div>
                    </div>
                    <div class="l_item">
                         <button>推荐项目</button>
                         <p>
                             <span>严选</span>
                             <b>山东某企业出资5000万寻金矿企业山东某企业出资5000万寻金山东北</b>
                             <i>2018-03-12</i>
                         </p>
                         <div class="info">
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                             <span>拿地方式：<i>定向摘牌</i></span>
                         </div>
                    </div> -->
                </div>
                <div class="right">
                    <div class="t"><i></i><span>热门投资人</span></div>
                    <div class="l_con">
                        <div v-for="(item,index) in FindancingHot.list">
                            <nuxt-link :to="{path:'/pinpai/detail',query:{id:item.id}}">
                                <img :src="item.financingPicture" alt="">
                                <p>
                                    <i>{{ item.financingName }}</i><br>
                                    <b>{{ item.microProfile }}</b>
                                </p>
                            </nuxt-link>
                            <!-- <p>{{ item.microProfile }}</p> -->
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <Footer/>
    </div>
</template>

<script>
import Headersub from '~/components/headersub.vue';
import Footer from '~/components/footer.vue';
import P from '../../api/pinpai'
export default {
    watchQuery: true,
    data(){
        return {

        }
    },
    components:{
        Headersub,
        Footer
    },
    async asyncData(context){
            // console.log('大咖')
            let [
                soilPaging,
                FindFinancingDetailed,
                FindancingHot,
            ]
            = await Promise.all([
                P.soilPaging(),
                P.FindFinancingDetailed({'id':context.route.query.id+''}),
                P.FindancingHot(),
            ])
            return {
                soilPaging: soilPaging.data,
                FindFinancingDetailed: FindFinancingDetailed.data,
                FindancingHot: FindancingHot.data,
            }

    },
    beforeRouteUpdate (to, from, next) {
		document.body.scrollTop = 0
        document.documentElement.scrollTop = 0
		next()
  	},
}
</script>

<style>
.banner_pic{
    width: 100%;
    height: 350px;
    position: relative;
}
div.banner_pic div.sup{
    width: 1200px;
    height: 100%;
    position: absolute;
    top:0;
    left:50%;
    margin-left: -600px;
}
div.banner_pic div.sup div.sub{
    width: 360px;
    height: 100%;
    background-color:rgba(255, 255, 255, 0.8);
    float: left;
    text-align: center;
}
div.banner_pic div.sup div.sub img{
    width: 90px;
    height: 90px;
    display: inline-block;
    border-radius: 50%;
    margin-top: 47px;
}
div.banner_pic div.sup div.sub span{
    display: block;
    margin-top: 32px;
    font-size: 18px;
    color:#333;
    margin-bottom: 20px;
}
div.banner_pic div.sup div.sub p{
    width: 280px;
    margin-left: 60px;
    text-align: justify;
    position: relative;
    color: #666;

}
div.banner_pic div.sup div.sub p b{
    position:absolute;
    left: -50px;
    top: 0;
}
div.banner_pic div.sup div.sub button{
    width: 100px;
    height: 34px;
    text-align: center;
    line-height: 34px;
    color: #fff;
    border: none;
    outline: 0;
    border-radius: 6px;
    background-color: #dd514c;
    margin-top: 30px;
}
p.introduce{
    padding: 0!important;
    padding-left: 15px!important;
    width: 730px;
    text-align: justify;
    line-height: 22px;
}
p.introduce img{
    max-width: 700px!important;
}
div.l_con{
    height: auto!important;
}
div.l_con div p b{
    font-size: 14px;
    color: #999;
    line-height: 20px;
    height: 40px;
    overflow: hidden;
    display: inline-block;
}
div.l_con div p{
    margin-left: 14px;
}
div.l_con div{
    padding-bottom: 20px;
}
</style>

