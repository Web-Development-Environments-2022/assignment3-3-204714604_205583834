
<template>
  <div class="container">
    <h1 class="title">Search Page</h1>
    <div>
      <b-form @submit.prevent="searchRecipes">
        <!--Cover Image Section-->
        <b-row>
          <b-col>
            <b-row class="section" id="coverImgSection">
              <img src="../images/cover_search_image.webp" id="coverSearchImg">
            </b-row>
          </b-col>
          <b-col class="user-side">
            <h1>Last Search</h1>
            <p><span class="last-search-headings">Search Query: </span>{{lastSearch}}</p>
            <p><span class="last-search-headings">Cusines: </span>{{lastCuisines}}</p>
            <p><span class="last-search-headings">Diets: </span>{{lastDiets}}</p>
            <p><span class="last-search-headings">Intolerances: </span>{{lastIntols}}</p>
          </b-col>
        </b-row>

        <!--Query Section-->
        <b-row id="querySection" class="section">
          <b-input v-model="form.searchQuery" type="text" placeholder="Enter your query" id="queryInput" />
          <b-button type="submit" variant="primary" id="submitbtn">Search</b-button>
        </b-row>
        <!--Filters Section-->
        <b-row class="section" id="filtersSection">
            <b-dropdown text="Cuisines" class="dropdwn-filters">
              <b-dropdown-item-btn v-for="cuis in cuisinesData" :key="cuis" @click="updateFilterList('cuisines',cuis)">{{cuis}}</b-dropdown-item-btn>
            </b-dropdown>
            <b-dropdown text="Diets" class="dropdwn-filters">
              <b-dropdown-item-btn v-for="diet in dietsData" :key="diet" @click="updateFilterList('diets',diet)">{{diet}}</b-dropdown-item-btn>
            </b-dropdown>
            <b-dropdown text="intolerances" class="dropdwn-filters">
              <b-dropdown-item-btn v-for="intol in intolerancesData" :key="intol" @click="updateFilterList('intolerances',intol)">{{intol}}</b-dropdown-item-btn>
            </b-dropdown>
            <b-form-select :options="[5,10,15]" v-model="form.recipesNumber" class="recipesNumber"></b-form-select>
        </b-row>
      </b-form>
    </div>
    <div id="filters-wrapper" v-if="!searchbtnpressed">
    <b-row>
      <b-col>
        <b-row>
          <p>Cuisines:</p>
        </b-row>
        <b-row>
            <ul class="filters-ul">
              <li v-for="cuis in form.selectedCuisines" :key="cuis" class="filters-li">{{cuis}}</li>
            </ul>
        </b-row>
      </b-col>
      <b-col>
        <b-row>
          <p>Diets:</p>
        </b-row>
        <b-row>
            <ul class="filters-ul">
              <li v-for="diet in form.selectedDiets" :key="diet" class="filters-li">{{diet}}</li>
            </ul>
        </b-row>
      </b-col>
      <b-col>
        <b-row>
          <p class="">Intolerances:</p>
        </b-row>
        <b-row>
            <ul class="filters-ul">
              <li v-for="intol in form.selectedIntols" :key="intol" class="filters-li">{{intol}}</li>
            </ul>
        </b-row>
      </b-col>
    </b-row>
    </div>
    <b-row>
      <b-dropdown text="Sort Recipes " v-if="searchbtnpressed">
        <b-dropdown-item-btn @click="sortArrByKey(res,'preparation')">Sort By Preparation Time</b-dropdown-item-btn>
        <b-dropdown-item-btn @click="sortArrByKey(res,'aggregateLikes')">Sort By Popularity</b-dropdown-item-btn>

      </b-dropdown>
    </b-row>
    <b-row>
    <RecipePreviewListSearch class="recipeprev" :recipes="res"></RecipePreviewListSearch>
    </b-row>
  </div>
  
</template>

<script>
import diets from "../assets/diets";
import cuisines from "../assets/cuisines";
import intolerances from "../assets/intolerances";
import RecipePreviewListSearch from "../components/RecipePreviewListSearch.vue";

export default {
    name: "Search",
    data() {
        return {
            form: {
                searchQuery: "",
                recipesNumber: 5,
                selectedCuisines: [],
                selectedDiets: [],
                selectedIntols: []
            },
            cuisinesData: cuisines,
            dietsData: diets,
            intolerancesData: intolerances,
            searchbtnpressed:false,
            res: [],
            lastSearch:localStorage.lastSearchQuery,
            lastCuisines:localStorage.lastCuisines,
            lastDiets:localStorage.lastDiets,
            lastIntols:localStorage.lastIntols
        };
    },
    methods: {
        async searchRecipes() {
            // let url = "https://api.spoonacular.com/recipes/complexSearch?";
            let cuisinesString = this.getStringRep(this.form.selectedCuisines);
            let dietsString = this.getStringRep(this.form.selectedDiets);
            let intolsString = this.getStringRep(this.form.selectedIntols);
            localStorage.setItem("lastSearchQuery",this.form.searchQuery);
            localStorage.setItem("lastCuisines",cuisinesString);
            localStorage.setItem("lastDiets",dietsString);
            localStorage.setItem("lastIntols",intolsString)
            this.lastSearch=localStorage.lastSearchQuery
            this.lastCuisines=localStorage.lastCuisines;
            this.lastDiets=localStorage.lastDiets;
            this.lastIntols=localStorage.lastIntols;
            // url += "query=";
            // url += this.form.searchQuery;
            // url += "&number=";
            // url += this.form.recipesNumber;
            // url += "&cuisine=";
            // url += cuisinesString;
            // url += "&diet=";
            // url += dietsString;
            // url += "&intolerances=";
            // url += intolsString;
            let url="http://localhost:3000/recipes/search/";
            var cuisinesStringUrl=cuisinesString;
            var dietsStringUrl=dietsString;
            var intolsStringUrl=intolsString;

            if (cuisinesString==""){
              cuisinesStringUrl=null;
            }
            if (dietsString==""){
              dietsStringUrl=null;
            }
            if (intolsString==""){
              intolsStringUrl=null;
            }
            url=url+this.form.searchQuery+"/"+this.form.recipesNumber+"/"+cuisinesStringUrl+"/"+dietsStringUrl+"/"+intolsStringUrl
            this.res=await this.axios.get(url);
            this.res=this.res.data;
            // let response = await this.axios.get(url, {
            //     params: {
            //         apiKey: "1813b7edcb964e93aee04c4f4dcbdfc7"
            //     }
            // });
            // let results=response.data.results;
            // //this.res=results;
            // let nextUrl="https://api.spoonacular.com/recipes/";
            // let detailedRecipes=[];
            // for (let i=0;i<results.length;i++){
            //   let finalResponse = await this.axios.get(nextUrl+results[i].id+"/information", {
            //     params:{
            //         apiKey: " 1813b7edcb964e93aee04c4f4dcbdfc7"
                    
            //     }
            //   });
            //   detailedRecipes.push(finalResponse.data);
            // }
            // this.res=detailedRecipes
            this.searchbtnpressed=true;

            if (detailedRecipes.length==0){
              alert("No Recipes Were Found")
            }
            
        },
        getStringRep(lst) {
            let ret = "";
            for (let i = 0; i < lst.length; i++) {
                if (i > 0) {
                    ret += ",";
                }
                ret += lst[i];
            }
            return ret;
        },
        updateFilterList(type,item){
          var lst;
          if (type=="cuisines"){
            lst=this.form.selectedCuisines
          }
          else if (type=="diets"){
            lst=this.form.selectedDiets
          }
          else if(type=="intolerances"){
            lst=this.form.selectedIntols
          }
          if (!lst.includes(item)){
            lst.push(item);
          }
          else{
            let index=lst.indexOf(item);
            lst.splice(index,1);

          }
        },
        sortArrByKey(arr,key){
          if (key=='preparation'){
          const sorted = arr.sort((a, b) => a.readyInMinutes.localeCompare(b.readyInMinutes))
          }
          else{
          const sorted = arr.sort((a, b) => a.aggregateLikes.localeCompare(b.aggregateLikes))

          }


        }
    },
    components: {RecipePreviewListSearch }
}
</script>

<style>

#coverSearchImg{
  width: 35%;
}

#coverImgSection{
  justify-content: center;
}


.section{
  margin-bottom: 40px;

}

#queryInput{
      width: 60%;
      margin-right: 10px;
}

#limitNumberSelection{
      width: 5%;
}

#submitbtn{
  width: 15%;
}

.searchFiltersHeadings{
      justify-content:center;

}

#submitSection{
        justify-content:center;

}
.recipeprev{
  justify-content: space-around;
}

.dropdwn-filters{
  margin-left: 30px;
}
#filters-title-wrapper{
  justify-content: space-around;
}
.recipesNumber{
  width: 70px;
  margin-left: 30px;
}
.user-side{
  width: 20%;
}
.last-search-headings{
  font-weight: bold;

}
</style>