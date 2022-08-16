<template>
  <div>
    <b-container class="recipes" v-if="general==true">
        <b-row >
            <b-col>
                <div class="card" style="width: 18rem;">
                    <img class="card-img-top" src="../images/asidaa.jpg" alt="Card image cap">
                    <div class="card-body">
                        <h5 class="card-title">Asida</h5>
                        <p class="card-text">The Asida is a traditional recipe of lybian people, and took from Snir's grandomther and made on special events such as Rosh Hashana and Passover</p>
                        <button class="btn btn-primary" v-b-toggle.collapse-1 @click="activateRecipe(1)" >Watch Asida Recipe</button>
                    </div>
                </div>
            </b-col>
            <b-col>
                <div class="card" style="width: 18rem;" >
                    <img class="card-img-top" src="../images/shnitzel.webp" alt="Card image cap" >
                    <div class="card-body">
                        <h5 class="card-title">Schnitzel</h5>
                        <p class="card-text">A popular dish throughout Israel, chicken schnitzel is a simple, budget-friendly dish to prepare. It is often served with French fries</p>
                        <button class="btn btn-primary" v-b-toggle.collapse-1 @click="activateRecipe(2)" >Watch Schnitzel Recipe</button>
                    </div>
                </div>
            </b-col>
            <b-col>
                <div class="card" style="width: 18rem;">
                    <img class="card-img-top" src="../images/hummus.jpg" alt="Card image cap">
                    <div class="card-body">
                        <h5 class="card-title">Hummus</h5>
                        <p class="card-text">Hummus made from cooked and smashed chickpeas, tahini, olive oil, garlic, lemon juice, and salt, is a great source of dietary fiber, vitamin B and protein. Hummus is also rumored to be an aphrodisiac.</p>
                        <button class="btn btn-primary" v-b-toggle.collapse-1 @click="activateRecipe(3)" >Watch Hummus Recipe</button>
                    </div>
                </div>
            </b-col>       
        </b-row>
    </b-container>
<b-container v-if="recipe1==true">
    <b-row>
        <b-col>


<div class="accordion" role="tablist">
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-1 variant="info">Origins of the Asida</b-button>
      </b-card-header>
      <b-collapse id="accordion-1" visible accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <p>
                Asida is a cooked staple food made from grains, commonly sorghum, red millet, or corn, as shown above. It is eaten with almost every meal, be it meats, stews, fish or vegetables. It is consumed similar to other staple diets such as rice or mashed potatoes.  To eat Asida, cut a piece using the Right hand, mold between the fingers, create a dip in the middle, scoop the stew and place into the mouth.
                The recipe of the Asida were taken from Snir's grandomther
            </p>
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
        <b-col>
                             <img class="card-img-top" src="../images/asidaa.jpg" alt="Card image cap">
   
        </b-col>
    </b-row>
</b-container>

<b-container v-if="recipe2==true">
    <b-row>
        <b-col>


<div class="accordion" role="tablist">
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-4 variant="info">Origins of the Shnitzel</b-button>
      </b-card-header>
      <b-collapse id="accordion-4" visible accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <p>
Chicken schnitzel is a popular and tasty treat served throughout Israel. Schnitzel is Austrian in origin; veal (known as Wiener Schnitzel) or pork were the traditional meats of choice. Fried schnitzel later found its way to Israel with European Jews. Like many other foods, Jews adapted this regional dish to suit their unique dietary kosher laws. This recipe given by Daniel's grandomther
            </p>
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-5 variant="info">Ingredients</b-button>
      </b-card-header>
      <b-collapse id="accordion-5" accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <ul>
                <li>
                    6 boneless, skinless chicken breasts
                </li>
                <li>
                    1 cup all-purpose flour

                </li>
                <li>
                    2 cups breadcrumbs
                </li>
                <li>
                    3 eggs
                </li>
                <li>
                    1 tablespoon Dijon mustard
                </li>
                <li>
                    1 tablespoon lemon zest
                </li>
                <li>
                    ⅓ cup sesame seeds
                </li>
                <li>
                    Kosher salt and pepper
                </li>
                <li>
                    Extra virgin olive oil for frying
                </li>
                <li>
                    Lemon wedges for garnish
                </li>
            </ul>
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-6 variant="info">Instructions</b-button>
      </b-card-header>
      <b-collapse id="accordion-6" accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <ol>
                <li>
                    Clean chicken breasts and rinse. Place between two layers of plastic wrap and hit with a mallet until 1/8th inch thickness. Have no mercy.
                </li>
                    Beat the eggs and stir in dijon mustard. Add lemon zest, sesame seeds salt and pepper to the breadcrumbs.
                <li>
                    Coat chicken breasts with flour completely and shake off excess. Dunk in the egg mixture, shake off excess. Finally the chicken goes into the breadcrumbs - make sure the chicken is completely and evenly covered.                
                </li>
                <li>
                    Bring oil in a frying pan to high heat. The oil should cover the schnitzel about halfway. Fry chicken on both sides until golden. Place on paper towels to soak up the leftover oil and serve with a lemon wedge.                
                </li>
                <li>
                    Work the dough once more with a wooden spoon until it is smooth. This time it will stay sticky!
                </li>

            </ol>
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
  </div>
    
        </b-col>
        <b-col>
                             <img class="card-img-top" src="../images/shnitzel.webp" alt="Card image cap">
   
        </b-col>
    </b-row>
</b-container>

<b-container v-if="recipe3==true">
    <b-row>
        <b-col>


<div class="accordion" role="tablist">
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-7 variant="info">Origins of the Shnitzel</b-button>
      </b-card-header>
      <b-collapse id="accordion-7" visible accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <p>
Hummus is a popular dish in the Middle East, North Africa, and the Mediterranean. Thankfully today, hummus is becoming more popular in the western world. Sabra, for example, is a well-known Middle Eastern-style food product company that produces over 14 different hummus flavors available in the US and Canada. This recipe were given by Daniel grandmother.            </p>
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-8 variant="info">Ingredients</b-button>
      </b-card-header>
      <b-collapse id="accordion-8" accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <ul>
                <li>
                    1 x 400 g tin of chickpeas
                </li>
                <li>
                    1 small clove of garlic
                </li>
                <li>
                    1 tablespoon tahini
                </li>
                <li>
                    1 lemon

                </li>
                <li>
                    extra virgin olive oil
                </li>
            </ul>
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-9 variant="info">Instructions</b-button>
      </b-card-header>
      <b-collapse id="accordion-9" accordion="my-accordion" role="tabpanel">
        <b-card-body>
          <b-card-text>
            <ol>
                <li>
                    Drain and tip the chickpeas into a food processor.
                </li>
                <li>
                    Peel and add the garlic, then add the tahini, a good squeeze of lemon juice and 1 tablespoon of oil.
                </li>
                <li>
                    Season with a pinch of sea salt, then pop the lid on and blitz.
                </li>
                <li>
                    Use a spatula to scrape the houmous down the sides of the bowl, then blitz again until smooth.
                </li>
                <li>
                    Have a taste and add more lemon juice or a splash of water to loosen, if needed, then transfer to a serving bowl.
                </li>
                <li>
                    Serve with sliced crunchy veg, such as carrots, cucumbers, radishes or peppers, and some warm flatbreads.
                </li>
            </ol>
          </b-card-text>
        </b-card-body>
      </b-collapse>
    </b-card>
  </div>
    
        </b-col>
        <b-col>
                             <img class="card-img-top" src="../images/hummus.jpg" alt="Card image cap">
   
        </b-col>
    </b-row>
</b-container>
    <b-container>
        <b-row>
            <b-col></b-col>
            <b-col>
                    <b-button v-if="general==false" @click="activateRecipe(4)" block class=" btn btn-danger">return</b-button>

            </b-col>
            <b-col></b-col>


        </b-row>
    </b-container>

        
  </div>
</template>

<script>
export default {
    data(){
        return{
            general:true,
            recipe1:false,
            recipe2:false,
            recipe3:false
        }
    },
    methods:{
        activateRecipe(recipeNumber){
            if (recipeNumber===1){
                this.general=false;
                this.recipe1=true;
                this.recipe2=false;
                this.recipe3=false;
            }
            else if(recipeNumber==2){
                this.general=false;
                this.recipe1=false;
                this.recipe2=true;
                this.recipe3=false; 
            }
            else if(recipeNumber==3){
                this.general=false;
                this.recipe1=false;
                this.recipe2=false;
                this.recipe3=true;     
            }
            else{
                this.general=true;
                this.recipe1=false;
                this.recipe2=false;
                this.recipe3=false;   
            }
        }
    }

}
</script>

<style>

</style>