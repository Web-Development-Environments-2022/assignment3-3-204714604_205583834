<template>
    <div class="myFavoriteRecipes">
        <b-container>
            <div class="jumbotron">
                <h1 class="title">{{ this.$root.store.username }} Favorites Recipes</h1>
                <router-link v-if="!$root.store.username" to="/login" tag="button">You need to Login to vue this</router-link>
                {{ !$root.store.username }}

                <div v-if="userRecipesArray.length > 0">
                    <b-container>
                            <b-row v-for="r in userRecipesArray" :key="r.id">
                                <RecipePreviewSearch :username="$root.store.username" class="recipePreview" :recipe="r" />
                            </b-row>
                            
                    </b-container>
                </div>
                <div v-else>
                    Liked Recipes list is empty - No Liked Recipes                                                                   <!-- CHANGE -->
                </div>
            </div>
        </b-container>
    </div>
</template>

<script>
    import RecipePreview from "../components/RecipePreview";
import RecipePreviewSearch from "../components/RecipePreviewSearch.vue";
import RecipePreviewRandom from "../components/RecipePreviewRandom.vue";
import RecipeFavoritesVue from "../components/RecipeFavorites.vue";
    export default {
        components: {
    RecipePreviewSearch
},
        mounted(){
            this.getFavoriteRecipes()

        },
        data() {
            return {
                userRecipesArray: [],
            }
        },
        methods:{
            async getFavoriteRecipes(){
                let username=this.$root.store.username;
                if (username==null){
                    return
                }
                // let response=await this.axios.get("http://localhost:3000/users/getFavorites/"+this.$root.store.username);
                // this.userRecipesArray=response.data;
                this.userRecipesArray=[
    {
        "id": 511728,
        "title": "Pasta Margherita",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/511728-556x370.jpg",
        "popularity": 1,
        "vegan": false,
        "vegetarian": false,
        "glutenFree": false,
        "isClicked": true,
        "isFavorite": true
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
        "isClicked": true,
        "isFavorite": true
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
        "isClicked": true,
        "isFavorite": true
    },
    {
        "id": 653185,
        "title": "No-Bake Chocolate Peanut Butter Pie",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/653185-556x370.jpg",
        "popularity": 30,
        "vegan": false,
        "vegetarian": false,
        "glutenFree": true,
        "isClicked": true,
        "isFavorite": true
    },
    {
        "id": 654812,
        "title": "Pasta and Seafood",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/654812-556x370.jpg",
        "popularity": 1,
        "vegan": false,
        "vegetarian": false,
        "glutenFree": false,
        "isClicked": true,
        "isFavorite": true
    },
    {
        "id": 654857,
        "title": "Pasta On The Border",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/654857-556x370.jpg",
        "popularity": 1,
        "vegan": false,
        "vegetarian": false,
        "glutenFree": false,
        "isClicked": true,
        "isFavorite": true
    },
    {
        "id": 654883,
        "title": "Pasta Vegetable Soup",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/654883-556x370.jpg",
        "popularity": 1,
        "vegan": false,
        "vegetarian": false,
        "glutenFree": false,
        "isClicked": true,
        "isFavorite": true
    },
    {
        "id": 654936,
        "title": "Pasta with Raw Tomato & Lemon Infused Olive Oil",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/654936-556x370.jpg",
        "popularity": 8,
        "vegan": false,
        "vegetarian": true,
        "glutenFree": true,
        "isClicked": false,
        "isFavorite": true
    },
    {
        "id": 654950,
        "title": "Pasta With Shrimp",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/654950-556x370.jpg",
        "popularity": 1,
        "vegan": false,
        "vegetarian": false,
        "glutenFree": false,
        "isClicked": false,
        "isFavorite": true
    },
    {
        "id": 654959,
        "title": "Pasta With Tuna",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/654959-556x370.jpg",
        "popularity": 2,
        "vegan": false,
        "vegetarian": false,
        "glutenFree": false,
        "isClicked": true,
        "isFavorite": true
    },
    {
        "id": 656329,
        "title": "Pizza bites with pumpkin",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/656329-556x370.jpg",
        "popularity": 9,
        "vegan": false,
        "vegetarian": true,
        "glutenFree": true,
        "isClicked": true,
        "isFavorite": true
    },
    {
        "id": 716300,
        "title": "Plantain Pizza",
        "readyInMinutes": 45,
        "image": "https://spoonacular.com/recipeImages/716300-556x370.jpg",
        "popularity": 95,
        "vegan": false,
        "vegetarian": false,
        "glutenFree": false,
        "isClicked": false,
        "isFavorite": true
    }
]
            }

        },
        async created(){
            // try {
            //     const ResponseData = await this.axios.get(
            //         "http://localhost:3000/getFavorites/"+this.$root.store.username,
            //     );
            //     this.userRecipesArray = ResponseData.data;  
            // } catch (err) {
            //     console.log(err);
            // }
        }
    }
</script>

<style>
    .favoritesPageDiv{
        text-align: center;
        background-size: cover;
        /* background-image: url("../pictures/background.jpg"); */
    }
</style>