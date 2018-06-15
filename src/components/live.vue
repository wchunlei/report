<template>
  <div class="hello">
    <div style="display:inline-block;margin-right:50px">
      <div id="containerLive" :style="{width: '800px', height: '600px'}"></div>
    </div>
    <div style="display:inline-block;margin-right:50px;text-align: left;">
      <div style="display:inline-block;margin-right:50px">
        <div class="select">
          <el-select v-model="selectYear" placeholder="请选择" class="select-info">
            <el-option
              v-for="item in yearOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value"
              class="select-info-option">
            </el-option>
          </el-select>
        </div>
      </div>
      <div id="containerLiveArea" :style="{width: '800px', height: '600px'}"></div>
    </div>

    <el-dialog
      title="消亡-存活"
      :visible.sync="centerDialogVisibleMap"
      width="1800px"
      :fullscreen='full'
      center>
      <mapLive ref="mapLive" :qdate="qdate" :qdq="qdq" :dialog="centerDialogVisibleMap"></mapLive>
      <span slot="title">
        <span style="color: #ccc;font-size: 24px;display:inline-block;margin-right:400px">消亡</span>
        <span style="color: red;font-size: 24px;display:inline-block;margin-left:400px">存活</span>
      </span>
    </el-dialog>
  </div>
</template>

<script type="text/ECMAScript-6">
  import Highcharts from 'highcharts/highstock';
  import HighchartsMore from 'highcharts/highcharts-more';
  import HighchartsDrilldown from 'highcharts/modules/drilldown';
  import Highcharts3D from 'highcharts/highcharts-3d';
  import mapLive from './mapLive';
  HighchartsMore(Highcharts)
  HighchartsDrilldown(Highcharts);
  Highcharts3D(Highcharts);
  export default {
    name: 'HelloWorld',
    components: {mapLive},
    props: ['dialogLive'],
    data () {
      const yearOptions = () => {
        let arr = [];
        for (let i = 1996;i <= 2016;i++) {
          for (let j=1; j<13; j++) {
            let obj = {};
            let month = j;
            if (month < 10) {
              month = '0' + month;
            }
            obj.value = i.toString() + '-' + month;
            obj.label = i.toString() + '年' + month + '月';
            arr.push(obj);
            if (i == 2016 && j == 6) {
              return arr;
            }
          }
        }
        //console.log('arr',arr);
        return arr;
      };
      return {
        yearOptions: yearOptions() ,
        selectYear: '2016-06',
        centerDialogVisibleMap: false,
        full: true,
        qdate: '',
        qdq: '',
        allData: {
          datasets: [],
          xData: []
        },
        dataX: [],
        dataY: [],
        live: [],
        liveObj: {},
        die: [],
        dieObj: {},
        liveRate: [],
        dataSumObj: {},
        dataLiveX: [],
        dataLiveY: []
      }
    },
    created() {

    },
    watch: {
      "selectYear" (newval,oldval) {
        this.liveInfo(newval);
        this.qdate = newval;
      },
    },
    mounted(){
      this.getData();
      this.liveInfo('2016-06');
      this.init();
      this.drawLineLiveArea()
    },
    methods: {
      getData () {
        this.$http.get('http://10.0.10.253:8000/api/qychl').then(response => {
            console.log('response.data',response.data);
            if (this.dataX) {
              this.dataX = [];
            }
            if (this.liveRate) {
              this.liveRate = [];
            }
            response.data.map(arr=>{
              let temp;
              //temp = arr.sj.split('-').join('.');
              temp = parseInt(arr.sj.split('-')[0]) + parseInt(arr.sj.split('-')[1])*0.083;
              this.dataX.push(parseFloat(temp));
              this.live.push(parseFloat(arr.cunhuo));
              this.die.push(parseFloat(arr.xiaowang));
              this.liveRate.push(parseFloat(arr.cunhuolv));
            })
          //console.log('dataX',this.dataX)
            this.liveObj.data = this.liveRate;
            this.liveObj.name = "存活率";
            this.liveObj.type = "line";
            this.liveObj.unit = "";
            this.liveObj.valueDecimals = 1;
            this.dataY.push(this.liveObj);
            this.dataSumObj.data = this.live;
            this.dataSumObj.name = "存活企业";
            this.dataSumObj.type = "area";
            this.dataSumObj.unit = "家";
            this.dataSumObj.valueDecimals = 0;
            this.dataY.push(this.dataSumObj);
            this.dieObj.data = this.die;
            this.dieObj.name = "消亡企业";
            this.dieObj.type = "area";
            this.dieObj.unit = "家";
            this.dieObj.valueDecimals = 0;
            this.dataY.push(this.dieObj);
            this.allData.datasets = this.dataY;
            this.allData.xData = this.dataX;
          //console.log("allData1",this.allData)
            this.init();
          })
          .catch(function (response) {
            console.log(response);
          });
      },
      liveInfo (newval) {
        this.$http.get('http://10.0.10.253:8000/api/qychxx',{params: {
              qdate: newval
            }}).then(response => {
            if (this.dataLiveX) {
              this.dataLiveX = [];
            }
            if (this.dataLiveY) {
              this.dataLiveY = [];
            }
            let tempObj = {};
            let temp = [];
            let tempObj1 = {};
            let temp1 = [];
            response.data.map(arr=>{
              this.dataLiveX.push(arr.dq);
              temp.push(arr.xiaowang);
              temp1.push(arr.cunhuo);
            })
            tempObj.name = "消亡";
            tempObj.data = temp;
            tempObj1.name = "存活";
            tempObj1.data = temp1;
            this.dataLiveY.push(tempObj);
            this.dataLiveY.push(tempObj1);
            console.log(this.dataLiveY)
            this.drawLineLiveArea();
          })
          .catch(function (response) {
            console.log(response);
          });
      },
      init () {
        /*
         本例子的目的是为了演示通过 Dom 事件、Highcharts 事件、Highcharts API 来讲一个页面中的多个图表进行联动的。
         本例通过循环创建类似的图表并绑定鼠标的滑动事件来对多个图表进行演示联动效果。
         */
        /**
         * 为了让多个图表的提示框即十字准星线能够联动，这里绑定多个图表的附件 dom 的鼠标事件进行联动
         */
        console.log('Highcharts',Highcharts.charts)
        $('#containerLive').bind('mousemove touchmove touchstart', function (e) {
          /*let chart;
          let point;
          let event;*/
          for (let i = 6; i < Highcharts.charts.length; i++) {
            if (typeof Highcharts.charts[i] !== 'undefined') {
              if (Highcharts.charts[i].renderTo.id == '') {
                //console.log('Highcharts.charts',Highcharts.charts[i].renderTo.id + '123')
                let chart = Highcharts.charts[i];
                let event = chart.pointer.normalize(e.originalEvent); // Find coordinates within the chart
                let point = chart.series[0].searchPoint(event, true); // Get the hovered point
                //console.log('event',chart.pointer)
                if (point) {
                  point.highlight(e);
                }
              }
            }
          }
        });
        /**
         * 重写内部的方法， 这里是将提示框即十字准星的隐藏函数关闭
         */
        Highcharts.Pointer.prototype.reset = function () {
          return undefined;
        };
        /**
         * 高亮当前的数据点，并设置鼠标滑动状态及绘制十字准星线
         */
        Highcharts.Point.prototype.highlight = function (event) {
          this.onMouseOver(); // 显示鼠标激活标识
          this.series.chart.tooltip.refresh(this); // 显示提示框
          this.series.chart.xAxis[0].drawCrosshair(event, this); // 显示十字准星线
        };
        /**
         * 同步缩放效果，即当一个图表进行了缩放效果，其他图表也进行缩放
         */
        function syncExtremes(e) {
          var thisChart = this.chart;
          if (e.trigger !== 'syncExtremes') {
            Highcharts.each(Highcharts.charts, function (chart) {
              if (chart !== thisChart) {
                if (chart.xAxis[0].setExtremes) {
                  chart.xAxis[0].setExtremes(e.min, e.max, undefined, false, { trigger: 'syncExtremes' });
                }
              }
            });
          }
        }
        // 获取 JSON 数据，数据文件地址：
        //https://github.com/highcharts/highcharts/blob/master/samples/data/activity.json
        let _this = this;
        //$.getJSON('https://data.jianshukeji.com/jsonp?filename=json/activity.json&callback=?', function (activity) {
          //console.log('activity',activity)
          //activity = _this.allData;
        //console.log("allData1",_this.allData)
          //console.log("allData1",_this.allData.xData)
          $.each(_this.allData.datasets, function (i, dataset) {
            // 添加 X 数据
            //console.log('dataset',dataset.data)
            dataset.data = Highcharts.map(dataset.data, function (val, j) {
              return [_this.allData.xData[j], val];
            });
            //console.log('dataset1',dataset.data)
            let dom = $('<div class="chart">')
              .appendTo('#containerLive')
            //console.log(dom[0])
            //dom[0].style.width = '800px';
            //dom[0].style.height = '200px';
            //_this.$nextTick(function() {
              let chart = Highcharts.chart(dom[0], {
                chart: {
                  width: 800,
                  height: 200,
                  marginLeft: 40, // Keep all charts left aligned
                  spacingTop: 20,
                  spacingBottom: 20,
                  zoomType: 'x'
                },
                title: {
                  text: dataset.name,
                  align: 'left',
                  margin: 0,
                  x: 30
                },
                credits: {
                  enabled: false
                },
                legend: {
                  enabled: false
                },
                xAxis: {
                  crosshair: true,
                  events: {
                    setExtremes: syncExtremes
                  },
                  labels: {
                    format: '{value} '
                  }
                },
                yAxis: {
                  minTickInterval:0.01,
                  /*tickPositioner: function () {
                    if(dataset.type == 'line') {
                      var positions = [],
                        tick = Math.floor(this.dataMin),
                        increment = Math.ceil((this.dataMax - this.dataMin) / 6);
                      for (tick; tick - increment <= this.dataMax; tick += increment) {
                        positions.push(tick);
                      }
                      return positions;
                    }
                  },*/
                  title: {
                    text: null
                  }
                },
                plotOptions: {
                  area: {
                    cursor: 'pointer',
                    events: {
                      click: function () {
                        alert()
                        console.log(this)
                      }
                    },
                    dataLabels: {
                      enabled: true,
                      format: '{dataset.name}'
                    }
                  },
                  line: {
                    cursor: 'pointer',
                    events: {
                      click: function () {
                        alert()
                        console.log(this)
                      }
                    },
                    dataLabels: {
                      enabled: true,
                      format: '{dataset.name}'
                    }
                  }

                },
                tooltip: {
                  positioner: function () {
                    return {
                      x: this.chart.chartWidth - this.label.width, // right aligned
                      y: -1 // align to title
                    };
                  },
                  borderWidth: 0,
                  backgroundColor: 'none',
                  pointFormat: '{point.y}',
                  headerFormat: '',
                  shadow: false,
                  style: {
                    fontSize: '18px'
                  },
                  valueDecimals: dataset.valueDecimals
                },
                series: [{
                  data: dataset.data,
                  name: dataset.name,
                  type: dataset.type,
                  color: Highcharts.getOptions().colors[i],
                  fillOpacity: 0.3,
                  tooltip: {
                    valueSuffix: ' ' + dataset.unit
                  }
                }]
              });
            //})
          });
        //});
      },
      drawLineLiveArea () {
        let _this = this;
        var chart = Highcharts.chart('containerLiveArea', {
          chart: {
            type: 'column'
          },
          title: {
            text: '企业存亡数量'
          },
          xAxis: {
            categories: this.dataLiveX
          },
          yAxis: {
            min: 0,
            title: {
              text: '企业存亡数量'
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
                    _this.centerDialogVisibleMap = true;
                    _this.qdq = this.category;
                    _this.qdate = _this.selectYear;
                    console.log(this)
                  }
                }
              }
            }
          },
          series: this.dataLiveY
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
  .select {
    margin-bottom: 20px;
  }
</style>
<style>
  .v-modal {
    z-index: 0 !important;
  }
</style>
