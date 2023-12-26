<template>
  <body>
<div id="app">
    
  <div class="bmi-calculator">
      <h1>BMI Calculator</h1>

      <div v-if="!result" class="input-section">
        <label for="height">Height (cm):</label>
        <input type="number" v-model="height" id="height" placeholder="Enter height">

        <label for="weight">Weight (kg):</label>
        <input type="number" v-model="weight" id="weight" placeholder="Enter weight" style="margin-bottom: 15px;">

        <button style=" border-radius: 8px;" @click="calculateBMI">Calculate BMI</button >
      </div>

      <div v-if="result" class="result-section">
        <p>Your BMI is: {{ bmi }}</p>
        <p class="category">{{ bmiCategory }}</p>
      </div>
    </div>
  </div>
</body>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      height: null,
      weight: null,
      result: false,
      bmi: null
    };
  },
  methods: {
    calculateBMI() {
      if (this.height && this.weight) {
        const heightInMeters = this.height / 100;
        const bmi = this.weight / (heightInMeters * heightInMeters);
        this.bmi = bmi.toFixed(2);
        this.result = true;
      } else {
        alert('Please enter both height and weight');
      }
    }
  },
  computed: {
    bmiCategory() {
      if (this.bmi < 18.5) {
        return 'Underweight';
      } else if (this.bmi >= 18.5 && this.bmi < 24.9) {
        return 'Normal weight';
      } else if (this.bmi >= 25 && this.bmi < 29.9) {
        return 'Overweight';
      } else {
        return 'Obese';
      }
    }
  }
};
</script>

<style>
html, body {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  min-height: 100%;
  background: linear-gradient(to bottom, #7FFFD4, #00CED1);
  color: #000;
}

#app {
  height: 100%;
  margin-top: 40px;
  padding-bottom: 80px;
}

.bmi-calculator {
  max-width: 400px;
  margin: 30px;
  margin-top:80px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.301);
  background-color: #fff;
}

h1 {
  color: #045455;
  font-size: 24px;
  margin-bottom: 20px;
  flex-direction: column;
}

.input-section {
  display: flex;
  flex-direction: column;
  align-items: center;
}

label {
  font-size: 14px;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 15px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  background-color: #007BFF;
  color: #fff;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 20px;
}

.result-section {
  margin-top: 20px;
  text-align: center;
}

.category {
  font-weight: bold;
  color: #28a745; /* Green for Normal weight */
}
</style>
