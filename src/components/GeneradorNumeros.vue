<template>
  <div class="generador-loteria">
    <h1>Generador de Números de Lotería</h1>
    <div>
      <label for="cantidad-numeros">Cantidad de Números (máx 20):</label>
      <input
        v-model.number="numberCount"
        type="number"
        id="cantidad-numeros"
        min="1"
        :max="maxNumbers"
        @input="validateInput"
      />
    </div>
    <div>
      <label for="numero-maximo">Número Máximo (1-50):</label>
      <input
        v-model.number="maxNumber"
        type="number"
        id="numero-maximo"
        min="1"
        :max="maxNumberTotal"
        @input="validateInputTotal"
      />
    </div>
    <button @click="generateNumbers">Generar</button>
    <div v-if="generatedNumbers.length">
      <h2>Números Generados:</h2>
      <div class="display-numeros">
        <span
          v-for="(number, index) in sortedNumbers"
          :key="index"
          class="item-numero"
        >
          {{ number }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      numberCount: 14, // Valor por defecto establecido en 14
      maxNumber: 25, // Valor por defecto establecido en 25
      maxNumbers: 20,
      maxNumberTotal: 50, // Valor por defecto establecido en 50
      generatedNumbers: [],
    };
  },
  computed: {
    sortedNumbers() {
      return [...this.generatedNumbers].sort((a, b) => a - b);
    },
  },
  methods: {
    validateInput() {
      if (this.numberCount > this.maxNumbers) {
        this.numberCount = this.maxNumbers;
      } else if (this.numberCount < 1) {
        this.numberCount = 1;
      }
    },
    validateInputTotal() {
      if (this.maxNumber > this.maxNumberTotal) {
        this.maxNumber = this.maxNumberTotal;
      } else if (this.maxNumber < 1) {
        this.maxNumber = 1;
      }
    },
    generateNumbers() {
      this.generatedNumbers = [];
      const numbersSet = new Set();

      while (numbersSet.size < this.numberCount) {
        const randomNumber = Math.floor(Math.random() * this.maxNumber) + 1;
        numbersSet.add(randomNumber);
      }

      this.generatedNumbers = Array.from(numbersSet);
    },
  },
};
</script>

<style scoped>
.generador-loteria {
  margin: 20px;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

label {
  margin-right: 10px;
  font-weight: bold;
  color: #333;
}

input {
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  margin-top: 10px;
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #45a049;
}

.display-numeros {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 20px;
}

.item-numero {
  background-color: #4CAF50;
  color: white;
  border: 1px solid #ccc;
  border-radius: 50%;
  padding: 10px;
  margin: 5px;
  width: 40px;
  height: 40px;
  font-size: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-weight: bold;
}
</style>
