<template>
	<!-- 头条榜 -->
    <div id="list-headline">
        <i class="title"></i>
        <div class="listWrap">
            <!-- 主播榜 -->
            <table class="list-anchor">
                <tr v-for="(index, item) in headlineList">
                    <td><span class="rank{{index < 3 ? (' rank'+(index+1)) : ''}}">{{index > 2 ? (index + 1) : ''}}</span></td>
                    <td>
                        <img class="avator" v-bind:src=item.avator onerror="this.src='//s1.yy.com/guild/header/10001.jpg'" />
                        <i class="duanwei">{{item.duanwei | formatDuanwei}}</i>
                    </td>
                    <td>
                        <span class="tip">主播呢称</span>
                        <span class="nick">{{item.nick}}</span>
                        <span class="tip">闪耀值</span>
                        <span class="value">{{item.value | formatNumber}}</span>
                    </td>
                    <td>
                        <i class="broadcast{{item.live == 1 ? ' live' : ''}}"></i>
                    </td>
                </tr>
            </table>
            <!-- 壕友榜 -->
            <table class="list-user">
                <tr v-for="(index, item) in userList">
                    <td>
                        <span class="tip">壕友呢称</span>
                        <span class="nick">{{item.nick}}</span>
                        <span class="tip">影响力</span>
                        <span class="value">{{item.value | formatNumber}}</span>
                    </td>
                </tr>
            </table>
        </div>
    </div>
    <div class="yellowBlank"></div>
    <!-- 天梯榜 -->
    <div id="list-tianti">
        <i class="title"></i>
        <div class="listWrap">
            <table>
                <tr v-for="(index, item) in tiantiList">
                    <td><span class="rank{{index < 3 ? (' rank'+(index+1)) : ''}}">{{index > 2 ? (index + 1) : ''}}</span></td>
                    <td>
                        <img class="avator" v-bind:src=item.avator onerror="this.src='//s1.yy.com/guild/header/10001.jpg'" />
                        <i class="duanwei">{{item.duanwei | formatDuanwei}}</i>
                    </td>
                    <td>
                        <span class="nickname">{{item.nickname}}</span>
                        <span class="value">星星数：<em>{{item.stars}}</em></span>
                    </td>
                    <td>
                        <i class="broadcast{{item.live == 1 ? ' live' : ''}}"></i>
                    </td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>
import Vue from 'vue';
Vue.filter('formatDuanwei', function (type) {
    let duanwei = '';
    switch(Number(type)){
        case 1: duanwei = '青铜段位'; break;
        case 2: duanwei = '白银段位'; break;
        case 3: duanwei = '黄金段位'; break;
        case 4: duanwei = '铂金段位'; break;
        case 5: duanwei = '钻石段位'; break;
        case 6: duanwei = '王者段位'; break;
        default: duanwei = '暂无段位'; break;
    }
    return duanwei;
})
Vue.filter('formatNumber', function (num) {
    if (!num) {
        return "0";
    }
    var num1 = parseInt(num/10000);
    return num >= 100000000 ? (num1.toString().replace(/(?=(?!^)(\d{3})+$)/g, ',')+'万') : (num.toString().replace(/(?=(?!^)(\d{3})+$)/g, ','));

})
export default {
    data:function(){
        let tiantiList = [];
        let headlineList = [];
        let userList = [];
        for(let i = 0; i < 10; i++){
            headlineList[i] = {};
            headlineList[i].rank = (i+1);
            headlineList[i].duanwei = (i > 6 ? (i - 6) : i);
            headlineList[i].nick = (i % 2 == 0 ? ('头条头条头条头条头条头条'+i) : (('头条头条头头条头条头条头条头条头条头条头条'+i)));
            headlineList[i].avator = '//s1.yy.com/guild/header/10001.jpg';
            headlineList[i].live = (i % 2 == 1 ? 1 : 0);
            headlineList[i].value = 64369991 * (10 - i);

            userList[i] = {};
            userList[i].value = 12345 * (10 - i);
            userList[i].nick = (i % 2 == 0 ? ('头条头条头条头条头条头条'+i) : (('头条头条头条头条头条头条头条头条头条头条头条'+i)));

            tiantiList[i] = {};
            tiantiList[i].rank = (i+1);
            tiantiList[i].duanwei = (i > 6 ? (i - 6) : i);
            tiantiList[i].nickname = (i % 2 == 0 ? ('头条头条头条头条头条头条'+i) : (('头条头条头条头条头条头条头条头条头条头条'+i)));
            tiantiList[i].avator = '//act.m.yystatic.com/act/images/default_grey_yy.png';
            tiantiList[i].stars = (i * 2);
            tiantiList[i].live = (i % 2 == 0 ? 1 : 0);
        }
        return {
            headlineList: headlineList,
            userList: userList,
            tiantiList: tiantiList
        }
     },
     ready:function(){
        let $listBtn = $('.listBtn');
        $listBtn.addClass('active');
     }
}

</script>
<style scoped lang="scss">
@import '../../assets/sass/base/_mixin.scss';
@import '../../assets/sass/list.scss';
</style>
