<template>
  <div class="calculator__container">
    <div class="calculator__title"> {{ title }} </div>
    <div class="calculator__body">
      <div class="calculator__body left">
        <div class="calculator__description">{{ calculatorDescription }}</div>
        <div class="calculator__content">
          <div class="content__title"><label>{{ inputLabel }}</label></div>
          <div class="content__input">
            <input v-model="input" />
            <button @click="calculate">{{ buttonText }}</button>
          </div>
          <div
            v-if="error"
            class="content__error"
          >{{ error }}</div>
          <div class="content__description">{{ inputDescription }}</div>
        </div>
        <slot name="result"></slot>
      </div>
      <div class="calculator__body right">BILD</div>
    </div>
  </div>
</template>
<script>
import { ref } from "vue";
export default {
  name: "PlantCalculator",
  props: {
    title: {
      type: String,
      default: "Hecken-Rechner: Ratzfatz zum Ergebnis",
    },
    inputLabel: {
      type: String,
      default: "Länge in m",
    },
    error: {
      type: String,
      default: "",
    },
    resultTitle: {
      type: String,
      default: "Ihr Ergebnis:",
    },
    calculatorDescription: {
      type: String,
      default:
        "Unser neuer Heckenrechner Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. Atvero os et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lore ipsum dolor sit amet.",
    },
    inputDescription: {
      type: String,
      default:
        "*Bitte tragen Sie hier die ipsum dolor sit amet, consetetur sadipscing elitr.",
    },
    buttonText: {
      type: String,
      default: "Jetzt berechnen",
    },
  },
  setup(props, context) {
    let input = ref("");
    function calculate() {
      context.emit("calculate", input.value);
    }

    return {
      input,
      calculate,
    };
  },
};
</script>
<style scoped>
.calculator__container {
  font-family: OpenSans, PTSans, Helvetica, Arial, sans-serif;
  font-size: 1rem;
  line-height: 1.4rem;
  color: #000000;
  width: 100%;
}

.calculator__title {
  width: 100%;
  padding: 1.5rem 0;
  font-size: 1.5rem;
  font-weight: 700;
  text-align: center;
}
.calculator__body {
  width: 100%;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  padding-right: 1rem;
}
.calculator__body.left {
  width: 70%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: space-between;
}
.calculator__body.right {
  width: 30%;
  height: 336px;
  width: 336px;
  background: lightgray;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3rem;
  color: darkgrey;
}
.calculator__description {
  width: 100%;
  line-height: 1.4;
  font-size: 1rem;
}
.calculator__content {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  margin-top: 1rem;
}
.content__title {
  font-weight: 700;
}
.content__title label {
  margin-bottom: 0.25rem;
}
.content__title label::after {
  content: " *";
  font-size: 1.3rem;
}
.content__input {
  width: 100%;
}
.content__input input {
  height: 2.5rem;
  line-height: 1.5rem;
  padding: 0 0.5rem 0 0.75rem;
  border: 1px solid transparent;
  background-color: #f0ece7;
  font-size: 0.875rem;
  width: 40%;
  box-sizing: border-box;
  margin-right: 1rem;
}
.content__input input:focus {
  border: 1px solid black;
  background-color: white;
  outline: none;
}
.content__input button {
  height: 2.5rem;
  vertical-align: middle;
  padding: 0.5rem 1rem;
  color: #fff;
  background-color: #005932;
  font-size: 1rem;
  font-weight: 700;
  line-height: 1.5;
  border: 0;
  border-radius: 2px;
  cursor: pointer;
  box-sizing: border-box;
}
.content__error {
  color: #be122b;
  margin-top: 0.25rem;
}
.content__description {
  margin-top: 1rem;
}
</style>
