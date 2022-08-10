<template>
  <b-container>
    <h3>
      {{ title }}:
      <slot></slot>
    </h3>
    <b-row>
      <b-col v-for="r in recipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import RecipePreview from "./RecipePreview.vue";
export default {
  name: "RecipePreviewList",
  components: {
    RecipePreview,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    searchQuery: {
      type: String,
      required: false,
    },
    amount: {
      type: String,
      required: false,
    },
    cuisine: {
      type: String,
      required: false,
    },
    diet: {
      type: String,
      required: false,
    },
    intolerance: {
      type: String,
      required: false,
    },
  },
  data() {
    return {
      recipes: [],
    };
  },
  mounted() {
    this.updateRecipes();
  },
  methods: {
    async updateRecipes() {
      if (this.title == "Randome Recipes") {
        await this.randomRecipes();
      } else if (this.title == "Search Results") {
        await this.searchRecipes();
      }
    },
    async randomRecipes() {
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/recipes/random"
          // "https://test-for-3-2.herokuapp.com/recipes/random"
        );

        // console.log(response);
        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
        // console.log(this.recipes);
      } catch (error) {
        console.log(error);
      }
    },
    async searchRecipes() {
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain +
            "/recipes/search" +
            "?query=" +
            this.searchQuery +
            "&amount=" +
            this.amount +
            "&cuisine=" +
            this.cuisine +
            "&diet=" +
            this.diet +
            "&intolerance=" +
            this.intolerance
          // "https://test-for-3-2.herokuapp.com/recipes/random"
        );

        // console.log(response);
        // console.log(response.data.results);
        const recipes = response.data.results;
        this.recipes = [];
        this.recipes.push(...recipes);
        // console.log(this.recipes);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  min-height: 400px;
}
</style>
