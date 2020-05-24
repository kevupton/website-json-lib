<template>
  <div class="hello" v-if="value">
    <h2>{{ meta.name }} {{ value.path }}</h2>
    <item :id="value.metaTags" />
  </div>
</template>

<script>
module.exports = {
  name: "HelloWorld",
  props: ["value", "meta", "namespaceService"],

  mounted: function() {
    const newValue = { ...this.value };
    var changes = false;

    if (!this.value.metaTags) {
      newValue.metaTags = this.namespaceService.createItem("meta-tags");
      changes = true;
    }

    if (changes) {
      this.$emit("input", newValue);
    }
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
