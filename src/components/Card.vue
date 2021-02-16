<template>
   <div class="card">
    <button class="close-button" @click="removeCardFromList">
      ×
    </button>
    <div class="body">
      {{ body }}
    </div>
    <p>{{ text }}</p>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    body: {
      type: String,
      required: true
    },
    text: {
      type: String,
      required: false
    },
    listIndex: {
      type: Number,
      required: true
    },
    cardIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    removeCardFromList() {
      if(confirm('本当にこのカードを削除しますか？')) {
        this.$store.dispatch('removeCardFromList', { cardIndex: this.cardIndex, listIndex: this.listIndex })
      }
    }
  },

}
</script>

<style>

</style>