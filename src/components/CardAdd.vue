<template>
  <form :class="classList" class="addcard" @submit.prevent="addCardToList">
    <input v-model="body"
      type="text"
      class="title-input"
      placeholder="Add new card title"
      @focusin="startEditing"
      @focusout="finishEditing"
    />
    <input 
    v-model="text"
    type="text"
    class="cardText-input"
    placeholder="Add text"
    @focusin="startEditing"
    @focusout="finishEditing"
    style="margin-top:15px;">
    <button
      type="submit"
      :class="titleExists || textExists"
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
      text: '',
      isEditing: false,
    }
  },
  methods: {
    addCardToList() {
      this.$store.dispatch('addCardToList', { body: this.body, text:this.text, listIndex: this.listIndex })
      this.body = ''
      this.text = ''
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
      return this.body.length > 0  ? 'addable' : ''
    },
    textExists() {
      return this.text.length > 0  ? 'addable' : ''
    },
  }
}
</script>

<style>

</style>