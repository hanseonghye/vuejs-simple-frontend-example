<template>
  <section class="section">
    <div class="container is-fluid">
      <div class="columns">
        <div class="column is-9">
          <h1 class="title">
            <i class="fa fa-cube"></i>
            Tasks
          </h1>
        </div>

        <div class="column has-text-right">
          <router-link class="button is-primary" to="/tasks/new">
            <i class="fa fa-fw fa-plus"></i>
            New Task
          </router-link>
        </div>
      </div>

      <ListView :collection="paginatedItems" />

      <hr />

      <b-pagination
        :total="item.length"
        :surrent.sync="current"
        :order="order"
        :size="size"
        :simple="isSimple"
        :rounded="isrounded"
        :per-page="perPage"
        icon-pack="fa"
        aria-next-label="Next page"
        aria-previous-label="Previous page"
        aria-page-label="Page"
        aria-current-label="current page"
      >
      </b-pagination>
    </div>
  </section>
</template>

<script>
import { mapGetters } from "vuex";
import ListView from "@/modules/task/components/TaskList";

function paginate(array, page_size, page_number) {
  --page_number;
  return array.slice(page_number * page_size, (page_number + 1) * page_size);
}

export default {
  name: "TaskList",
  data() {
    return {
      total: 200,
      current: 1,
      perPage: 5,
      order: "",
      size: "",
      isSimple: false,
      isRounded: false
    };
  },
  components: {
    ListView
  },
  metaInfo: {
    title: "Tasks"
  },
  computed: {
    ...mapGetters({
      item: "task/collection/items"
    }),
    paginatedItems() {
      return paginate(this.items, this.perPage, this.current);
    }
  }
};
</script>
