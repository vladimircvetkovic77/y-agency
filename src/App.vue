<template>
  <PlantCalculator
    @calculate="(value) => plantCalculator(value, 1)"
    :error="error.errorCalculator1"
  >
    <template #result>
      <div
        v-if="result.calculator1"
        class="calculator__result"
      >
        <div class="result__title">Ihr Ergebnis:</div>
        <div class="result__description">
          Für Ihren Gartenabschnitt benötigen Sie
          <span style="font-size: 2rem; font-weight: 700;">{{result.calculator1}}</span>
          <span style="font-size: 1.5rem; font-weight: 700;"> x {{ product.name }}</span>
          <br>
          (das entspricht insgesamt {{ result.calculator1 * product.plant_in_package }} Heckenpflanzen)
        </div>
      </div>
    </template>
  </PlantCalculator>
  <PlantCalculator
    @calculate="(value) => plantCalculator(value, 2)"
    :error="error.errorCalculator2"
  >
    <template #result>
      <div
        v-if="result.calculator2"
        class="calculator__result"
      >
        <div class="result__title">Ihr Ergebnis:</div>
        <div class="result__description">
          Für Ihre geplante Hecke benötigen Sie
          <span style="font-size: 2rem; font-weight: 700;">{{result.calculator2}} </span>
          <span style="font-size: 1.5rem; font-weight: 700;"> Pflanzen </span>
          der Sorte {{ product.sorte }}
        </div>
      </div>
    </template>
  </PlantCalculator>
</template>

<script>
import PlantCalculator from "./components/PlantCalculator.vue";
import { reactive } from "vue";
export default {
  name: "App",
  components: {
    PlantCalculator,
  },
  setup() {
    let error = reactive({
      errorCalculator1: "",
      errorCalculator2: "",
    });

    let result = reactive({
      calculator1: "",
      calculator2: "",
    });

    const product = {
      name: "Hainbuche, ca. 62 x 61 x 113 cm",
      sorte: "HYZ Hainbuche",
      planting_distance: 20,
      plant_in_package: 3,
    };
    function plantCalculator(value, calculator) {
      error[`errorCalculator${calculator}`] = "";
      const regexTwoDecimalNumber = /^\d+([.,]\d{1,2})?$/;
      if (regexTwoDecimalNumber.test(value)) {
        if (value.includes(",")) {
          value = parseFloat(value.replace(",", "."));
        }
        if (calculator === 1) {
          result.calculator1 = Math.round(
            value / (product.planting_distance / 100) / product.plant_in_package
          );
        }
        if (calculator === 2) {
          result.calculator2 = Math.ceil(
            value / (product.planting_distance / 100)
          );
        }
      } else {
        error[`errorCalculator${calculator}`] =
          "*Bitte geben Sie eine Zahl ein.";
        result[`calculator${calculator}`] = "";
      }
    }
    return {
      plantCalculator,
      error,
      result,
      product,
    };
  },
};
</script>

<style>
#app {
  max-width: 80rem;
  margin: auto;
}
html {
  font-size: 14px;
}
.calculator__result {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  margin-top: 2.5rem;
}
.result__title {
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 1rem;
}
.result__description {
  font-size: 1rem;
}
</style>
