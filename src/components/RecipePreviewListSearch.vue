<template>
    <b-container>
        <!-- <h3 v-if="recipes.length!=0">Search Results</h3> -->
        <b-row v-for="recipe in recipes" :key="recipe.id">
            
            <RecipePreviewSearch :recipe="recipe" class="recipePrev"></RecipePreviewSearch>
        </b-row>
    </b-container>
</template>
<script>
import RecipePreviewSearch from "./RecipePreviewSearch.vue";
export default {
  name: "RecipePreviewListSearch",
  components: {
    RecipePreviewSearch
},
//   data(){
//     return{
//         recipes:[]
//     };
//   },
  props:{
    recipes:Array,
    username:{
      type:String,
      required:false,
      default:""
      }
    }
  }


</script>