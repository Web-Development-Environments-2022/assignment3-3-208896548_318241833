<template>
  <div class="container">
    <h1 class="title">Search Page</h1>
    <br />
    <b-form-input v-model="text" placeholder="Enter your search"></b-form-input>
    <!-- <div class="mt-2">Value: {{ text }}</div> -->
    <br />
    <b-form-select
      v-model="selected_size"
      :options="options_size"
      class="mb-3"
      value-field="item"
      text-field="name"
      disabled-field="notEnabled"
    ></b-form-select>
    <br />
    <b-form-select
      v-model="selected_cuisines"
      :options="options_cuisines"
      class="mb-3"
      value-field="item"
      text-field="name"
      disabled-field="notEnabled"
    ></b-form-select>
    <br />
    <b-form-select
      v-model="selected_diets"
      :options="options_diets"
      class="mb-3"
      value-field="item"
      text-field="name"
      disabled-field="notEnabled"
    ></b-form-select>
    <br />
    <b-form-select
      v-model="selected_intolerances"
      :options="options_intolerances"
      class="mb-3"
      value-field="item"
      text-field="name"
      disabled-field="notEnabled"
    ></b-form-select>

    <!-- Selected: <strong>{{ selected }}</strong> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: "",
      selected_size: "5",
      options_size: [
        { item: "5", name: "5 search results" },
        { item: "10", name: "10 search results" },
        { item: "15", name: "15 search results" },
      ],
      selected_cuisines: "A",
      options_cuisines: [
        { item: "A", name: "5 search results" },
        { item: "B", name: "10 search results" },
        { item: "C", name: "15 search results" },
      ],
      selected_diets: "A",
      options_diets: [
        { item: "A", name: "5 search results" },
        { item: "B", name: "10 search results" },
        { item: "C", name: "15 search results" },
      ],
      selected_intolerances: "A",
      options_intolerances: [
        { item: "A", name: "5 search results" },
        { item: "B", name: "10 search results" },
        { item: "C", name: "15 search results" },
      ],
    };
  },
};
</script>
