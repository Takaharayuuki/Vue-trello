<template>
  <form class="addcard" @submit.prevent="addCardToList">
    <input v-model="body"
           type="text"
           class="text-input"
           placeholder="Add new card"
    />
    <button type="submit" class="add-button">
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
    }
  },
  methods: {
    addCardToList() {
      this.$store.dispatch('addCardList', { body: this.body, listIndex: this.listIndex })
      this.body = ''
    }
  },
}
</script>

<style>

</style>