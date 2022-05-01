<template>
  <div id="app">
    <v-app>
      <v-tabs>
        <v-tab
          v-for="item in items"
          :key="item">
          {{ item }}
        </v-tab>
        <v-tab-item>
          <Alert />
        </v-tab-item>
        <v-tab-item>
          <Tree />
        </v-tab-item>
			</v-tabs>
    </v-app>
  </div>
</template>

<script>
import Tree from './components/Tree.vue'
import Alert from './components/Alert.vue'

export default {
  name: 'App',
  components: {
    Tree,
    Alert
  },
  data: () => ({
    items: ['題目一','題目二']
  })
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
</style>
