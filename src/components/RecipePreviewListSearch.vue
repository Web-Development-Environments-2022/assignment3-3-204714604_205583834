<template>
    <b-container>
        <h3>Search Results</h3>
        <b-row v-for="recipe in recipes" :key="recipe.id">
            <RecipePreview :recipe="recipe" class="recipePrev"></RecipePreview>
        </b-row>
    </b-container>
</template>
<script>
import RecipePreview from "./RecipePreview.vue";
export default {
  name: "RecipePreviewList",
  components: {
    RecipePreview
  },
  props:{
    title:{
        type:String,
        required:true
    }
  },
//   data(){
//     return{
//         recipes:[]
//     };
//   },
  props:{
    recipes:[]
    }
  }


</script>