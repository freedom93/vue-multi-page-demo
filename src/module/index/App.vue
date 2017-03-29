<template>
	<vhead></vhead>
	<vindex></vindex>
	<vfoot></vfoot>
</template>

<script>
import '../../assets/js/lib/viewpoint.js'
import vhead from '../../components/common/Head'
import vfoot from '../../components/common/Foot'
import vindex from '../../components/index/Index'
export default {
	components: {
      vhead,
      vfoot,
      vindex
    }
}
</script>
<style lang="scss"> 
@import '../../assets/sass/base/_mobile.scss'; 
</style>

