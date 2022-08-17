<template>
  <div class="container">
        <b-card>
          <b-card-header>
            <h2>{{recipe.title}}</h2>
          </b-card-header>
          <b-card-body>
    <b-container>
      <b-row>
        <b-col>
    <div class="accordion" role="tablist">
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-1 variant="info">Technical details</b-button>
      </b-card-header>
      <b-collapse id="accordion-1" visible accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <ul>
              <li><p><strong>Preparation Time:</strong>{{recipe.readyInMinutes}}</p></li>
              <li><p><strong>Number Of Likes:</strong>{{recipe.popularity}}</p></li>
              <li v-if="recipe.glutenFree"><p><strong>Gluten-Free:</strong>&#x2705;</p></li>
              <li v-if="!recipe.glutenFree"><p><strong>Gluten-Free:</strong>&#x274C;</p></li>
              <li v-if="recipe.vegan"><p><strong>Vegan:</strong>&#x2705;</p></li>
              <li v-if="!recipe.vegan"><p><strong>Vegan:</strong>&#x274C;</p></li>
              <li v-if="recipe.vegetarian"><p><strong>Vegetarian:</strong>&#x2705;</p></li>
              <li v-if="!recipe.vegetarian"><p><strong>Vegetarian:</strong>&#x274C;</p></li>
              <li v-if="recipe.isClicked"><p><strong>Watched Before:</strong>&#x2705;</p></li>
              <li v-if="!recipe.isClicked"><p><strong>Watched Before:</strong>&#x274C;</p></li>
            </ul>
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-2 variant="info">Ingredients</b-button>
      </b-card-header>
      <b-collapse id="accordion-2" accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <ul>
              <li
                v-for="(r, index) in recipe.extendedIngredients"
                :key="index + '_' + r.id"
              ><strong>{{r.name}}:</strong> {{r.amount}} {{r.unit}}</li>
            </ul>
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-3 variant="info">Instructions</b-button>
      </b-card-header>
      <b-collapse id="accordion-3" accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            {{recipe.instructions}}
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
  </div>
  </b-col>
  <b-col cols="5" >
    <b-row>
    <img :src="recipe.image" class="recipe-image" width="100%"/>
    </b-row>
    <b-row>
      <b-col>
        <img src="../images/watchedSymbol.png">
      </b-col>
      <b-col v-if="!recipe.isFavorite">
        <img src="../images/before_favorite.jpg" @click="makeFavorite" width="100%">

      </b-col>
      <b-col   v-if="recipe.isFavorite">
        <img src="../images/after_favorite.png" width="100%">

      </b-col>
    </b-row>
  </b-col>
  </b-row>
    </b-container>
    </b-card-body>
    </b-card>

    <!-- <p>{{recipe}}</p> -->
    <!-- <div v-if="recipe"> --> 
      <!-- <div class="recipe-header mt-3 mb-4">
        <h1>{{ recipe.title }}</h1>
        <img :src="recipe.image" class="center" />
      </div> -->
      <!-- <div class="recipe-body"> -->
        <!-- <div class="wrapper"> -->
          <!-- <div class="wrapped">
            <div class="mb-3">
              <div>Ready in {{ recipe.readyInMinutes }} minutes</div>
              <div>Likes: {{ recipe.aggregateLikes }} likes</div>
            </div>
            Ingredients:
            <ul>
              
            </ul>
          </div> -->
          <!-- <div class="wrapped">
            Instructions:
            <ol>
              <li v-for="s in recipe._instructions" :key="s.number">
                {{ s.step }}
              </li>
            </ol>
          </div> -->
        <!-- </div> -->
      <!-- </div> -->
      <!-- <pre>
      {{ $route.params }}
      {{ recipe }}
    </pre
      > -->
    <!-- </div> -->
  </div>
</template>

<script>
export default {
  name:'recipe',
  methods:{
                async makeFavorite(){
            let url="http://127.0.0.1:3000/users/favorites";
            if (!this.isFavorite){
              const response=await this.axios.post(url,{
              recipeId:this.recipe.id,
              username:this.$root.store.username
            });
              this.isFavorite=true;
              }
              
            }
  },
  mounted() {
    this.axios.get(this.recipe.image).then((i) => {
    this.image_load = true;
    });
  },
  data() {
    return {
      recipe: null,
      image_load: false,

    };
  },
  async created() {
    try {
      let response;
      let temp=this.$root.store.username;
      if (temp==undefined){
        temp="null";
      }
      // response = this.$route.params.response;
      try {
        response = await this.axios.get(
          // "https://test-for-3-2.herokuapp.com/recipes/info",
          // this.$root.store.server_domain + "/recipeExtendedInfo",
              this.$root.store.server_domain +"/recipes"+ "/recipeExtendedInfo/"+this.$route.params.recipeId+"/"+temp
              // ,
          // {
          //   params: { id: this.$route.params.recipeId,
          //             user_id:this.$root.store.username
          //              }
          // }
        );
        this.recipe=response.data
        // console.log("response.status", response.status);
        if (response.status !== 200) this.$router.replace("/NotFound");
      } catch (error) {
        console.log("error.response.status", error.response.status);
        this.$router.replace("/NotFound");
        return;
      }

      let {
        analyzedInstructions,
        instructions,
        extendedIngredients,
        aggregateLikes,
        readyInMinutes,
        image,
        title
      } = response.data.recipe;

      let _instructions = analyzedInstructions
        .map((fstep) => {
          fstep.steps[0].step = fstep.name + fstep.steps[0].step;
          return fstep.steps;
        })
        .reduce((a, b) => [...a, ...b], []);

      let _recipe = {
        instructions,
        _instructions,
        analyzedInstructions,
        extendedIngredients,
        aggregateLikes,
        readyInMinutes,
        image,
        title
      };

      // this.recipe = _recipe;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style scoped>
.wrapper {
  display: flex;
}
.wrapped {
  width: 50%;
}
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
/* .recipe-header{

} */
</style>
