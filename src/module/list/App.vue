<template>
	<vhead></vhead>
	<vlist></vlist>
	<vfoot></vfoot>
</template>

<script>
import '../../assets/js/lib/viewpoint.js'
import vhead from '../../components/common/Head'
import vfoot from '../../components/common/Foot'
import vlist from '../../components/list/List'
export default {
	components: {
      vhead,
      vfoot,
      vlist
    }
}
</script>
<style lang="scss"> 
@import '../../assets/sass/base/_mobile.scss'; 
</style>

