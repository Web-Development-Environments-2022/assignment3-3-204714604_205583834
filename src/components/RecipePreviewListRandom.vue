<template>
    <b-container>
        <b-row v-for="recipe in recipes" :key="recipe.id">
            <RecipePreviewRandom :recipe="recipe" class="recipePrev"></RecipePreviewRandom>
        </b-row>
    </b-container>
</template>
<script>
import RecipePreviewRandom from "./RecipePreviewRandom.vue";
import RecipePreviewSearch from "./RecipePreviewSearch.vue";
export default {
  name: "RecipePreviewListRandom",
  components: {
    RecipePreviewRandom
},
//   data(){
//     return{
//         recipes:[]
//     };
//   },
  props:{
    recipes:Array
    }
  }


</script>