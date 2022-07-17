<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>Please check all inputs and make sure you enter at least a few characters into each input field.</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" v-model="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" v-model="descInput"></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" v-model="linkInput" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import axios from 'axios';
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false,
      titleInput : '',
      descInput : '',
      linkInput : ''
    };
  },
  methods: {
    submitData() {

      if (
        this.titleInput.trim() === '' ||
        this.descInput.trim() === '' ||
        this.linkInput.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      axios.post('https://foggett-f7580-default-rtdb.firebaseio.com/data.json', {
        id : new Date().toISOString(),
        title : this.titleInput,
        description : this.descInput,
        url : this.linkInput
      })

      this.titleInput = ''
      this.descInput = ''
      this.linkInput = ''

    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  },
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