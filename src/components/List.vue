<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <p class="list-counter">total: {{ totalCardInList }}</p>
      <div class="deletelist" @click="removeList">×</div>
    </div>
    <div class="cardInputBox">
      <draggable
        group="cards"
        :list="cards"
        @end="$emit('change')"
        >
        <card
          v-for="(item, index) in cards"
          :body="item.body"
          :key="item.id"
          :cardIndex="index"
          :listIndex="listIndex"
          :text="item.text"
        />
        <CardAdd :listIndex='listIndex' />
      </draggable>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import CardAdd from './CardAdd.vue'
import Card from './Card.vue'

export default {
  name: 'List',
  components: {
    Card,
    CardAdd,
    draggable
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    cards: {
      type: Array,
      required: true
    },
    listIndex: {
      type: Number,
      required: true,
    },
  },
  methods: {
    removeList() {
      if(confirm('本当にこのリストを削除しますか？')){
        this.$store.dispatch('removelist', { listIndex: this.listIndex })
      }
    }
  },
  computed: {
    totalCardInList() {
      return this.cards.length
    }
  }
}
</script>

<style>

</style>