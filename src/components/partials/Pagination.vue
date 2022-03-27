<template>
  <div class="pagination-container">
    <nav aria-label="Page navigation example" v-if="nbrPages > 1">
      <ul class="pagination">
        <li
          v-if="page > 1"
          :class="['page-item', page == 1 ? 'disabled' : '']"
          @click="changePage(page - 1)"
        >
          <a
            class="page-link"
            href="#"
            :aria-disabled="page == 1 ? true : false"
            >Previous</a
          >
        </li>
        <li
          v-for="(item, index) in 5"
          :key="index"
          :class="['page-item', index + 1 == page ? 'active' : '']"
          @click="changePage(index + 1)"
        >
          <a class="page-link" href="#">{{ index + 1 }}</a>
        </li>

        <li
          v-if="page < 5"
          :class="['page-item', page == 5 ? 'disabled' : '']"
          @click="changePage(page + 1)"
        >
          <a class="page-link" href="#">Next</a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
// import { eventBus } from '../../main';
export default {
  name: 'Pagination',
  data() {
    return {};
  },
  props: {
    // method,
    nbrPages: {
      type: Number,
      required: true,
    },
    page: {
      type: Number,
      required: true,
    },
  },
  methods: {
    changePage(page) {
      console.log('pagination : ' + page);
      this.$emit('change-page', page);
    },
  },
};
</script>

<style lang="scss" scoped>
.pagination-container {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
