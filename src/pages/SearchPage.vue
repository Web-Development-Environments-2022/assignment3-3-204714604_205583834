
<template>
  <div class="container">
    <h1 class="title">Search Page</h1>

    <div>
      <b-form @submit.prevent="searchForRecipes" @reset.prevent="resetfields">
        <b-row class="form_rows">
          <input v-model="form.searchQuery" type="text" placeholder="Enter your query" />
        </b-row>
        <b-row class="form_rows">
          <b-dropdown text="Cuisine?" class="drpdwn">
            <b-dropdown-item v-for="cuis in cuisinesData" :key="cuis">{{cuis}}</b-dropdown-item>
          </b-dropdown>
          <b-dropdown text="Diet?" class="drpdwn">
            <b-dropdown-item v-for="cuis in cuisinesData" :key="cuis">{{cuis}}</b-dropdown-item>
          </b-dropdown>

          <b-dropdown text="intolerance?" class="drpdwn">
            <b-dropdown-header>intolerance Preferences</b-dropdown-header>
            <b-dropdown-item @click="form.intolerance=true">Yes</b-dropdown-item>
            <b-dropdown-item @click="form.intolerance=false">No</b-dropdown-item>
          </b-dropdown>

        </b-row>
        <b-row>
          <b-button type="submit" variant="primary">Search</b-button>
        </b-row>
      </b-form>
    </div>
  </div>
</template>

<script>
import diets from "../assets/diets";
import cuisines from "../assets/cuisines";
import intolerances from "../assets/intolerances";
export default {
  name: "Search",
  data() {
    return {
      form: {
        searchQuery: "",
        recipesNumber: 5,
        cuisine: "",
        diet: "",
        intolerance: ""
      },
      cuisinesData: cuisines,
      dietsData: diets,
      intolerancesData: intolerances,
    }
  },
  methods: {
    async searchForRecipes() {
      let url = "https://api.spoonacular.com/recipes/complexSearch?";
      url += "query"
      url += form.query

      const response = await this.axios.post(
        url + "/" + this.form.cuisine

      )
    }



  }


}
</script>

<style>
.form_rows {
  padding-bottom: 20px;
}

.drpdwn {
  margin-left: 0px;
  margin-right: 10px;
}
</style>