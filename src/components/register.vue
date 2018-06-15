<template>
  <div >
    <div id="containerResister" style="width: 400px;height: 225px;display: inline-block;box-shadow: 2px 2px 2px #888888;"></div>
  </div>
</template>

<script type="text/ECMAScript-6">
  import Highcharts from 'highcharts/highstock';
  import HighchartsMore from 'highcharts/highcharts-more';
  import HighchartsDrilldown from 'highcharts/modules/drilldown';
  import Highcharts3D from 'highcharts/highcharts-3d';
  HighchartsMore(Highcharts)
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
        full: true,
        rate: [],
        dataX: [],
        dataSum: [],
        total: ''
      }
    },
    created () {
      this.time();
    },
    mounted(){
      this.init();
      //this.drawLineLiveArea()
    },
    methods: {
      time () {
        this.$http.get('http://10.0.10.253:8000/api/generalRegCount').then(response => {
            console.log('response.data',response.data.regCountEachYear);
            if (this.dataX) {
              this.dataX = [];
            }
            if (this.dataSum) {
              this.dataSum = [];
            }
            this.total = response.data.regCountTotal
            response.data.regCountEachYear.map(arr=>{
              this.rate.push(arr.delta);
              this.dataX.push(arr.year);
              this.dataSum.push(arr.count);
            })
            console.log(this.dataX)
            this.init();
          })
          .catch(function (response) {
            console.log(response);
          });
      },
      init () {
        var chart = Highcharts.chart('containerResister', {
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
            text: '企业注册数量'+ '(' +this.total + '家)',
            style: {
              //"color": "blue" ,
              "font-size": '18px'
            }
          },
          /*subtitle: {
            text: this.total + '家',
            style: {
              "color": "blue" ,
              "font-size": '18px'
            }
          },*/
          xAxis: [{
            categories: this.dataX,
            crosshair: true
          }],
          yAxis: [{ // Primary yAxis
            labels: {
              format: '{value}',
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
              format: '{value} ',
              style: {
                color: Highcharts.getOptions().colors[0]
              }
            },
            opposite: true
          }],
          legend: {
            enabled: false,
            align: 'left',
            verticalAlign: 'top',
            y: 70,
            layout: 'vertical'
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
            data: this.dataSum,
            dataLabels: {
              x: 100,
              backgroundColor: 'red'
            },
            tooltip: {
              valueSuffix: ' '
            }
          }, {
            name: '增长率',
            type: 'spline',
            data: this.rate,
            tooltip: {
              valueSuffix: ''
            }
          }]
        });
      }
    }
  }
</script>
