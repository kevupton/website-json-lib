<template>
  <div>
    <md-table>
      <md-table-row>
        <md-table-head>Path</md-table-head>
        <md-table-head>Name</md-table-head>
        <md-table-head>Created At</md-table-head>
        <md-table-head>Last Updated</md-table-head>
        <md-table-head></md-table-head>
      </md-table-row>

      <md-table-row v-for="page in pages" :key="page.id">
        <md-table-cell>{{ page.value.path }}</md-table-cell>
        <md-table-cell>{{ page.meta.name }}</md-table-cell>
        <md-table-cell md-date>{{
          page.createdAt.toDateString()
        }}</md-table-cell>
        <md-table-cell md-date>{{ page.updatedAt }}</md-table-cell>
        <md-table-cell md-date>
          <md-button
            class="md-icon-button md-dense md-raised"
            @click="editPage(page.id)"
          >
            <md-icon>edit</md-icon>
          </md-button>
          <md-button
            class="md-icon-button md-dense md-accent md-raised"
            @click="deletePage(page.id)"
          >
            <md-icon>delete</md-icon>
          </md-button>
        </md-table-cell>
      </md-table-row>

      <md-table-row>
        <md-table-cell colspan="2">
          <md-field>
            <label>Name</label>
            <md-input v-model="name" required />
          </md-field>
        </md-table-cell>
        <md-table-cell colspan="2">
          <md-field>
            <label>Path</label>
            <md-input v-model="path" required />
          </md-field>
        </md-table-cell>
        <md-table-cell>
          <md-button class="md-primary md-raised" @click="create()">
            Create
          </md-button>
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
    return {
      pages: [],
      path: "",
      name: "",
      subscription: undefined
    };
  },
  methods: {
    create: function() {
      if (!this.path || !this.name) {
        return;
      }

      this.namespaceService.createItem({
        component: "page",
        value: { path: this.path },
        meta: { name: this.name }
      });

      this.name = "";
      this.path = "";
    },
    deletePage: function(pageId) {
      this.namespaceService.deleteItem(pageId);
    },
    editPage: function(pageId) {
      this.$router.push("/item/" + pageId);
    }
  },
  mounted: function() {
    const self = this;
    this.subscription = this.namespaceService
      .filterItems({ component: "page" })
      .subscribe(function(pages) {
        self.pages = pages;
      });
  },
  destroyed: function() {
    this.subscription.unsubscribe();
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
