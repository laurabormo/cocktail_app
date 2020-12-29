<template>
  <div>
    <md-list>
      <div v-for="ingredient in ingredients" :key="ingredient.strIngredient1">
        <md-list-item :to="'/ingredient/' + ingredient.strIngredient1">
          <span class="md-list-item-text">{{ ingredient.strIngredient1 }}</span>
       <md-icon>keyboard_arrow_right</md-icon>
        </md-list-item>
        <md-divider></md-divider>
      </div>
    </md-list>
  </div>
</template>

<script>
import DataService from "../dataservice";
export default {
  name: "ingredient",
  data() {
    return {
      ingredients: [],
    };
  },
  created: function () {
    DataService.getIngredients().then((data) => {
      
      this.ingredients = data.data.drinks;
    });
  },
};
</script>

<style>
</style>