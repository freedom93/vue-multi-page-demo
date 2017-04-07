<template>
	<div id="rule">
        <div v-for="(index, item) in imgList" class="rule-item">
            <div class="img9Wrap" v-if="(index == 8)">
                <img src="../../assets/images/transparent.gif" v-lazyload:opt.fadein="item.img" class="{{item.class}} lazy" />
            </div>
            <img  v-else src="../../assets/images/transparent.gif"  v-lazyload:opt.fadein="item.img" class="{{item.class}} lazy" />
            <div  v-if="(index == 1 || index == 3 || index == 5 || index == 6 || index == 8 || index == 9)" class="yellowBlank"></div>
        </div>
	</div>
</template>

<script>
import Vue from 'vue'; 
import "vue-lazyload-img";
import img1 from '../../assets/images/rule-img1.jpg';
import img2 from '../../assets/images/rule-img2.jpg';
import img3 from '../../assets/images/rule-img3.jpg';
import img4 from '../../assets/images/rule-img4.jpg';
import img5 from '../../assets/images/rule-img5.jpg';
import img6 from '../../assets/images/rule-img6.jpg';
import img7 from '../../assets/images/rule-img7.jpg';
import img8 from '../../assets/images/rule-img8.jpg';
import img9 from '../../assets/images/rule-img9.jpg';
import img10 from '../../assets/images/rule-img10.jpg';
import img11 from '../../assets/images/rule-img11.jpg';
import img12 from '../../assets/images/rule-img12.jpg';
import img13 from '../../assets/images/rule-img13.jpg'
import img14 from '../../assets/images/rule-img14.jpg';
import img15 from '../../assets/images/rule-img15.jpg';

Vue.use(Vue.lazyimg,{
    fade: true,
    nohori: true,
    speed: 20,   
});
export default {
    data:function(){
        var imgs = [img1, img2, img3, img4, img5, img6, img7, img8, img9, img10, img11, img12, img13, img14, img15];
        var imgList = [];
        for(let i = 0; i < 15; i++){
            imgList[i] = {};
            imgList[i].img = imgs[i];
            imgList[i].class = 'img'+(i+1);
        }
        return {imgList: imgList}
     },         
     ready:function(){
        let $ruleBtn = $('.ruleBtn');
        $ruleBtn.addClass('active');        
     }    
}

</script>
<style scoped lang="scss">
@import '../../assets/sass/base/_mixin.scss';
@import '../../assets/sass/rule.scss';	
</style>
