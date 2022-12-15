<template>
  <base-card>
    <li>
      <div>
        <header>
          <h3>{{ title }}</h3>
          <base-button @click="deleteResource(id)" mode="flat">Delete</base-button>
        </header>
      </div>
      <p>{{ description }}</p>
      <nav>
        <a :href="link">View resource</a>
      </nav>
    </li>
  </base-card>
</template>

<script>
export default {
  inject: ['deleteResource'],
  props: {
    id: {
      type: String,
      required: true
    },
    title: {
      String,
      required: true,
    },
    link: {
      String,
      required: true,
    },
    description: {
      String,
      required: true,
    }
  },
  data() {
    return {

    }
  }
}
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>