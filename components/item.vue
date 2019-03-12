<template lang=pug>
  .row.center.content
    .content-item.col-6 {{prop}}
</template>

<script>
	export default {
		name: 'item',
		props: ['prop']
	}
</script>

<style lang=sass>
	.row
		justify-content: center
</style>

