<template>
<div>
  <header>
    my Trello
  </header>
  <main>
    <p class="info-line">All: {{ totalTasks }} tasks</p>
    <draggable :list="lists" class="list-index" @end="movingList">
      <List
        v-for="(item, index) in lists"
        :key="item.id"
        :title="item.title"
        :listIndex="index"
        :cards="item.cards"
        @change="movingCard"
       />
      <ListAdd />
    </draggable>
  </main>
</div>
</template>

<script>
import draggable from 'vuedraggable'
import ListAdd from './ListAdd.vue'
import List from './List.vue'
import { mapState } from 'vuex'

export default {
  name: 'Board',
  components: {
    List,
    ListAdd,
    draggable
  },
  computed: {
    ...mapState([
      'lists'
    ]),
    totalTasks() {
      return this.$store.getters.totalTasks
    }
  },
  methods: {
    movingCard() {
      this.$store.dispatch('updateList', { lists: this.lists })
    },
    movingList() {
      this.$store.dispatch('updateList', { lists: this.lists })
    }
  },
}
</script>
