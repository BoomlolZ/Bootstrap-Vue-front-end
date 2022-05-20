<template>
  <div class="">
    <b-button variant="danger" id="show-btn" class="mr-1" @click="showModal">
      <b-icon icon="trash"></b-icon>
    </b-button>
    <b-modal ref="my-modal" hide-header-close  title="Confirm your Delete">
      <div class="d-block text-center">
        <h4>Are you sure to Delete this Data</h4>
      </div>
      <template #modal-footer="{ hide }">
        <b-button   class="mt-3" @click="hide()">Cancel</b-button>
        <b-button  variant="danger" class="mt-3" @click="$emit('delete',{id});hide()">Delete</b-button>
      </template>
    </b-modal>
  </div>
</template>
<script>
export default {
  name: "DeleteBtn",
  props: {
    id: Number,
  },
  data() {
    return {
    };
  },
  methods: {
    showModal() {
      this.$refs["my-modal"].show();
    },
  },
};
</script>
