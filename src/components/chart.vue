<script>
import Highcharts from "highcharts";
import _ from "lodash";

export default {
  methods: {
    dataSource() {
      const chart = this.blood_group.map(item => item.blood_group);

      const base = blood_group
        .countBy()
        .map((value, key) => ({ key, value }))
        .orderBy(["value"], ["desc"])
        .value();

      const categories = base.map(item => item.key);

      const values = base.map(item => item.value);

      this.setup({ categories, values });
    },

    setup(obj) {
      const { categories, values } = obj;

      Highcharts.chart("container-for-chart", {
        chart: {
          type: "column"
        },
        title: {
          text: "Vuejs Project"
        },
        subtitle: {
          text: "By David Ikenna"
        },
        xAxis: {
          categories: categories,
          crosshair: true
        },
        yAxis: {
          min: 0,
          title: {
            text: "number of people"
          }
        },

        series: [
          {
            name: "Blood group",
            data: values
          }
        ]
      });
    }
  }
};
</script>

<template>
  <div id="container-for-chart"></div>
</template>
