<template>
  <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
        <div class="modal-header">
        <slot name="header">default header</slot>
        </div>
        
            <b-modal
            id="modal-prevent-closing"
            ref="modal"
            @show="resetModal"
            @hidden="resetModal"
            @ok="handleOk"
            >
                <form ref="form" @submit.stop.prevent="handleSubmit">

                <!--------------------------------------------------------- Recipe Name --------------------------------------------------------->
                    <b-form-group
                        label="Recipe name:"
                        label-for="name-input"
                        invalid-feedback="name is required"
                        :state="nameState"
                        >
                        <b-form-input
                            v-model="name"
                            :state="nameState"
                            required
                        ></b-form-input>
                    </b-form-group>

                <!--------------------------------------------------------- Image --------------------------------------------------------->
                    <b-form-group
                        label="Recipe Image URL:"
                        label-for="image-input"
                        >
                        <b-form-input required></b-form-input>
                    </b-form-group>

                <!--------------------------------------------------------- Ingridients list and amounts --------------------------------------------------------->
                    <label for="exampleFormControlTextarea1">Ingredients list & Amounts:</label>
                    <textarea class="form-control" id="exampleFormControlTextarea1" rows="3"></textarea>
                    <br>

                <!--------------------------------------------------------- Dishes Number --------------------------------------------------------->
                    <b-form-group
                        label="Number of dishes:"
                        label-for="DishesNumber-input"
                        >
                        <b-form-input type="number" required></b-form-input>
                        </b-form-group>

                <!--------------------------------------------------------- Cooking Time --------------------------------------------------------->
                    <b-form-group
                        label="Cooking time:"
                        label-for="cookTime-input"
                        >
                        <b-form-input required></b-form-input>
                    </b-form-group>

                <!--------------------------------------------------------- Instructions --------------------------------------------------------->
                    <label for="exampleFormControlTextarea1">Instructions:</label>
                    <textarea class="form-control" id="exampleFormControlTextarea1" rows="3"></textarea>
                    <br>

                <!--------------------------------------------------------- Vegan/ Vegetarian/ Gluten Free --------------------------------------------------------->
                    <input class="form-check-input" type="checkbox" value="" id="Vegan">
                    <label class="form-check-label" for="Vegan">
                        Vegan
                    </label>
                    <br>
                    <input class="form-check-input" type="checkbox" value="" id="Vegetarian">
                    <label class="form-check-label" for="Vegetarian">
                        Vegetarian
                    </label>
                    <br>
                    <input class="form-check-input" type="checkbox" value="" id="Gluten Free">
                    <label class="form-check-label" for="Gluten Free">
                        Gluten Free
                    </label>

                </form>
            </b-modal>

          <div class="modal-footer">
            <slot name="footer">
              <button
                class="modal-submit-button"
                @click="$emit('close')"
              >Submit</button>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
    props: {
        show: Boolean
    },
    methods: {
        async addNewRecipe(){
            const response = await this.axios.post(
                    "http://localhost:3000" + "/routes/recipes.js",

                    {
                        username: this.form.user_id,
                        dishesNumber: this.form.DishesNumber,
                        instructions: this.form.instructions,
                        GlutenFree: this.form.GlutenFree,
                        RecipePicture: this.form.RecipePicture,
                        CookingTime: this.form.CookingTime,
                        Veganism: this.form.Veganism,
                        Vegeterian: this.form.Vegeterian,
                        RecipeName: this.form.RecipeName
                    }
                );
            }
        }
}
</script>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 700px;
  margin: 15px auto;
  padding: 10px 30px;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.modal-header h3 {
  color: #42b983;
}

.modal-submit-button {
  background-color: #42b983;
  font-size: 130%;
  border: 0px ;
}

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>