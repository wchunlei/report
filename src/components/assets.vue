<template>
  <div >
    <div id="containerAssets" style="width: 400px;height: 225px;display: inline-block;margin-top: -52px;box-shadow: 2px 2px 2px #888888;"></div>
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
        full: true,
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
        this.$http.get('http://10.0.10.253:8000/api/generalRegCapital').then(response => {
            console.log('response.data1',response.data.regCapital);
            if (this.dataX) {
              this.dataX = [];
            }
            if (this.dataSum) {
              this.dataSum = [];
            }
            this.total = response.data.regCapitalTotal
            response.data.regCapital.map(arr=>{
              this.dataX.push(arr.hydm);
              this.dataSum.push(arr.capital);
            })
            console.log(this.dataX)
            this.init();
          })
          .catch(function (response) {
            console.log(response);
          });
      },
      init () {
        var chart = Highcharts.chart('containerAssets', {
          chart: {
            polar: true,
            type: 'line'
          },
          title: {
            text: '注册资本(20万亿)'
          },
          pane: {
            size: '80%'
          },
          xAxis: {
            categories: this.dataX,
            tickmarkPlacement: 'on',
            lineWidth: 0,
            gridLineColor: '#ccc'
          },
          yAxis: {
            gridLineInterpolation: 'polygon',
            lineWidth: 0,
            min: 0,
            gridLineColor: '#ccc'
          },
          tooltip: {
            shared: true,
            //pointFormat: '<span style="color:{series.color}">{series.name}: <b>${point.y:,.0f}</b><br/>'
          },
          legend: {
            enabled: false,
            align: 'left',
            verticalAlign: 'top',
            y: 70,
            layout: 'vertical'
          },
          series: [{
            name: '注册资本',
            data: this.dataSum,
            pointPlacement: 'on'
          }]
        });
      }
    }
  }
</script>
