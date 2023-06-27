<script>
    import { AgChartsVue } from "ag-charts-vue";
    import { getData } from "./data.js";

    const ChartExample = {
        template: `<ag-charts-vue :options="options"></ag-charts-vue>`,
        components: {
            'ag-charts-vue': AgChartsVue,
        },
        data: function () {
            return {
                options: null,
            };
        },
        created() {
            this.options = {
                data: getData(),
                series: [
                    {
                        type: 'pie',
                        angleKey: 'value',
                        calloutLabelKey: 'label',
                        sectorLabelKey: 'value',
                        sectorLabel: {
                            color: 'white',
                            fontWeight: 'bold',
                        },
                    },
                ],
            };
            // console.log(this.options.data)
        },
        methods: {
            getData() {
                // Define or import your getData function here.
                // This function should return the required data structure for your chart.
            },
        },
        mounted() {},
    };

    export default ChartExample;

</script>
