<template>
	<div id="list">
        <h2>实时榜单</h2>
	</div>
</template>

<script>
import Vue from 'vue'; 
export default {
    data:function(){
        
        return {}
     },         
     ready:function(){
        let $listBtn = $('.listBtn');
        $listBtn.addClass('active');        
     }    
}

</script>
<style scoped lang="scss">
@import '../../assets/sass/base/_mixin.scss';
@import '../../assets/sass/rule.scss';	
</style>
