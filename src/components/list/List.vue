<template>
	<!-- 实时榜 -->
    <div id="list-anchor">
        <i class="title"></i>
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
                        <img class="avator" src="../../assets/images/list/yy.png" onerror="this.src='../../assets/images/list/yy.png'" />
                        <span class="duanwei">铂金段位</span> 
                    </td>
                    <td>
                        <span class="nickname">{{item.nickname}}</span>
                        <span class="value">星星数：<em>{{item.stars}}</em></h5>
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
export default {
    data:function(){
        let tiantiList = [];
        for(let i = 0; i < 10; i++){
            tiantiList[i] = {};
            tiantiList[i].rank = (i+1);
            tiantiList[i].duanwei = (i+1);
            tiantiList[i].nickname = (i % 2 == 0 ? ('头条头条头条头条头条头条'+i) : (('头条头条头条头条头条头条头条头条头条头条头条头条'+i)));
            tiantiList[i].avator = '../../assets/images/list/yy.png';
            tiantiList[i].stars = (i * 2);
            tiantiList[i].live = (i % 2 == 0 ? 1 : 0);
        }
        return {tiantiList: tiantiList}
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
