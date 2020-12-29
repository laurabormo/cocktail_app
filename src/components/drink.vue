<template>
  <div class="md-layout">
    <md-card
      class="md-layout-item "
      v-for="drink in drinks"
      :key="drink.idDrink"
    >
      <md-card-header>
        <md-card-header-text>
          <span class="md-title">{{ drink.strDrink }}</span>
          <div id="ingredienti">
            <span class="md-subhead">Ingredients</span>
            <p>{{ drink.strMeasure1 }} {{ drink.strIngredient1 }}</p>
            <p>{{ drink.strMeasure2 }} {{ drink.strIngredient2 }}</p>
            <p>{{ drink.strMeasure3 }} {{ drink.strIngredient3 }}</p>
            <p>{{ drink.strMeasure4 }} {{ drink.strIngredient4 }}</p>
            <p>{{ drink.strMeasure5 }} {{ drink.strIngredient5 }}</p>
            <p>{{ drink.strMeasure6 }} {{ drink.strIngredient6 }}</p>
            <p>{{ drink.strMeasure7 }} {{ drink.strIngredient7 }}</p>
            <p>{{ drink.strMeasure8 }} {{ drink.strIngredient8 }}</p>
            <p>{{ drink.strMeasure9 }} {{ drink.strIngredient9 }}</p>
            <p>{{ drink.strMeasure10 }} {{ drink.strIngredient10 }}</p>
            <p>{{ drink.strMeasure11 }} {{ drink.strIngredient11 }}</p>
            <p>{{ drink.strMeasure12 }} {{ drink.strIngredient12 }}</p>
            <p>{{ drink.strMeasure13 }} {{ drink.strIngredient13 }}</p>
            <p>{{ drink.strMeasure14 }} {{ drink.strIngredient14 }}</p>
            <p>{{ drink.strMeasure15 }} {{ drink.strIngredient15 }}</p>
          </div>
        </md-card-header-text>
        <md-card-media md-big>
          <img :src="drink.strDrinkThumb" />
        </md-card-media>
      </md-card-header>
      <md-card-content>
        <md-card-expand>
          <md-card-actions md-alignment="space-between">
            <div>
              <md-button>Save</md-button>
            </div>
            <md-card-expand-trigger>
              <md-button>Learn more</md-button>
            </md-card-expand-trigger>
          </md-card-actions>
          <md-card-expand-content>
            <md-card-content>
              <div id="glass">
                <span class="md-title">Correct glass:</span>
              </div>
              <p>{{ drink.strGlass }}</p>
              <span class="md-title">How to do:</span>
              <p>{{ drink.strInstructions }}</p>
            </md-card-content>
          </md-card-expand-content>
        </md-card-expand>
      </md-card-content>
    </md-card>
  </div>
</template>

<script>
import DataService from "../dataservice";
export default {
  name: "specifiche",
  data() {
    return {
      drinks: [],
    };
  },
  created: function () {
    DataService.getDrink(this.$route.params.id).then((data) => {
      this.drinks = data.data.drinks;
    });
  },
};
</script>