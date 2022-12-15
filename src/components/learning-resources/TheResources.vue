<template>
  <base-card>
    <base-button :mode="storedResourceMode" @click="setSelectedTab('stored-resources')">Stored Resources</base-button>
    <base-button :mode="addResourceMode" @click="setSelectedTab('add-resource')">Add Resources</base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>

import StoredResources from "./StoredResources.vue";
import AddResource from "./AddResource.vue";

export default {
  components: { StoredResources, AddResource },
  computed: {
    storedResourceMode: function () {
      return this.selectedTab == 'stored-resources' ? null : 'flat'
    },

    addResourceMode: function () {
      return this.selectedTab == 'add-resource' ? null : 'flat'
    }
  },
  mounted: function () {
    const LS = localStorage.getItem('resources');
    console.log(JSON.parse(LS));
    if (LS && JSON.parse(LS).length > 0) {
      const items = JSON.parse(LS);
      for (const key in items) {
        if (Object.hasOwnProperty.call(items, key)) {
          const element = items[key];
          this.storedResources.push(element);
        }
      }
    } else {
      localStorage.setItem('resources', JSON.stringify([]));
      this.storedResources = [];
    }
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: []
    }
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource,
    }
  },
  methods: {
    setSelectedTab(name) {
      this.selectedTab = name;
    },
    addResource(title, description, link) {
      this.storedResources.push({
        id: (new Date).toISOString(),
        title, description, link
      });
      const items = [...this.storedResources];
      console.log(items);
      localStorage.setItem('resources', JSON.stringify(items));

      this.setSelectedTab('stored-resources');
      console.log('added', this.storedResources.length);
    },
    deleteResource(id) {
      console.log(id);
      const deleteIndex = this.storedResources.findIndex(item => item.id === id);
      this.storedResources.splice(deleteIndex, 1);
      localStorage.setItem('resources', JSON.stringify(this.storedResources));
    }
  }

}
</script>