<template>
	<vhead></vhead>
	<vnews></vnews>
	<vfoot></vfoot>
</template>

<script>
import '../../assets/js/lib/viewpoint.js'
import vhead from '../../components/common/Head'
import vfoot from '../../components/common/Foot'
import vnews from '../../components/news/News'
export default {
	components: {
      vhead,
      vfoot,
      vnews
    }
}
</script>
<style lang="scss"> 
@import '../../assets/sass/base/_mobile.scss'; 
</style>

