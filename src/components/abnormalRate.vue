<template>
  <div >
    <div id="containerAbnormal" style="width: 460px;height: 200px;display: inline-block"></div>
  </div>
</template>

<script type="text/ECMAScript-6">
  import Highcharts from 'highcharts/highstock';
  import HighchartsMore from 'highcharts/highcharts-more';
  import HighchartsDrilldown from 'highcharts/modules/drilldown';
  import Highcharts3D from 'highcharts/highcharts-3d';
  //import exporting from 'highcharts/modules/exporting';
  HighchartsMore(Highcharts)
  HighchartsDrilldown(Highcharts);
  Highcharts3D(Highcharts);
  //exporting(Highcharts);
  export default {
    name: 'HelloWorld',
    components: {  },
    data () {
      return {
        pro: '',
        centerDialogVisibleMap: false,
        qdate: '',
        qdq: '',
        full: true
      }
    },
    created () {

    },
    mounted(){
      this.init();
      //this.drawLineLiveArea()
    },
    methods: {
      init () {
        var chart = Highcharts.chart('containerAbnormal', {
          title: {
            text: '平均死亡率'
          },
          subtitle: {
            text: ''
          },
          yAxis: {
            title: {
              text: '平均死亡率'
            }
          },
          legend: {
            layout: 'vertical',
            align: 'right',
            verticalAlign: 'middle'
          },
          plotOptions: {
            series: {
              label: {
                connectorAllowed: false
              },
              pointStart: 2010
            }
          },
          series: [{
            name: '平均死亡率',
            data: [43934, 52503, 57177, 69658, 97031, 119931, 137133, 154175]
          }],
          responsive: {
            rules: [{
              condition: {
                maxWidth: 500
              },
              chartOptions: {
                legend: {
                  layout: 'horizontal',
                  align: 'center',
                  verticalAlign: 'bottom'
                }
              }
            }]
          }
        });
      }
    }
  }
</script>
