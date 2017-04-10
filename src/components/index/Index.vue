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
                        <img class="avator" v-bind:src="item.headurl" onerror="this.src='//act.m.yystatic.com/act/images/default_grey_yy.png'" />
                        <i class="duanwei">{{item.duanwei | formatDuanwei}}</i>
                    </td>
                    <td>
                        <span class="tip">主播呢称</span>
                        <span class="nick">{{item.nick | decode}}</span>
                        <span class="tip">闪耀值</span>
                        <span class="value">{{item.ticket | formatNumber}}</span>
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
                        <span class="nick">{{item.nick | decode}}</span>
                        <span class="tip">影响力</span>
                        <span class="value">{{item.power | formatNumber}}</span>
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
                        <img class="avator" v-bind:src="item.headurl" onerror="this.src='//act.m.yystatic.com/act/images/default_grey_yy.png'" />
                        <i class="duanwei">{{item.duanwei | formatDuanwei}}</i>
                    </td>
                    <td>
                        <span class="nickname">{{item.nick | decode}}</span>
                        <span class="value">星星数：<em>{{item.ticket | formatNumber}}</em></span>
                    </td>
                    <td>
                        <i class="broadcast{{item.islive == 1 ? ' live' : ''}}"></i>
                    </td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>
import Vue from 'vue';
import VueResouse from 'vue-resource';
Vue.use(VueResouse);
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
Vue.filter('formatNumber',function(num){
    if(!num){
        return "0";
    }
    return num.toString().replace(/(?=(?!^)(\d{3})+$)/g, ',');
})
Vue.filter('decode',function(value){
	var value = _html(value);
	return String(value).replace(/&#(\d+);/g, function(match, dec) {
		return String.fromCharCode(dec);
	});

	function _html(str){
	  var tep = document.createElement('div');
	  tep.innerHTML = str;
	  str = tep.innerText || tep.textContent;
	  tep = null;
	  return str;
	}
})
export default {
    data:function(){
        let tiantiList = [];
        let headlineList = [];
        let userList = [];
        /*
	        for(let i = 0; i < 10; i++){
	            headlineList[i] = {};
	            headlineList[i].rank = (i+1);
	            headlineList[i].duanwei = (i > 6 ? (i - 6) : i);
	            headlineList[i].nick = (i % 2 == 0 ? ('头条头条头条头条头条头条'+i) : (('头条头条头头条头条头条头条头条头条头条头条'+i)));
	            headlineList[i].avator = '../../assets/images/list/yy.png';
	            headlineList[i].live = (i % 2 == 1 ? 1 : 0);
	            headlineList[i].value = ( i % 2 == 1 ? 1000 * i : 200 * i);

	            userList[i] = {};
	            userList[i].value = (i+1);
	            userList[i].nick = (i % 2 == 0 ? ('头条头条头条头条头条头条'+i) : (('头条头条头条头条头条头条头条头条头条头条头条'+i)));

	            tiantiList[i] = {};
	            tiantiList[i].rank = (i+1);
	            tiantiList[i].duanwei = (i > 6 ? (i - 6) : i);
	            tiantiList[i].nickname = (i % 2 == 0 ? ('头条头条头条头条头条头条'+i) : (('头条头条头条头条头条头条头条头条头条头条'+i)));
	            tiantiList[i].avator = '../../assets/images/list/yy.png';
	            tiantiList[i].stars = (i * 2);
	            tiantiList[i].live = (i % 2 == 0 ? 1 : 0);
	        }
        */
        return {
            headlineList: headlineList,
            userList: userList,
            tiantiList: tiantiList
        }
     },
     methods: {
     	//头条梯
        toutiaoRender:function(){
            let she = this;
            she.$nextTick(function () {
            	let url = '//act1.m.yystatic.com/act/file/headline2017/headlineHour.txt';
		        let options = {
		            jsonp: 'callback',
		            jsonpCallback: 'headlineHour'
		        }
		        this.$http.jsonp(url, options).then(function(resp){
		        	let data = resp.data.listInfo.topchid;
		        	let len = data.length;
		        	// 不足10条
	        		for(let i = 1;  len <= 10 && i < (11 - len); i++){
	        			let obj = {};
	        			obj.rank = len + i;
	        			obj.nick = '虚位以待';
	        			obj.ticket = 0;
	        			obj.headurl = '//act.m.yystatic.com/act/images/default_grey_yy.png';
	        			data.push(obj)
	        		}
	        		// 超过10条
	        		let data2 = [];
        			for(let i = 0; len > 10 && i < 10; i++){
        				data2.push(data[i])
        			}
		        	she.headlineList = len > 10 ? data2 : data;
		        }, function(error) {
		            console.log('主播头条榜请求出错', error)
		            let data = [];
		            for(let i = 1;  i <= 10; i++){
	        			let obj = {};
	        			obj.rank = i;
	        			obj.nick = '虚位以待';
	        			obj.ticket = 0;
	        			obj.headurl = '//act.m.yystatic.com/act/images/default_grey_yy.png';
	        			data.push(obj)
	        		}
		        	she.headlineList = data;
		        });
		    })                    
        },
        //壕友梯
        haoyouRender:function(){
            let she = this;
            she.$nextTick(function () {
            	let url = '//act1.m.yystatic.com/act/file/headline2017/friend.txt';
		        let options = {
		            jsonp: 'callback',
		            jsonpCallback: 'friend'
		        }
		        this.$http.jsonp(url, options).then(function(resp){
		        	let data = resp.data.listInfo.topchid;
		        	let len = data.length;
		        	// 不足10条
	        		for(let i = 1;  len <= 10 && i < (11 - len); i++){
	        			let obj = {};
	        			obj.rank = len + i;
	        			obj.nick = '虚位以待';
	        			obj.power = 0;
	        			obj.headurl = '//act.m.yystatic.com/act/images/default_grey_yy.png';
	        			data.push(obj)
	        		}
	        		// 超过10条
	        		let data2 = [];
        			for(let i = 0; len > 10 && i < 10; i++){
        				data2.push(data[i])
        			}
		        	she.userList = len > 10 ? data2 : data;
		        }, function(error) {
		            console.log('壕友榜请求出错', error)
		            let data = [];
		            for(let i = 1;  i <= 10; i++){
	        			let obj = {};
	        			obj.rank = i;
	        			obj.nick = '虚位以待';
	        			obj.power = 0;
	        			obj.headurl = '//act.m.yystatic.com/act/images/default_grey_yy.png';
	        			data.push(obj)
	        		}
		        	she.userList = data;
		        });
		    })                    
        },
     	//天梯榜
        tiantiRender:function(){
            let she = this;
            she.$nextTick(function () {
            	let url = '//act1.m.yystatic.com/act/file/headline2017/star.txt';
		        let options = {
		            jsonp: 'callback',
		            jsonpCallback: 'star'
		        }
		        this.$http.jsonp(url, options).then(function(resp){
		        	let data = resp.data.listInfo.topchid;
		        	let len = data.length;
		        	// 不足10条
	        		for(let i = 1;  len <= 10 && i < (11 - len); i++){
	        			let obj = {};
	        			obj.rank = len + i;
	        			obj.nick = '虚位以待';
	        			obj.ticket = 0;
	        			obj.headurl = '//act.m.yystatic.com/act/images/default_grey_yy.png';
	        			data.push(obj)
	        		}
	        		// 超过10条
	        		let data2 = [];
        			for(let i = 0; len > 10 && i < 10; i++){
        				data2.push(data[i])
        			}
		        	she.tiantiList = len > 10 ? data2 : data;
		        }, function(error) {
		            console.log('天梯榜请求出错', error)
		            let data = [];
		            for(let i = 1;  i <= 10; i++){
	        			let obj = {};
	        			obj.rank = i;
	        			obj.nick = '虚位以待';
	        			obj.ticket = 0;
	        			obj.headurl = '//act.m.yystatic.com/act/images/default_grey_yy.png';
	        			data.push(obj)
	        		}
		        	she.tiantiList = data;
		        });
		    })                    
        }
     },
     ready:function(){
        let $listBtn = $('.listBtn');
        $listBtn.addClass('active');
        this.tiantiRender();
        this.haoyouRender();
        this.toutiaoRender();
     }
}

</script>
<style scoped lang="scss">
@import '../../assets/sass/base/_mixin.scss';
@import '../../assets/sass/index.scss';	
</style>
