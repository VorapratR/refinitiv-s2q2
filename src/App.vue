<template>
  <div id="app">
    <b-container>
      <b-row class="my-3">
        <b-col>
          <b-input
            v-model="input"
            placeholder="Filter category"
            @keyup="filterCategory()"
          ></b-input>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <b-table-simple
            v-if="categories.length != 0"
            striped
            hover
            :borderless="true"
            :outlined="false"
          >
            <b-thead>
              <b-tr>
                <b-th>No</b-th>
                <b-th>Category name</b-th>
              </b-tr>
            </b-thead>
            <b-tbody>
              <b-tr v-for="(category, index) in categories" :key="index">
                <b-td> {{ index + 1 }} </b-td>
                <b-td> {{ category }} </b-td>
              </b-tr>
            </b-tbody>
          </b-table-simple>
          <div v-else>
            <h5>No category</h5>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      categories: [],
      input: "",
    };
  },
  created() {
    this.getCategories();
  },
  methods: {
    getCategories() {
      let api = "https://api.publicapis.org/categories";
      this.axios.get(api).then((response) => {
        this.categories = response.data;
      });
    },
    controlFilter() {
      this.input == "" ? this.getCategories() : this.filterCategory();
    },
    filterCategory() {
      let bufferCategories = this.categories.filter((category) =>
        category.includes(this.input)
      );
      this.categories = bufferCategories;
    },
  },
};
</script>

<style>
</style>
