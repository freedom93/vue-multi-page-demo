<template>
	<div id="head">
		<a v-on:click="goWebPage('rule')" class="ruleBtn"></a>
	 	<a v-on:click="goWebPage('news')" class="newsBtn"></a>
	 	<a v-on:click="goWebPage('list')" class="listBtn"></a>
	</div>
</template>

<script>
export default {
    methods:{
    	goWebPage: function(type){
    		let $head = $('#head a');
    		let $ruleBtn = $('.ruleBtn');
    		let $newsBtn = $('.newsBtn');
    		let $listBtn = $('.listBtn');
    		let url = '';
    		$head.removeClass('active');
    		type == 'rule' && ($ruleBtn.addClass('active'), url = 'rule.html')
    		type == 'news' && ($newsBtn.addClass('active'), url = 'news.html')
    		type == 'list' && ($listBtn.addClass('active'), url = 'list.html')
            window.location.href = url;
        }
    }
}
</script>
<style scoped lang="scss">
@import '../../assets/sass/base/_mixin.scss';
@import '../../assets/sass/head.scss';	
</style>