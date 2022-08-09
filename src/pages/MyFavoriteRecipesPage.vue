<template>
    <div class="myFavoriteRecipes">
        <b-container>
            <div class="jumbotron">
                <h1 class="title">{{ this.$root.store.username }} Favorites Recipes</h1>
                <router-link v-if="!$root.store.username" to="/login" tag="button">You need to Login to vue this</router-link>
                {{ !$root.store.username }}

                <div v-if="userRecipesArray.length > 0">
                    <b-container>
                        <b-col>
                            <b-col v-for="r in userRecipesArray" :key="r.id">
                                <RecipePreview class="recipePreview" :recipe="r" />
                            </b-col>
                        </b-col>
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
    export default {
        components: {
            RecipePreview
        },
        data() {
            return {
                userRecipesArray: [],
            }
        },
        async created(){
            try {
                const ResponseData = await this.axios.get(
                    "http://localhost:3000/getMyfavourite/"+this.$root.store.username,
                );
                this.userRecipesArray = ResponseData.data;  
            } catch (err) {
                console.log(err);
            }
        }
    }
</script>

<style>
    .favoritesPageDiv{
        text-align: center;
        background-size: cover;
        background-image: url("../pictures/background.jpg");
    }
</style>