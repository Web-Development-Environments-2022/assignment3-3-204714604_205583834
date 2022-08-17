<template>
  <div class="container">
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
              <li v-if="recipe.isClicked"><p><strong>Watched Before:</strong>&#x2763;</p></li>
              <li v-if="!recipe.isClicked"><p><strong>Watched Before:</strong>&#x2763;</p></li>   
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
                <li>
                    300 g (10 oz) plain flour
                </li>
                <li>
                    100 g (3½ oz) butter
                </li>
                <li>
                    1 tsp salt
                </li>
                <li>
                    Honey or date syrup
                </li>
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
            <ol>
                <li>
                    Pour 500 ml (16 fl oz) of water into a large pan. Add the salt and 25 g (1 oz) of the butter. Bring gently to the boil. Once it comes to the boil remove from the heat.
                </li>
                    Sieve the flour and add it to the pan. With a wooden spoon, work the dough until it becomes smooth and free of lumps. It should reach a stage where it is no longer sticky and has the consistency of plasticene.
                <li>
                    Add 250 ml ( 8 fl oz) of water to the pan and bring it gently to the boil. Break the dough up a little and cook gently for 15-20 minutes stirring occasionally.
                </li>
                <li>
                    If all the water has not been absorbed after 20 minutes simply pour off any excess and cook for a few more minutes until there is no sign of any water.
                </li>
                <li>
                    Work the dough once more with a wooden spoon until it is smooth. This time it will stay sticky!
                </li>
                <li>
                    Melt the remaing butter and put a tbsp or two on a plate. Spread it around them place the sticky dough on top.
                </li>
                <li>
                    Fold the edge of the dough from the bottom to the top, turning the plate as you do so. The dough will lose all its stickiness. Once the dough is roughly circular, turn it over and smooth it with your hands.
                </li>
                <li>
                    Create a depression in the middle of the dough. Drizzle butter into the depression and over the aseeda. Finally drizzle some honey or date syrup around the outside.
                </li>
            </ol>
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
    <b-row height="100px">
    </b-row>
  </b-col>
  </b-row>
    </b-container>

    <p>{{recipe}}</p>
    <div v-if="recipe">
      <div class="recipe-header mt-3 mb-4">
        <h1>{{ recipe.title }}</h1>
        <img :src="recipe.image" class="center" />
      </div>
      <div class="recipe-body">
        <div class="wrapper">
          <div class="wrapped">
            <div class="mb-3">
              <div>Ready in {{ recipe.readyInMinutes }} minutes</div>
              <div>Likes: {{ recipe.aggregateLikes }} likes</div>
            </div>
            Ingredients:
            <ul>
              <li
                v-for="(r, index) in recipe.extendedIngredients"
                :key="index + '_' + r.id"
              >
                {{ r.original }}
              </li>
            </ul>
          </div>
          <div class="wrapped">
            Instructions:
            <ol>
              <li v-for="s in recipe._instructions" :key="s.number">
                {{ s.step }}
              </li>
            </ol>
          </div>
        </div>
      </div>
      <!-- <pre>
      {{ $route.params }}
      {{ recipe }}
    </pre
      > -->
    </div>
  </div>
</template>

<script>
export default {
  name:'recipe',
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
      // response = this.$route.params.response;
      try {
        response = await this.axios.get(
          // "https://test-for-3-2.herokuapp.com/recipes/info",
          // this.$root.store.server_domain + "/recipeExtendedInfo",
              this.$root.store.server_domain +"/recipes"+ "/recipeExtendedInfo/"+this.$route.params.recipeId+"/"+this.$root.store.username
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
