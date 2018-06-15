<template>
  <div >
    <div id="containerBusiness" style="width: 400px;height: 225px;display: inline-block;margin-top: -35px;box-shadow: 2px 2px 2px #888888;"></div>
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
        var chart = Highcharts.chart('containerBusiness', {
          chart: {
            spacing : [40, 0 , 40, 0]
          },
          title: {
            floating:true,
            text: '行业分布'
          },
          tooltip: {
            pointFormat: '{series.name}: <b>{point.percentage:.1f}%</b>'
          },
          plotOptions: {
            pie: {
              allowPointSelect: true,
              cursor: 'pointer',
              dataLabels: {
                enabled: true,
                format: '<b>{point.name}</b>: {point.percentage:.1f} %',
                style: {
                  color: (Highcharts.theme && Highcharts.theme.contrastTextColor) || 'black'
                }
              },
              point: {
                events: {
                  mouseOver: function(e) {  // 鼠标滑过时动态更新标题
                    // 标题更新函数，API 地址：https://api.hcharts.cn/highcharts#Chart.setTitle
                    chart.setTitle({
                      text: e.target.name+ '\t'+ e.target.y + ' %'
                    });
                  }
                  //,
                  // click: function(e) { // 同样的可以在点击事件里处理
                  //     chart.setTitle({
                  //         text: e.point.name+ '\t'+ e.point.y + ' %'
                  //     });
                  // }
                }
              },
            }
          },
          legend: {
            enabled: false,
            layout: 'vertical',
            align: 'right',
            verticalAlign: 'middle'
          },
          series: [{
            type: 'pie',
            innerSize: '80%',
            name: '市场份额',
            data: [
              {name:'ww',   y: 45.0},
              ['IE',       26.8],
              {
                name: 'Chrome',
                y: 12.8
              },
              ['Safari',    8.5],
              ['Opera',     6.2],
              ['其他',   0.7]
            ]
          }]
        }, function(c) { // 图表初始化完毕后的会掉函数
          // 环形图圆心
          var centerY = c.series[0].center[1],
            titleHeight = parseInt(c.title.styles.fontSize);
          // 动态设置标题位置
          c.setTitle({
            y:centerY + titleHeight/2
          });
        });
      }
    }
  }
</script>
