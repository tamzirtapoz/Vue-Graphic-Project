<template>
  <figure class="highcharts-figure">
    <div
      id="container2"
      :style="{ width: windowWidth > 1303 ? '40vw' : '80vw' }"
      class="container-fluid"
    ></div>
  </figure>
</template>

<script>
import { mapState } from "vuex";

export default {
  props: {
    Highcharts: Function,
  },
  data() {
    return {
      loadHighchart() {
        // Create the chart
        this.Highcharts.chart("container2", {
          chart: {
            type: "pie",
            // width: 500,
          },
          ...this.pieDrilldownProperties,
        });
      },
    };
  },

  computed: {
    ...mapState(["pieDrilldownProperties"]),
  },

  mounted() {
    this.loadHighchart();
  },
};
</script>

<style lang="scss">
.highcharts-figure,
.highcharts-data-table table {
  min-width: 320px;
  max-width: 660px;
  margin: 1em auto;
}

#container2 {
  height: 400px;
  min-width: 310px;
  max-width: 500px;
}

.highcharts-data-table table {
  font-family: Verdana, sans-serif;
  border-collapse: collapse;
  border: 1px solid #ebebeb;
  margin: 10px auto;
  text-align: center;
  width: 100%;
  max-width: 500px;
}
.highcharts-data-table caption {
  padding: 1em 0;
  font-size: 1.2em;
  color: #555;
}
.highcharts-data-table th {
  font-weight: 600;
  padding: 0.5em;
}
.highcharts-data-table td,
.highcharts-data-table th,
.highcharts-data-table caption {
  padding: 0.5em;
}
.highcharts-data-table thead tr,
.highcharts-data-table tr:nth-child(even) {
  background: #f8f8f8;
}
.highcharts-data-table tr:hover {
  background: #f1f7ff;
}
.highcharts-container.highcharts-container {
  z-index: auto !important;
  overflow: visible !important;
}
</style>
