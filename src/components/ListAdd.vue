<template>
  <form :class="classList" action="addlist" @submit.prevent="addList">
    <input
      v-model="title"
      type="text"
      class="text-input"
      placeholder="Add new list"
      @focusin="startEditing"
      @focusout="finishEditing"
      >
    <button
      type="submit"
      :class="titleExists"
      class="add-button"
      v-if="isEditing || titleExists"
      >
      Add
    </button>
  </form>
</template>

<script>
export default {
   name: 'ListAdd',
  data () {
    return {
      title: '',
      isEditing: false,
    }
  },
  methods: {
    addList() {
      this.$store.dispatch('addlist', { title: this.title })
      this.title = ''
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
      return this.title.length > 0 ? 'addable' : ''
    },
  }
}
</script>
