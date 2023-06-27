<script>
import { AgChartsVue } from "ag-charts-vue";
import jsonData from "./data.json"; // Assuming the JSON file is named "data.json" and located in the same folder as your Vue script

const monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "June",
 "July", "Aug", "Sep", "Oct", "Nov", "Dec"];

const LineExample = {
    template: `
        <ag-charts-vue :options="options"></ag-charts-vue>
    `,
  data() {
    return {
      markerSize: 10,
      options: {}
    };
  },
  components: {
    AgChartsVue,
  },
  methods: {
    parseJSONData() {
      const transformedData = jsonData.map(row => {
        return {
            date: `${monthNames[new Date(row.date).getMonth()]} ${new Date(row.date).getFullYear().toString().slice(-2)}`,
            var: parseFloat(row["Var"].slice(0, -1))
        };
      });

      return transformedData;
    },
    updateOptions() {
      const transformedData = this.parseJSONData();

      this.options.data = transformedData;
      this.options.series = [
        {
          xKey: "date",
          yKey: "var",
          marker: {
            size: this.markerSize
          }
        }
      ];
      this.options.title = {
        text: "Monthly Average Volatility"
      };
      this.options.axes = [
        {
            type: 'category',
            position: 'bottom',
            title: {
                text: 'Time',
            },
        },
        {
            type: 'number',
            position: 'left',
            title: {
                text: 'VaR (%)',
            },
            tick: {
                interval: 0.5,
            },
        },
      ];
    }
  },
  beforeMount() {
    this.updateOptions();
  }
};

export default {
        components: {
            LineExample,
        },
    };
</script>
