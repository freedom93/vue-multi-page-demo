<template>
	<div id="news">
        <!-- 轮次榜 -->
        <div class="roundList">
            <div class="list-head"></div>
            <div class="list-body">
                <div class="list-item" v-for="(index, item) in roundList">
                    <span class="title">第{{index + 1}}轮</span>
                    <div class="content">
                        <div class="champion">
                            <img class="avator" src="//s1.yy.com/guild/header/10001.jpg" onerror="this.src='//s1.yy.com/guild/header/10001.jpg'" />
                            <i class="duanwei">暂无段位</i>
                        </div>
                        <table>
                            <tr v-for="(index2, item2) in anchorList">
                                <td>
                                    <p><span class="nick">虚位以待虚位以待虚位以待虚位以待虚位以待</span><i class="name">头条</i></p>
                                    <span class="value">闪耀值：<em>798</em></span>
                                    <i class="stars"></i>
                                </td>
                                <td>
                                    <i class="people"></i>
                                </td>
                            </tr>
                        </table>
                        <table>
                            <tr>
                                <td>
                                    <img class="avator" src="//s1.yy.com/guild/header/10001.jpg" onerror="this.src='//s1.yy.com/guild/header/10001.jpg'" />
                                </td>
                                <td>
                                    <span class="nickname">虚位以待</span>
                                    <span class="value">影响力：<em>798</em></span>
                                </td>
                            </tr>
                        </table>
                    </div>
                </div>
            </div>
            <a class="load-more" href="javascript:void(0);" v-on:click="loadMore"></a>
        </div>
        <!-- <div class="yellowBlank"></div> -->
        <!-- 我的头条 -->
        <!-- <div class="yellowBlank"></div> -->
        <!-- 头条擂主 -->
        <!-- <div class="yellowBlank"></div> -->
        <!-- 头条段位榜 -->
        <!-- <div class="yellowBlank"></div> -->
        <!-- Y阅八卦 -->
	</div>
</template>

<script>
import Vue from 'vue';
export default {
    data:function(){
        let dataList = {};
        let anchorList = [];
        let roundList = [];
        for(let j = 0; j < 4; j++){
            j < 3 && (anchorList[j] = {});
            roundList[j] = {};
        }
        dataList.anchorList = anchorList;
        dataList.roundList = roundList;
        return dataList
    },
    methods: {
        loadMore: function(){
            let that = this;
            let anchorList = that._data.anchorList;
            let roundList = that._data.roundList;
            for(let j = 4; j < 24; j++){
                j < 3 && (anchorList[j] = {});
                roundList[j] = {};
            }
            this._data.anchorList = anchorList;
            this._data.roundList = roundList;
        }
    },
    ready:function(){
        let $newsBtn = $('.newsBtn');
        $newsBtn.addClass('active');
    }
}

</script>
<style scoped lang="scss">
@import '../../assets/sass/base/_mixin.scss';
@import '../../assets/sass/news.scss';
</style>
