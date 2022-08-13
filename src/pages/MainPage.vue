<template>
  <div class="container">

    <!-- <h1 class="title">Main Page</h1> -->
    <!-- <RecipePreviewList title="Randome Recipes" class="RandomRecipes center" />
    <router-link v-if="!$root.store.username" to="/login" tag="button">You need to Login to vue this</router-link>
   {{ !$root.store.username }} -->
    <!-- <RecipePreviewList
      title="Last Viewed Recipes"
      :class="{
        RandomRecipes: true,
        blur: !$root.store.username,
        center: true
      }"
      disabled -->
      <!-- </RecipePreviewList> -->
    <b-container>      
      <b-row>
        <b-col cols="4">
          <b-row>
            <h2>Explore this recipes</h2>
          </b-row>
          <b-row>
            <RecipePreviewListRandom :recipes="this.randomRecipes"></RecipePreviewListRandom>
          </b-row>
          <b-row>
            <b-button @click="generateRandom">Generate new Recipes</b-button>
          </b-row>
        </b-col>
        <b-col v-if="$root.store.username" cols="4"></b-col>
        <b-col v-if="$root.store.username" cols="4">
          <b-row>
            <h2>Last watched recipes</h2>
          </b-row>
          <b-row>
            <RecipePreviewListRandom :recipes="this.randomRecipes" class="col"></RecipePreviewListRandom>
          </b-row>
        </b-col>
        <b-col cols="3" v-if="!$root.store.username"></b-col>
        <b-col v-if="!$root.store.username" cols="3">
          <b-form @submit.prevent="loginUser">
            <b-row>
              <h1>Sign In</h1>
            </b-row>
            <b-row>
              <p>Username:</p>
            </b-row>
            <b-row>
              <b-input placeholder="Enter user" v-model="form.username"/>
            </b-row>
            <b-row>
              <p>Password:</p>
            </b-row>
            <b-row>
              <b-input placeholder="Enter password" type="password" v-model="form.password"/>
            </b-row>
            <b-row>
              <b-col>
                <b-button type="submit">Login</b-button>
              </b-col>
              <b-col>
                <b-button to="/register">Register</b-button>
              </b-col>  

            </b-row>
          </b-form>
          <b-row>
          </b-row>
        </b-col>
      </b-row>
      </b-container>

    
    <!-- <div
      style="position: absolute;top: 70%;left: 50%;transform: translate(-50%, -50%);"
    >
      Centeredasdasdad
    </div>-->
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
import RecipePreviewListRandom from '../components/RecipePreviewListRandom.vue';
export default {
  components: {
    // RecipePreviewList,
  
    RecipePreviewListRandom,
    
},
  data(){
    return{
      randomRecipes:[],
      form:{
        username:"",
        password:""
      }
    }
  },
  mounted(){
    this.randomRecipes=this.getRandomRecipes();
  },
  methods:{
    async generateRandom(){

    },
    async getLastWatched(){

    },
    async loginUser(){
      try{
          const response = await this.axios.post(
            "http://localhost:3000" + "/Login",
            {
              username: this.form.username,
              password: this.form.password
            }
          );
        this.$root.store.login(this.form.username);
        this.$router.push("/");
      }
       catch (err) {
        console.log(err.response);
        this.form.submitError = err.response.data.message;
      }

    },
    getRandomRecipes(){
      let url="http://localhost:3000/recipes/random"
      let randomRecipes=
      [
        {
            "id": 653185,
            "title": "No-Bake Chocolate Peanut Butter Pie",
            "readyInMinutes": 45,
            "image": "https://spoonacular.com/recipeImages/653185-556x370.jpg",
            "popularity": 30,
            "vegan": false,
            "vegetarian": false,
            "glutenFree": true,
            "isClicked": false,
            "isFavorite": false
        },
        {
            "id": 641958,
            "title": "Easy Eggplant Curry",
            "readyInMinutes": 45,
            "image": "https://spoonacular.com/recipeImages/641958-556x370.jpg",
            "popularity": 14,
            "vegan": true,
            "vegetarian": true,
            "glutenFree": true,
            "isClicked": false,
            "isFavorite": false
        },
        {
            "id": 651729,
            "title": "Grilled Lemon Garlic Artichokes",
            "readyInMinutes": 45,
            "image": "https://spoonacular.com/recipeImages/651729-556x370.jpg",
            "popularity": 9,
            "vegan": true,
            "vegetarian": true,
            "glutenFree": true,
            "isClicked": false,
            "isFavorite": false
        }
      ]
      
      return randomRecipes;

    }
  }

};
</script>

<style lang="scss" scoped>
.RandomRecipes {
  margin: 10px 0 10px;
}
.blur {
  -webkit-filter: blur(5px); /* Safari 6.0 - 9.0 */
  filter: blur(2px);
}
::v-deep .blur .recipe-preview {
  pointer-events: none;
  cursor: default;
}

</style>