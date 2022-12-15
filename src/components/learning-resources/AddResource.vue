<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid data" @close="confirmError">
    <template #default>
      <p>Unfortunately you cannot add a resource with invalida data</p>
      <p>second</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Gotcha</base-button>
    </template>
  </base-dialog>
  <base-card>
    <h2>Add resource</h2>
    <form @submit.prevent="onSubmit">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="title" ref="titleRef" />
      </div>

      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          type="text"
          name="description"
          id="description"
          ref="descriptionRef"
        ></textarea>
      </div>

      <div class="form-control">
        <label for="link">link</label>
        <input type="text" name="link" id="link" ref="linkRef" />
      </div>

      <div>
        <base-button type="submit">Add resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false
    };
  },
  methods: {
    onSubmit() {
      const enteredTitle = this.$refs.titleRef.value;
      const enteredDescription = this.$refs.descriptionRef.value;
      const enteredLink = this.$refs.linkRef.value;
      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(enteredTitle, enteredDescription, enteredLink);
    },
    confirmError(){
      this.inputIsInvalid = false;
    }
  }
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>