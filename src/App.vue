<template>
  <div class="page-container">
    <md-app md-waterfall md-mode="fixed">
      <md-app-toolbar class="md-primary">
        <link
          href="https://fonts.googleapis.com/icon?family=Material+Icons"
          rel="stylesheet"
        />
        <md-button class="md-icon-button" @click="menuVisible = !menuVisible">
          <md-icon>menu</md-icon>
        </md-button>
        <md-button to="/">
          <span class="md-title">CocktailAPP</span>
        </md-button>
        <div class="md-toolbar-section-end"></div>
      </md-app-toolbar>

      <md-app-drawer :md-active.sync="menuVisible" :key="$route.fullPath">
        <md-toolbar class="md-transparent" md-elevation="0">
          <span>Navigation</span>
          <div class="md-toolbar-section-end">
            <md-button class="md-icon-button md-dense" @click="toggleMenu">
              <md-icon>keyboard_arrow_left</md-icon>
            </md-button>
          </div>
        </md-toolbar>
        <md-list>
          <md-list-item to="/">
            <md-icon>home</md-icon>
            <span class="md-list-item-text">Home</span>
          </md-list-item>
          <md-list-item to="/categories">
            <md-icon>local_bar</md-icon>
            <span class="md-list-item-text">Types of drinks</span>
          </md-list-item>
          <md-list-item to="/ingredients">
            <md-icon>local_drink</md-icon>
            <span class="md-list-item-text">Ingredients list</span>
          </md-list-item>
          <md-list-item to="/search">
            <md-icon>search</md-icon>
            <span class="md-list-item-text">Search</span>
          </md-list-item>
          <md-list-item to="/favorite">
            <md-icon>star</md-icon>
            <span class="md-list-item-text">Saved</span>
          </md-list-item>
          <md-list-item v-if="!isLoggedin" to="/login">
            <md-icon>login</md-icon>
            <span class="md-list-item-text">Login</span>
          </md-list-item>
          <md-list-item v-if="isLoggedin" v-on:click="logout">
            <md-icon>logout</md-icon>
            <span class="md-list-item-text">Logout</span>
          </md-list-item>
        </md-list>
      </md-app-drawer>

      <md-app-content>
        <router-view></router-view>
      </md-app-content>
    </md-app>
  </div>
</template>

<style lang="scss" scoped>
.md-app {
  max-height: 1200px;
  border: 1px solid rgba(#000, 0.12);
}

// Demo purposes only
.md-drawer {
  width: 230px;
  max-width: calc(100vw - 125px);
}
</style>

<script>
import firebase from "firebase/app";

export default {
  name: "Reveal",
  data: () => ({
    menuVisible: false,
    isLoggedin: false,
    currentuser: false,
    searchinput: "",
  }),
  created() {
    if (firebase.auth().currentUser) {
      this.isLoggedin = true;
      this.currentUser = firebase.auth().currentUser.email;
    }
  },
  methods: {
    toggleMenu() {
      this.menuVisible = !this.menuVisible;
    },
    logout: function () {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.$confirm("Are you sore you want to logout?", "Logout").then(
            () => {
              this.$router.push("/login");
            },

            (err) => {
              this.$router.push("/");
            }
          );
        });
    },
  },
};
</script>