<template>
  <PWAPrompt />
  <img alt="Vue logo" src="./assets/logo.png">
  <h1>PWA example on vue</h1>
  <MeasurementsTable />
</template>

<script>
import PWAPrompt from './components/PWAPrompt.vue'
import MeasurementsTable from './components/MeasurementsTable.vue';

export default {
  name: 'App',
  components: {
    PWAPrompt,
    MeasurementsTable
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
	margin: 0 auto;
	width: 100%;
	max-width: 24rem;
}

:root {
	--background: #e0fbfc;
	--bright: #ee6c4d;
	--dark: #587faf;
	--darker: #293241;
	--accent: #98c1d9;
}

*,
*:before,
*:after {
	box-sizing: border-box;
	font-family: inherit;
	color: inherit;
	max-width: 100%;
}

*:focus {
	outline: 2px solid var(--bright);
	outline-offset: 2px;
}
</style>
