<template>
  <div>
    <md-table>
      <md-table-row>
        <md-table-head md-numeric>ID</md-table-head>
        <md-table-head>Path</md-table-head>
        <md-table-head>Created At</md-table-head>
        <md-table-head>Last Updated</md-table-head>
      </md-table-row>

      <md-table-row v-for="page in pages" :key="page.id">
        <md-table-cell md-numeric>{{ page.id }}</md-table-cell>
        <md-table-cell>{{ page.value.path }}</md-table-cell>
        <md-table-cell md-date>{{ page.createdAt }}</md-table-cell>
        <md-table-cell md-date>{{ page.updatedAt }}</md-table-cell>
      </md-table-row>

      <md-table-row>
        <md-table-cell md-numeric></md-table-cell>
        <md-table-cell>
          <md-field>
            <label>Page Path</label>
            <md-input
              v-model="newPagePath"
              required
            />
          </md-field>
        </md-table-cell>
        <md-table-cell></md-table-cell>
        <md-table-cell>
            <md-button class="md-primary md-raised" @click="create()">Add</md-button>
        </md-table-cell>
      </md-table-row>
    </md-table>
  </div>
</template>

<script>
module.exports = {
  name: "PageLayout",
  props: ["namespaceService"],
  data: function() {
    const self = this;
    return {
      pages: [],
      newPagePath: '',
      subscription: this.namespaceService
        .filterItems({ component: "page" })
        .subscribe(function(pages) {
          self.pages = pages;
        })
    };
  },
  methods: {
    create: function() {
      if (!this.newPagePath) {
        return;
      }

      this.namespaceService.createItem({
        component: 'page',
        value: { path: this.newPagePath },
      });

      this.newPagePath = '';
    }
  },
  destroyed: function() {
    this.subscription.unsubscribe();
    console.log(this);
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
