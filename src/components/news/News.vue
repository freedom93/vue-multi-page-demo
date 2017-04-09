<template>
	<div id="news">
        <!-- 轮次榜 -->
        <div class="roundList">
            <div class="list-head"></div>
            <div class="list-body">
                <div class="list-item">
                    <span class="title">第1轮</span>
                    <div class="content">
                        <div>
                            <img class="avator" src="../../assets/images/list/yy.png" onerror="this.src='../../assets/images/list/yy.png'" />
                            <i class="duanwei">暂无段位</i>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- 我的头条 -->

        <!-- 头条擂主 -->

        <!-- 头条段位榜 -->

        <!-- Y阅八卦 -->
	</div>
</template>

<script>
import Vue from 'vue'; 
export default {
    data:function(){
        return {}
     },
     ready:function(){
        let $newsBtn = $('.newsBtn');
        $newsBtn.addClass('active');
     }
}

</script>
<style scoped lang="scss">
@import '../../assets/sass/base/_mixin.scss';
@import '../../assets/sass/rule.scss';
</style>
