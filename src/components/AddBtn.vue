<template>
  <div>
    <b-button pill @click="$bvModal.show('modal-scoped')" variant="primary" size="lg">
      Add Data 
    <b-icon icon="file-earmark-plus"></b-icon>
    </b-button>

    <b-modal
      id="modal-scoped"
      ref="my-modal"
      hide-header-close
      title="Add new Data"
      header-bg-variant="primary"
      header-text-variant="white"
    >
      <label>First-name</label>
      <b-form-input v-model="fname" placeholder="Enter your First-name"></b-form-input>
      <label>Last-name</label>
      <b-form-input v-model="lname" placeholder="Enter your Last-name"></b-form-input>
      <label>User-name</label>
      <b-form-input v-model="username" placeholder="Enter your User-name"></b-form-input>
      <label>E-mail</label>
      <b-form-input v-model="email" placeholder="Enter your E-mail"></b-form-input>
      <label>Avatar</label>
      <b-form-input v-model="avatar" placeholder="Enter your Avatar"></b-form-input>
      <template #modal-footer="{ hide }">
        <b-button  variant="danger" class="mt-3" @click="clear();hide()">Cancel</b-button>
        <b-button v-b-modal.modal-multi-3 variant="success" class="mt-3" @click="$emit('save',saveData());hide();clear()">Save</b-button>
      </template>
    </b-modal>
     <!-- <b-modal 
     hide-header-close 
     id="modal-multi-3" 
     size="sm" title="Thank you!" 
     header-bg-variant="success"
     header-text-variant="white"
     ok-only>
    <p class="my-1">Create success!</p>
  </b-modal> -->
  </div>
</template>
<script>

export default {
  name: "AddBtn",
  data() {
    return {
      fname: "",
      lname: "",
      username: "",
      email: "",
      avatar: "",
    };
  },
  validations(){
    return {
      fname:"",
      lname: "",
      username: "",
      email: "",
      avatar: "",
    }
  },
  methods: {
    saveData() {
      const data = {
        fname: this.fname,
        lname: this.lname,
        username: this.username,
        email: this.email,
        avatar: this.avatar,
      };
      return data;
    },
    clear() {
      this.fname = "";
      this.lname = "";
      this.username = "";
      this.email = "";
      this.avatar = "";
    },
  },
};
</script>
