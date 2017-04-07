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
    		type == 'rule' && ($ruleBtn.hasClass('active') ? url = '' : url = 'rule.html', $ruleBtn.addClass('active'))
    		type == 'news' && ($newsBtn.hasClass('active') ? url = '' : url = 'news.html', $newsBtn.addClass('active'))
    		type == 'list' && ($listBtn.hasClass('active') ? url = '' : url = 'list.html', $listBtn.addClass('active'))
            url !== '' && (window.location.href = url)
        }
    }
}
</script>
<style scoped lang="scss">
@import '../../assets/sass/base/_mixin.scss';
@import '../../assets/sass/head.scss';	
</style>