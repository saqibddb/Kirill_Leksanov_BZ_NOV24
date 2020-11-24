<template>
	<Home />
</template>

<script>
import Home from '@/views/Home';

export default {
  name: 'App',
  components: {
    Home,
  }
};
</script>

<style lang="scss">
	:root {
		--primary: #0074D9;
		--secondary: #A8DAFF;
		--success: #71F79F;
		--typeface: #333333;
		--gray-3: #828282;
		--gray-4: #BDBDBD;
		--box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.1);
	}
</style>
