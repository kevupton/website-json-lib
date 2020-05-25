<template>
  <div>
    <md-tabs
      class="md-primary"
      md-alignment="centered"
      @change="(activeTab = $event)"
    >
      <md-tab id="generic" md-icon="home"></md-tab>
      <md-tab id="facebook" md-icon="https://raw.githubusercontent.com/kevupton/website-json-lib/master/src/assets/facebook.svg"></md-tab>
      <md-tab id="twitter" md-icon="https://raw.githubusercontent.com/kevupton/website-json-lib/master/src/assets/twitter.svg"></md-tab>
    </md-tabs>
    <md-content>
      <template v-if="activeTab === 'generic'">

      </template>
      <template v-else-if="activeTab === 'facebook'"> </template>
      <template v-else-if="activeTab === 'twitter'"> </template>
    </md-content>
  </div>
</template>

<script>
module.exports = {
  name: "MetaTags",
  props: ["value"],
  data: function() {
    return {
      activeTab: "generic"
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
