<template>
  <div id="app">
    <div id="nav">
      <b-navbar toggleable="lg" type="light" variant="info" id="navb">
        <b-navbar-brand id="nav-brand" href="#" disabled>YumTum</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <b-nav-item :to="{ name: 'main' }">Main</b-nav-item>
            <b-nav-item :to="{ name: 'search' }">Search</b-nav-item>
            <b-nav-item :to="{ name: 'about' }">About</b-nav-item>
            <b-nav-item-dropdown v-if="$root.store.username">
              <!-- Using 'button-content' slot -->
              <template #button-content>
                <em>Personal</em>
              </template>
              <b-dropdown-item :to="{ name: 'favorites' }"
                >Favorites recipes</b-dropdown-item
              >
              <b-dropdown-item :to="{ name: 'my_recipes' }"
                >My recipes</b-dropdown-item
              >
              <b-dropdown-item :to="{ name: 'family' }"
                >Family recipes</b-dropdown-item
              >
            </b-nav-item-dropdown>
            <b-nav-item v-b-modal.create v-if="$root.store.username"
              >Create Recipe</b-nav-item
            >
          </b-navbar-nav>
          <b-modal
            id="create"
            title="Create Recipe"
            @show="resetModal"
            @hidden="resetModal"
            @ok="handleOk"
          >
            <form ref="form" @submit.stop.prevent="handleSubmit">
              <b-form-group
                label="title"
                label-for="title-input"
                invalid-feedback="Title is required"
                :state="titleState"
              >
                <b-form-input
                  id="title-input"
                  :state="titleState"
                  required
                ></b-form-input>
              </b-form-group>

              <b-form-group
                label="ready in X minutes"
                label-for="readyInMinutes-input"
                invalid-feedback="readyInMinutes is required"
                :state="readyInMinutesState"
              >
                <b-form-input
                  id="readyInMinutes-input"
                  :state="readyInMinutesState"
                  required
                ></b-form-input>
              </b-form-group>

              <b-form-group
                label="image"
                label-for="image-input"
                invalid-feedback="image is required"
                :state="imageState"
              >
                <b-form-input
                  id="image-input"
                  :state="imageState"
                  required
                ></b-form-input>
              </b-form-group>

              <b-form-group label="vegan ?" label-for="vegan-input">
                <b-form-checkbox
                  id="vegan-input"
                  value="true"
                  unchecked-value="false"
                ></b-form-checkbox>
              </b-form-group>

              <b-form-group label="vegetarian ?" label-for="vegetarian-input">
                <b-form-checkbox
                  id="vegetarian-input"
                  value="true"
                  unchecked-value="false"
                ></b-form-checkbox>
              </b-form-group>

              <b-form-group label="gluten free ?" label-for="glutenFree-input">
                <b-form-checkbox
                  id="glutenFree-input"
                  value="true"
                  unchecked-value="false"
                ></b-form-checkbox>
              </b-form-group>

              <b-form-group
                label="ingredients"
                label-for="extendedIngredients-input"
                invalid-feedback="ingredients is required"
                :state="extendedIngredientsState"
              >
                <b-form-textarea
                  id="extendedIngredients-input"
                  :state="extendedIngredientsState"
                  required
                ></b-form-textarea>
              </b-form-group>

              <b-form-group
                label="instructions"
                label-for="instructions-input"
                invalid-feedback="instructions is required"
                :state="instructionsState"
              >
                <b-form-textarea
                  id="instructions-input"
                  :state="instructionsState"
                  required
                ></b-form-textarea>
              </b-form-group>

              <b-form-group
                label="servings"
                label-for="servings-input"
                invalid-feedback="servings is required"
                :state="servingsState"
              >
                <b-form-input
                  id="servings-input"
                  :state="servingsState"
                  required
                ></b-form-input>
              </b-form-group>
            </form>
          </b-modal>
          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto" v-if="!$root.store.username">
            <b-nav-item-dropdown right>
              <!-- Using 'button-content' slot -->
              <template #button-content>
                <em>hello guest</em>
              </template>
              <b-dropdown-item :to="{ name: 'login' }">Login</b-dropdown-item>
              <b-dropdown-item :to="{ name: 'register' }"
                >Register</b-dropdown-item
              >
            </b-nav-item-dropdown>
          </b-navbar-nav>
          <b-navbar-nav class="ml-auto" v-else>
            <b-nav-item-dropdown right>
              <!-- Using 'button-content' slot -->
              <template #button-content>
                <em>{{ $root.store.username }}</em>
              </template>
              <b-dropdown-item @click="Logout">Logout</b-dropdown-item>
            </b-nav-item-dropdown>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      titleState: null,
      readyInMinutesState: null,
      imageState: null,
      veganState: null,
      vegetarianState: null,
      glutenFreeState: null,
      extendedIngredientsState: null,
      instructionsState: null,
      servingsState: null,
    };
  },
  methods: {
    checkFormValidity() {
      const valid = this.$refs.form.checkValidity();
      this.titleState = valid;
      this.readyInMinutesState = valid;
      this.imageState = valid;
      this.veganState = valid;
      this.vegetarianState = valid;
      this.glutenFreeState = valid;
      this.extendedIngredientsState = valid;
      this.instructionsState = valid;
      this.servingsState = valid;
      return valid;
    },
    resetModal() {
      this.titleState = null;
      this.readyInMinutesState = null;
      this.imageState = null;
      this.veganState = null;
      this.vegetarianState = null;
      this.glutenFreeState = null;
      this.extendedIngredientsState = null;
      this.instructionsState = null;
      this.servingsState = null;
    },
    handleOk(bvModalEvent) {
      // Prevent modal from closing
      bvModalEvent.preventDefault();
      // Trigger submit handler
      this.handleSubmit();
    },
    handleSubmit() {
      // Exit when the form isn't valid
      if (!this.checkFormValidity()) {
        return;
      }
      // Hide the modal manually
      this.$nextTick(() => {
        this.$bvModal.hide("create");
        this.resetModal();
      });
    },
    Logout() {
      this.$root.store.logout();
      this.$root.toast("Logout", "User logged out successfully", "success");

      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    },
  },
};
</script>

<style lang="scss">
@import "@/scss/form-style.scss";

.container {
  background-color: rgb(51, 232, 220);
  background-size: cover;
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  border-radius: 2%;
  border-style: dotted;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background: url("https://previews.123rf.com/images/topform8/topform81307/topform8130700236/20674500-cookery-seamless-background.jpg");
  background-size: cover;
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
}

#nav {
  padding: 30px;
  color: rgb(51, 232, 220);
}
#navb {
  border-radius: 10%;
  border-style: dotted;
}
#nav-brand {
  background-color: rgb(51, 232, 220);
  border-radius: 5%;
  border-style: dotted;
}
#nav-collapse {
  background-color: rgb(51, 232, 220);
  border-radius: 5%;
  border-style: dotted;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
