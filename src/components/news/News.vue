<template>
	<div id="news">
        <h2>新闻</h2>
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
