<template>

    <div class="recipe-body">
      <b-container class="recipebody">
        <!-- <b-row>
        <b-col cols="10">
          <b-row>
            <p>{{recipe.title}}</p>
          </b-row>
          <b-row>
            <p>Preparation Time: {{recipe.readyInMinutes}} minutes</p>
          </b-row>
          <b-row>
            <p>Number Of Likes: {{recipe.popularity}}</p>
          </b-row>
          <b-row>
            <router-link
              :to="{ name: 'recipe', params: { recipeId: recipe.id } }"
              class="recipe-preview">
              <img v-if="image_load" :src="recipe.image" class="recipe-image" width="100%"/>
            </router-link>  
          </b-row>
        </b-col>
        <b-col cols="1"></b-col>
        <b-col cols="1">
          <b-row>
            <img v-if="image_load&&recipe.vegan" src="../images/veganSymbol.jpg" class="icon" />
          </b-row>
          <b-row>
            <img v-if="image_load&&recipe.vegetarian" src="../images/vegeterian_symbol.jpg" class="icon" />
          </b-row>
          <b-row>
            <img v-if="image_load&&isWatched" src="../images/watchedSymbol.png" class="icon" />
          </b-row>
          <b-row>
            <img v-if="image_load&&recipe.glutenFree" src="../images/gluten_free_image.png" class="icon">
          </b-row>
          <b-row>
            <img v-if="image_load&&!isFavorite" src="../images/before_favorite.jpg" class="icon"  @click="makeFavorite" />
          </b-row>
          <b-row>
            <img v-if="image_load&&isFavorite" src="../images/after_favorite.png" class="icon" />
          </b-row> -->
        
        <!-- </b-col> -->
        <!-- </b-row> -->
        <b-row>
          <b-col cols="4">
            <b-row>
            <h4>{{recipe.title}}</h4>
            </b-row>
            <b-row>
            <p>Preparation Time: {{recipe.readyInMinutes}} minutes</p>
            </b-row>
            <b-row>
            <p>Number Of Likes: {{recipe.popularity}}</p>
            <b-row>
              <!-- {{JSON.stringify(recipe.instructions)}} -->
            </b-row>
            </b-row>
              <!-- <ul class="icon_wrapper_new">
                <li><img v-if="image_load&&recipe.vegan" src="../images/veganSymbol.jpg" class="icon" /></li>
                <li><img v-if="image_load&&recipe.glutenFree" src="../images/gluten_free_image.png" class="icon"></li>
                <li><img v-if="image_load&&recipe.vegetarian" src="../images/vegeterian_symbol.jpg" class="icon" /></li>
                <li><img v-if="image_load&&isWatched" src="../images/watchedSymbol.png" class="icon" /></li>
                <li><img v-if="image_load&&!isFavorite" src="../images/before_favorite.jpg" class="icon"  @click="makeFavorite" /></li>
                <li><img v-if="image_load&&isFavorite" src="../images/after_favorite.png" class="icon" /></li>
              </ul>    -->
              <b-row>
              <b-col>
                <img v-if="image_load&&recipe.vegan" src="../images/veganSymbol.jpg" class="icon" />
              </b-col>
              <b-col>
                <img v-if="image_load&&recipe.glutenFree" src="../images/gluten_free_image.png" class="icon" />
              </b-col>
              <b-col>
                <img v-if="image_load&&recipe.vegetarian" src="../images/vegeterian_symbol.jpg" class="icon" />
              </b-col>
                            <b-col>
                <img v-if="image_load&&isWatched" src="../images/watchedSymbol.png" class="icon" />
              </b-col>
                            <b-col>
                <img v-if="image_load&&!isFavorite" src="../images/before_favorite.jpg" class="icon" @click="makeFavorite" />
              </b-col>
                            <b-col>
                <img v-if="image_load&&isFavorite" src="../images/after_favorite.png" class="icon" />
              </b-col>
              </b-row>
          </b-col>
          <b-col cols="8">
            <router-link
              :to="{ name: 'recipe', params: { recipeId: recipe.id } }"
              class="recipe-preview">
              <img v-if="image_load" :src="recipe.image" class="recipe-image" @click="makeWatched" />
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
            });
            this.username=localStorage.getItem("username");
            this.checkWatched();
            this.checkFavorite();
            this.image_load = true;

        },
        data() {
            return {
            image_load: false,
            isWatched:false,
            isFavorite:false,
            username:"",
            res:""
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
          async makeFavorite(){
            if(this.username==null){
              return;
            }
            let url="http://127.0.0.1:3000/users/favorites";
            if (!this.isFavorite){
              const response=await this.axios.post(url,{
              recipeId:this.recipe.id,
              username:this.username
            });
              this.isFavorite=true;
              }
              
            },
          async makeWatched(){
            let url="http://127.0.0.1:3000/users/addWatched";
            if (!this.isWatched){
              const response=await this.axios.post(url,{
              recipe_id:this.recipe.id,
              username:this.username
            });
              this.isWatched=true;

              }
            },
          async checkWatched(){
            if(this.username==null){
              return;
            }
            let url="http://127.0.0.1:3000/users/getWatched/";
            url=url+this.username+'/'+this.recipe.id;
            let response=await this.axios.get(url);
            if (response.data){
              this.isWatched=true;
            }
            else{
              this.isWatched=false;
            }

            // for(let i=0;i<watchedRecipes.length;i++){
            //   if (this.recipe.id===watchedRecipes[i].id){
            //     this.isWatched=true;
            //   }
            // }

          },
          async checkFavorite(){
            if(this.username==null){
              return;
            }
            let url="http://127.0.0.1:3000/users/getFavorites/";
            url=url+this.username+'/'+this.recipe.id;
            let response=await this.axios.get(url);
            if (response.data){
              this.isFavorite=true;
            }
            else{
              this.isFavorite=false;
            }
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