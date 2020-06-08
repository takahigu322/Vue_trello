<template>
  <div>
    <header>higu Trello</header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <draggable :list="lists" @end="movingList" class="list-index">
        <list
          v-for="(item, index) in lists"
          :key="item.id"
          :title="item.title"
          :cards="item.cards"
          :listIndex="index"
          @change="movingCard"
        />
        <list-add />
      </draggable>
      <!-- ★ここまで追記 -->
    </main>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import ListAdd from "./ListAdd";
// ★ここから追記
import List from "./List";
import { mapState } from "vuex";
// ★ここまで追記

export default {
  components: {
    draggable,
    ListAdd,
    // ★追記
    List
  },
  // ★追記
  computed: {
    ...mapState(["lists"]),
    totalCardCount() {
      return this.$store.getters.totalCardCount;
    }
  },
  methods: {
    movingCard: function() {
      this.$store.dispatch("updateList", { lists: this.lists });
    },
    movingList: function() {
      this.$store.dispatch("updateList", { lists: this.lists });
    }
  }
};
</script>
