<template>
  <div id="search-component">
    <h4>Hero Search</h4>

    <input id="search-box" v-model="searchWord">

    <ul class="search-result">
      <div v-show="searchWord!=''">
        <router-link
          tag="li" v-for="hero in searchHeroes"
          :to="'/detail/' + hero.id">
          {{hero.name}}
        </router-link>
      </div>
    </ul>

  </div>

</template>

<script>
  export default {
    name: "HeroSearch",
    data() {
      return {
        searchWord: "",
      }
    },
    computed: {
      heroes() {
        return this.$store.getters.heroes;
      },
      searchHeroes: function () {
        return this.heroes.filter(function (hero) {
          return hero.name.toLowerCase().indexOf(this.searchWord) > -1;
        }.bind(this));
      },
      pushSearchMessage(searchWord) {
        this.$store.dispatch('pushSearchHeroesMessage', searchWord);
      },
      // searchHero() {
      //   const heroName = this.searchWord;
      //   this.$store.dispatch('searchHero', heroName);
      // }
    }
  }
</script>

<style scoped>

  /* HeroSearch private styles */
  .search-result li {
    border-bottom: 1px solid gray;
    border-left: 1px solid gray;
    border-right: 1px solid gray;
    width: 195px;
    height: 16px;
    padding: 5px;
    background-color: white;
    cursor: pointer;
    list-style-type: none;
    margin-left: 39px;
  }

  .search-result li:hover {
    background-color: #607D8B;
  }

  .search-result li a {
    color: #888;
    display: block;
    text-decoration: none;
  }

  .search-result li a:hover {
    color: white;
  }

  .search-result li a:active {
    color: white;
  }

  #search-box {
    width: 200px;
    height: 20px;
  }

  ul.search-result {
    margin-top: 0;
    padding-left: 0;
  }

  /*
  Copyright 2017-2018 Google Inc. All Rights Reserved.
  Use of this source code is governed by an MIT-style license that
  can be found in the LICENSE file at http://angular.io/license
  */

</style>
