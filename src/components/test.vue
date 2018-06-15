<template>
  <div class="hello">
    <div id="container"></div>
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
    data () {
      return {
        pro: ''
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
        //初始化地图对象，加载地图
        let district;
        let map = new AMap.Map("container", {
          resizeEnable: true,
          //center: [114.00252, 22.554134],//地图中心点
          center: [114.00252, 22.654134],//地图中心点
          zoom: 11 //地图显示的缩放级别
        });
        AMap.service('AMap.DistrictSearch', function() {
          var opts = {
            subdistrict: 1,   //返回下一级行政区
            extensions: 'all',  //返回行政区边界坐标组等具体信息
            level: 'city'  //查询行政级别为 市
          };
          //实例化DistrictSearch
          district = new AMap.DistrictSearch(opts);
          district.setLevel('district');
          //行政区查询
          district.search('深圳市', function(status, result) {
            var bounds = result.districtList[0].boundaries;
            var polygons = [];
            if (bounds) {
              for (var i = 0, l = bounds.length; i < l; i++) {
                //生成行政区划polygon
                var polygon = new AMap.Polygon({
                  map: map,
                  strokeWeight: 1,
                  path: bounds[i],
                  fillOpacity: 0.7,
                  fillColor: '#CCF3FF',
                  strokeColor: '#CC66CC'
                });
                polygons.push(polygon);
              }
              map.setFitView();//地图自适应
            }
          });
        });
      },
      drawLineLiveArea () {
        var chart = Highcharts.chart('containerLiveArea', {
          chart: {
            type: 'column'
          },
          title: {
            text: '堆叠柱形图'
          },
          xAxis: {
            categories: ['苹果', '橘子', '梨', '葡萄', '香蕉']
          },
          yAxis: {
            min: 0,
            title: {
              text: '水果消费总量'
            },
            stackLabels: {  // 堆叠数据标签
              enabled: true,
              style: {
                fontWeight: 'bold',
                color: (Highcharts.theme && Highcharts.theme.textColor) || 'gray'
              }
            }
          },
          legend: {
            align: 'right',
            x: -30,
            verticalAlign: 'top',
            y: 25,
            floating: true,
            backgroundColor: (Highcharts.theme && Highcharts.theme.background2) || 'white',
            borderColor: '#CCC',
            borderWidth: 1,
            shadow: false
          },
          tooltip: {
            formatter: function () {
              return '<b>' + this.x + '</b><br/>' +
                this.series.name + ': ' + this.y + '<br/>' +
                '总量: ' + this.point.stackTotal;
            }
          },
          plotOptions: {
            column: {
              stacking: 'normal',
              dataLabels: {
                enabled: true,
                color: (Highcharts.theme && Highcharts.theme.dataLabelsColor) || 'white',
                style: {
                  // 如果不需要数据标签阴影，可以将 textOutline 设置为 'none'
                  textOutline: '1px 1px black'
                }
              }
            },
            series: {
              cursor: 'pointer',
              point: {
                events: {
                  click: function () {
                    alert()
                    console.log(this)
                  }
                }
              }
            }
          },
          series: [{
            name: '小张',
            data: [5, 3, 4, 7, 2]
          }, {
            name: '小彭',
            data: [2, 2, 3, 2, 1]
          }, {
            name: '小潘',
            data: [3, 4, 4, 2, 5]
          }]
        });
      }
    }
  }
</script>

<style scoped>
  .chart {
    min-width: 320px;
    max-width: 800px;
    height: 220px;
    margin: 0 auto;
  }
  #tip {
    background-color: #fff;
    padding:0 10px;
    border: 1px solid silver;
    box-shadow: 3px 4px 3px 0px silver;
    position: absolute;
    font-size: 12px;
    right: 10px;
    top: 5px;
    border-radius: 3px;
    line-height: 36px;
  }
</style>
