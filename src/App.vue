<script setup lang="ts">
import { ref } from "vue";
import useDate from "./composables/useDate";

const daysToAdd = ref(0);
const monthsToAdd = ref(0);
const heading = ref("Current Date");

const { date, getDay, getMonth, getYear, addDay, addMonth } = useDate();
const dates = ref(date.toString());

const handleInputChange = (event: Event) => {
  let { name, value } = event.target as HTMLInputElement;
  if (name === "day") {
    if (!value) value = "0";
    daysToAdd.value = parseInt(value);
  } else if (name === "month") {
    if (!value) value = "0";
    monthsToAdd.value = parseInt(value);
  }
};

const handleAddDaysAndMonths = () => {
  const newDate = addMonth(monthsToAdd.value, addDay(daysToAdd.value, date));
  return newDate;
};

const handleClick = () => {
  heading.value = "Updated date:";
  dates.value = handleAddDaysAndMonths().toString();
};
</script>

<template>
  <div>
    <h2>{{ heading }}</h2>
    <p>Date: {{ dates }}</p>
    <br />
    Add Day: <input name="day" type="number" @change="handleInputChange" />
    <br />
    Add Month: <input name="month" type="number" @change="handleInputChange" />
    <br />
    <button class="change-btn" @click="handleClick">Change The World</button>
  </div>
</template>

<style scoped>
div {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f0f0f0;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.header {
  text-align: center;
  margin-bottom: 20px;
}

h2 {
  color: #27ae60;
}

input {
  padding: 8px;
  width: 60px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.change-btn {
  background-color: #27ae60;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
  transition: background-color 0.3s ease;
}

.change-btn:disabled {
  background-color: #95a5a6;
  cursor: not-allowed;
}

.success-message {
  color: #2ecc71;
  margin-top: 10px;
}
</style>
