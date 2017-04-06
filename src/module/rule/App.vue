<template>
	<vhead></vhead>
	<vrule></vrule>
	<vfoot></vfoot>
</template>

<script>
import '../../assets/js/lib/viewpoint.js'
import vhead from '../../components/common/Head'
import vfoot from '../../components/common/Foot'
import vrule from '../../components/rule/Rule'
export default {
	components: {
      vhead,
      vfoot,
      vrule
    }
}
</script>
<style lang="scss"> 
@import '../../assets/sass/base/_mobile.scss'; 
</style>

