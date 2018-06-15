<template>
  <div >
    <div id="containerEconomic" style="width: 400px;height: 225px;display: inline-block;box-shadow: 2px 2px 2px #888888;"></div>
  </div>
</template>

<script type="text/ECMAScript-6">
  import Highcharts from 'highcharts/highstock';
  import HighchartsMore from 'highcharts/highcharts-more';
  import HighchartsDrilldown from 'highcharts/modules/drilldown';
  import Highcharts3D from 'highcharts/highcharts-3d';
  HighchartsMore(Highcharts);
  HighchartsDrilldown(Highcharts);
  Highcharts3D(Highcharts);
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
        var chart = Highcharts.chart('containerEconomic', {
          chart: {
            /*backgroundColor: {
             linearGradient: [0, 0, 500, 500],
             stops: [
             [0, 'rgb(255, 255, 255)'],
             [1, 'rgb(200, 200, 255)']
             ]
             },*/
            zoomType: 'xy'
          },
          title: {
            text: '数字经济'
          },
          subtitle: {
            text: '12000家'
          },
          xAxis: [{
            categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
              'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
            crosshair: true
          }],
          yAxis: [{ // Primary yAxis
            labels: {
              format: '{value}°C',
              style: {
                color: Highcharts.getOptions().colors[1]
              }
            },
            title: {
              text: '增长率',
              style: {
                color: Highcharts.getOptions().colors[1]
              }
            }
          }, { // Secondary yAxis
            title: {
              text: '数量',
              style: {
                color: Highcharts.getOptions().colors[0]
              }
            },
            labels: {
              format: '{value} mm',
              style: {
                color: Highcharts.getOptions().colors[0]
              }
            },
            opposite: true
          }],
          legend: {
            enabled: false,
            layout: 'vertical',
            align: 'right',
            verticalAlign: 'middle'
          },
          tooltip: {
            shared: true
          },
          /*legend: {
           layout: 'vertical',
           align: 'left',
           x: 120,
           verticalAlign: 'top',
           y: 100,
           floating: true,
           backgroundColor: (Highcharts.theme && Highcharts.theme.legendBackgroundColor) || '#FFFFFF'
           },*/
          /*legend: {

           },*/
          series: [{
            name: '数量',
            type: 'column',
            yAxis: 1,
            data: [49.9, 71.5, 106.4, 129.2, 144.0, 176.0, 135.6, 148.5, 216.4, 194.1, 95.6, 54.4],
            dataLabels: {
              x: 100,
              backgroundColor: 'red'
            },
            tooltip: {
              valueSuffix: ' mm'
            }
          }, {
            name: '增长率',
            type: 'spline',
            data: [7.0, 6.9, 9.5, 14.5, 18.2, 21.5, 25.2, 26.5, 23.3, 18.3, 13.9, 9.6],
            tooltip: {
              valueSuffix: '°C'
            }
          }]
        });
      }
    }
  }
</script>
