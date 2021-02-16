<template>
  <form :class="classList" class="addcard" @submit.prevent="addCardToList">
    <input v-model="body"
      type="text"
      class="text-input"
      placeholder="Add new card"
      @focusin="startEditing"
      @focusout="finishEditing"
    />
    <button
      type="submit"
      :class="titleExists"
      class="add-button"
      v-if="isEditing || titleExists">
      Add
    </button>
  </form>
</template>

<script>
export default {
  name: 'CardAdd',
  props: {
    listIndex: {
      type: Number,
      required: true,
    }
  },
  data() {
    return {
      body: '',
      isEditing: false,
    }
  },
  methods: {
    addCardToList() {
      this.$store.dispatch('addCardToList', { body: this.body, listIndex: this.listIndex })
      this.body = ''
    },
    startEditing() {
      this.isEditing = true
    },
    finishEditing() {
      this.isEditing = false
    }
  },
  computed: {
    classList() {
      return this.isEditing ? 'active' : ''
    },
    titleExists() {
      return this.body.length > 0 ? 'addable' : ''
    },
  }
}
</script>

<style>

</style>