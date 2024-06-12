<!--npm install chart.js  -->
<template>
  <div class="chart-container">
    <canvas ref="MyChart" />
  </div>
  <div class="income-expense-list">
    <div class="list-item" v-for="(item, index) in listItems" :key="index">
      <img :src="item.image" alt="icon" class="item-image" />
      <span class="item-name">{{ item.name }}</span>
      <span class="item-amount">{{ item.amount }}</span>
    </div>
  </div>

  
</template>

<script>
import { Chart, registerables } from "chart.js";
import ChartDataLabels from "chartjs-plugin-datalabels";
Chart.register(...registerables, ChartDataLabels);

export default {
  data: () => ({
    type: "doughnut",
    data: {
      labels: ["식비", "교통", "여가", "재테크", "고정", "기타"],
      datasets: [
        {
          label: "# of Votes",
          data: [12, 19, 3, 5, 2, 3],
          backgroundColor: [
            "rgba(255, 99, 132, 0.2)",
            "rgba(54, 162, 235, 0.2)",
            "rgba(255, 206, 86, 0.2)",
            "rgba(75, 192, 192, 0.2)",
            "rgba(153, 102, 255, 0.2)",
            "rgba(255, 159, 64, 0.2)",
          ],
          borderColor: [
            "rgba(255, 99, 132, 1)",
            "rgba(54, 162, 235, 1)",
            "rgba(255, 206, 86, 1)",
            "rgba(75, 192, 192, 1)",
            "rgba(153, 102, 255, 1)",
            "rgba(255, 159, 64, 1)",
          ],
          borderWidth: 1,
        },
      ],
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      layout: {
        padding: {
          top: 50,
          bottom: 50,
          left: 50,
          right: 50,
        },
      },
      plugins: {
        datalabels: {
          color: "#000",
          align: "end",
          anchor: "end",
          offset: 10,
          formatter: (value, context) => {
            return context.chart.data.labels[context.dataIndex];
          },
          font: {
            weight: "bold",
            size: 12,
          },
        },
      },
    },
    listItems: [
      { image: "./public/food.png", name: "식비", amount: "$1200" },
      { image: "path/to/image2.jpg", name: "교통", amount: "$1900" },
      { image: "path/to/image3.jpg", name: "여가", amount: "$300" },
      { image: "path/to/image4.jpg", name: "재테크", amount: "$500" },
      { image: "path/to/image5.jpg", name: "고정", amount: "$200" },
      { image: "path/to/image6.jpg", name: "기타", amount: "$300" },
    ],
  }),
  mounted() {
    this.createChart();
  },
  methods: {
    createChart() {
      new Chart(this.$refs.MyChart, {
        type: this.type,
        data: this.data,
        options: this.options,
      });
    },
  },
};
</script>

<style>
.chart-container {
  position: relative;
  width: 100%;
  max-width: 400px;
  height: 450px;
  margin: 0 auto;
}
canvas {
  width: 100%;
  height: 100%;
}
.income-expense-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}
.list-item {
  display: flex;
  align-items: center;
  justify-content: space-between; /* Align items to space between */
  margin-bottom: 10px;
  width: 80%;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  background-color: #f9f9f9;
}
.item-image {
  width: 50px;
  height: 50px;
  margin-right: 10px;
}
.item-name {
  font-weight: bold;
  margin-right: auto; /* Push the name to the left */
}
.item-amount {
  color: #555;
}
</style>
