<template>
    <div>
        <b-container>
            <b-row>
                <p>{{recipe.title}}</p>
            </b-row>
            <b-col>
                    <b-row>
                        <img v-if="image_load&&recipe.vegan" src="../images/veganSymbol.jpg" class="icon" cols="2"/>
                    </b-row>
                    <b-row>
                        <img v-if="image_load&&recipe.vegetarian" src="../images/vegeterian_symbol.jpg" class="icon" cols="2" />
                    </b-row>
                    <b-row>
                        <img v-if="image_load&&recipe.isClicked" src="../images/watchedSymbol.png" class="icon" cols="2"/>
                    </b-row>
                    <b-row>
                        <img v-if="image_load&&recipe.glutenFree" src="../images/gluten_free_image.png" class="icon" cols="2">
                    </b-row>
                    <b-row>
                        <img v-if="image_load&&!recipe.isFavorite" src="../images/before_favorite.jpg" class="icon"  @click="makeFavorite" cols="2" />
                    </b-row>
                    <b-row>
                        <img v-if="image_load&&recipe.isFavorite" src="../images/after_favorite.png" class="icon"/>
                    </b-row>
            </b-col>

            <b-row>
            <b-col cols="6">
                <b-row>
                    <p>Preparation Time:{{recipe.readyInMinutes}}</p>
                </b-row>
                <b-row>
                    <p>Likes:{{recipe.popularity}}</p>
                </b-row>
                <!-- <b-row>
                    <b-col>
                        <img v-if="image_load&&recipe.vegan" src="../images/veganSymbol.jpg" class="icon" cols="2"/>
                    </b-col>
                    <b-col>
                        <img v-if="image_load&&recipe.vegetarian" src="../images/vegeterian_symbol.jpg" class="icon" cols="2" />
                    </b-col>
                    <b-col>
                        <img v-if="image_load&&recipe.isClicked" src="../images/watchedSymbol.png" class="icon" cols="2"/>
                    </b-col>
                    <b-col>
                        <img v-if="image_load&&recipe.glutenFree" src="../images/gluten_free_image.png" class="icon" cols="2">
                    </b-col>
                    <b-col>
                        <img v-if="image_load&&!recipe.isFavorite" src="../images/before_favorite.jpg" class="icon"  @click="makeFavorite" cols="2" />
                    </b-col>
                    <b-col>
                        <img v-if="image_load&&recipe.isFavorite" src="../images/after_favorite.png" class="icon"/>
                    </b-col>
                </b-row> -->
            </b-col>
            <b-col cols="4">
            <router-link
              :to="{ name: 'recipe', params: { recipeId: recipe.id } }"
              class="recipe-preview">
              <img v-if="image_load" :src="recipe.image" class="recipe-image" width="100%" @click="makeWatched"/>
            </router-link>  
            </b-col>
            </b-row>
        </b-container>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                image_load:false
            }
                },
         mounted() {
            this.axios.get(this.recipe.image).then((i) => {
            this.image_load = true;
            });
         },
        props:{
            recipe: {
                type: Object,
                required: true
            },
            username:{
                type:String,
                required:true
            }


        }
    }
</script>

<style>

</style>