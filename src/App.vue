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
                <em>personal</em>
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
            <!-- <b-nav-item v-b-modal.create-recipe v-if="$root.store.username"
              >Create recipe</b-nav-item
            > -->
          </b-navbar-nav>

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
      <!-- <b-modal id="create-recipe" class="attachToDocument: true"
        >Hello From My Modal!</b-modal
      > -->
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
  methods: {
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
