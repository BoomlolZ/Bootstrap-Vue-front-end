<template>
  <div>
    <b-button
      variant="warning"
      class="mr-1"
      @click="showModal"
    >
      <b-icon icon="pencil-square"></b-icon>
    </b-button>
    
    <b-modal
      ref="my-modal"
      hide-header-close
      title="Edit Data"
      header-bg-variant="success"
      header-text-variant="white"
    >
      <label>First-name</label>
      <b-form-input v-model="p_fname"></b-form-input>
      <label>Last-name</label>
      <b-form-input v-model="p_lname"></b-form-input>
      <label>User-name</label>
      <b-form-input v-model="p_username"></b-form-input>
      <label>E-mail</label>
      <b-form-input v-model="p_email"></b-form-input>
      <label>Avatar</label>
      <b-form-input v-model="p_avatar"></b-form-input>
      <template #modal-footer="{ hide }">
        <b-button  variant="danger" class="mt-3" @click="hide();">Cancel</b-button>
        <b-button  variant="success" class="mt-3" @click="$emit('edit', {
              id,
              p_fname,
              p_lname,
              p_username,
              p_email,
              p_avatar,
            });hide();">Save</b-button>
      </template>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: "EditBtn",
  props: {
    id: Number,
    fname: String,
    lname: String,
    username: String,
    email: String,
    avatar: String,
  },
  data() {
    return {
      p_fname: this.fname,
      p_lname: this.lname,
      p_username: this.username,
      p_email: this.email,
      p_avatar: this.avatar,
      dialog: false,
    };
  },

    methods: {
    showModal() {
      this.$refs["my-modal"].show();
    },
  },
};
</script>
