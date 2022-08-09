<template>

    <div class="recipe-body">
      <b-container class="recipebody">
        <b-row>
          <b-col>
            <h4>{{recipe.title}}</h4>
            <p>Preparation Time: {{recipe.readyInMinutes}} minutes</p>
            <p>Number Of Likes: {{recipe.aggregateLikes}}</p>
              <ul class="icon_wrapper_new">
                <li><img v-if="image_load&&recipe.vegan" src="../images/veganSymbol.jpg" class="icon" /></li>
                <li><img v-if="image_load&&recipe.vegetarian" src="../images/vegeterian_symbol.jpg" class="icon" /></li>
                <li><img v-if="image_load&&isWatched" src="../images/watchedSymbol.png" class="icon" /></li>
                <li><img v-if="image_load&&!isFavorite" src="../images/before_favorite.jpg" class="icon"  @click="makeFavorite" /></li>
                <li><img v-if="image_load&&isFavorite" src="../images/after_favorite.png" class="icon" /></li>
              </ul>   
          </b-col>
          <b-col>
            <router-link
              :to="{ name: 'recipe', params: { recipeId: recipe.id } }"
              class="recipe-preview">
              <img v-if="image_load" :src="recipe.image" class="recipe-image" />
            </router-link>         
          </b-col>

        </b-row>

      </b-container>
    </div>

</template>

<script>
    export default {
        mounted() {
            this.axios.get(this.recipe.image).then((i) => {
            this.image_load = true;
            });
        },
        data() {
            return {
            image_load: false,
            isWatched:false,
            isFavorite:false
            };
        },
        props: {
            recipe: {
            type: Object,
            required: true
            }
        },
        methods:{
          //add to the DB
          makeFavorite(){
            this.isFavorite=true;
          }
        } 
    }

</script>

<style>
.icon_wrapper{
  display: flex;
  flex-direction: row;
}
.icon{
  height: 50px;
  text-decoration: none;
  margin-right: 30px;
}
ul{
      list-style-type: none;

}
.recipe-image{
  height:60%
}



.icon_wrapper_new{
    display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.recipeprevright{
      flex: 1;
    border: 2px solid yellow;
        width: 40%

}

.recipeprevleft{
      flex: 1;
    border: 2px solid yellow;
    margin-right: 20px;
    width: 40%

}

.recipebody{
  height: 250px;
  margin-bottom: 50px;
  padding: 15px;
  

}


</style>