<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <div class="deletelist" @click="removeList">×</div>
    </div>
    <card
      v-for="(item, index) in cards"
      :body="item.body"
      :key="item.id"
      :cardIndex="index"
      :listIndex="listIndex"
    />
    <CardAdd :listIndex='listIndex' />
  </div>
</template>

<script>
import CardAdd from './CardAdd.vue'
import Card from './Card.vue'

export default {
  name: 'List',
  components: {
    Card,
    CardAdd
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
}
</script>

<style>

</style>