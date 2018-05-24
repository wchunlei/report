<template>
  <div class="hello">
    <!--<el-select v-model="value" placeholder="请选择" class="select-info">
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value"
        class="select-info-option">
      </el-option>
    </el-select>-->

   <!-- <el-carousel :interval="3000" type="card" height="600px">
      <el-carousel-item v-for="item in 1" :key="item" style="width:1500px">
        &lt;!&ndash;<div id="myChart" :style="{width: '500px', height: '500px'}"></div>&ndash;&gt;
        <div id="container" :style="{width: '950px', height: '600px'}"></div>
      </el-carousel-item>
      <el-carousel-item v-for="item in 1" :key="item">
        &lt;!&ndash;<div id="myChart" :style="{width: '500px', height: '500px'}"></div>&ndash;&gt;
        <div id="container1" :style="{width: '950px', height: '600px'}"></div>
      </el-carousel-item>
      <el-carousel-item v-for="item in 1" :key="item">
        &lt;!&ndash;<div id="myChart" :style="{width: '500px', height: '500px'}"></div>&ndash;&gt;
        <div id="container2" :style="{width: '950px', height: '600px'}"></div>
      </el-carousel-item>
    </el-carousel>-->
    <div class="select" style="margin-left: 128px">
      <el-select v-model="selectBusiness" placeholder="请选择" class="select-info">
        <el-option
          v-for="item in businessOptions"
          :key="item.value"
          :label="item.label"
          :value="item.value"
          class="select-info-option">
        </el-option>
      </el-select>
    </div>

    <el-carousel :interval="30000" indicator-position="outside" height="700px">

      <el-carousel-item v-for="item in 1" :key="item">
        <!--<div id="myChart" :style="{width: '500px', height: '500px'}"></div>-->
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
            <!--<el-date-picker
              v-model="value"
              type="year"
              placeholder="选择年">
            </el-date-picker>-->
          </div>
          <div id="containerA" :style="{width: '800px', height: '600px'}"></div>
        </div>
        <div style="display:inline-block">
          <div class="select">
            <el-select v-model="selectArea" placeholder="请选择" class="select-info">
              <el-option
                v-for="item in areaOptions"
                :key="item.value"
                :label="item.label"
                :value="item.value"
                class="select-info-option">
              </el-option>
            </el-select>
          </div>
          <div id="containers" :style="{width: '800px', height: '600px'}"></div>
        </div>
      </el-carousel-item>

      <el-carousel-item v-for="item in 1" :key="item">
        <!--<div id="myChart" :style="{width: '500px', height: '500px'}"></div>-->
        <div style="display:inline-block;margin-right:50px">
          <div class="select">
            <el-select v-model="selectWorkYear" placeholder="请选择" class="select-info">
              <el-option
                v-for="item in yearOptions"
                :key="item.value"
                :label="item.label"
                :value="item.value"
                class="select-info-option">
              </el-option>
            </el-select>
            <!--<el-date-picker
              v-model="value"
              type="year"
              placeholder="选择年">
            </el-date-picker>-->
          </div>
          <div id="containerWork" :style="{width: '800px', height: '600px'}"></div>
        </div>
        <div style="display:inline-block">
          <div class="select">
            <el-select v-model="selectWorkArea" placeholder="请选择" class="select-info">
              <el-option
                v-for="item in areaOptions"
                :key="item.value"
                :label="item.label"
                :value="item.value"
                class="select-info-option">
              </el-option>
            </el-select>
          </div>
          <div id="containerWorks" :style="{width: '800px', height: '600px'}"></div>
        </div>
      </el-carousel-item>

      <el-carousel-item v-for="item in 1" :key="item">
        <!--<div id="myChart" :style="{width: '500px', height: '500px'}"></div>-->
        <div style="display:inline-block;margin-right:50px">
          <div class="select">
            <el-select v-model="selectMoneyYear" placeholder="请选择" class="select-info">
              <el-option
                v-for="item in yearOptions"
                :key="item.value"
                :label="item.label"
                :value="item.value"
                class="select-info-option">
              </el-option>
            </el-select>
            <!--<el-date-picker
              v-model="value"
              type="year"
              placeholder="选择年">
            </el-date-picker>-->
          </div>
          <div id="containerMoney" :style="{width: '800px', height: '600px'}"></div>
        </div>
        <div style="display:inline-block">
          <div class="select">
            <el-select v-model="selectMoneyArea" placeholder="请选择" class="select-info">
              <el-option
                v-for="item in areaOptions"
                :key="item.value"
                :label="item.label"
                :value="item.value"
                class="select-info-option">
              </el-option>
            </el-select>
          </div>
          <div id="containerMoneys" :style="{width: '800px', height: '600px'}"></div>
        </div>
      </el-carousel-item>

    </el-carousel>

    <el-dialog
      title="详情"
      :visible.sync="centerDialogVisible"
      width="1800px"
      fullscreen="true"
      modal-append-to-body="false"
      v-loading.body="listLoading"
      center>
      <!--<div style="text-align: center">
        <div id="map1" style="width: 850px;height:800px;display:inline-block"></div>
        <div id="map2" style="width: 850px;height:800px;display:inline-block"></div>
      </div>-->
      <!--<div v-loading.body="listLoading">加载中...</div>-->
      <!--<div v-loading.body="listLoading" style="z-index: 999">加载中...</div>-->
      <Map ref="map" :hydm="hydm" :year="year" :dq="dq" :dialog="centerDialogVisible"></Map>
      <!--<span slot="footer" class="dialog-footer">
        <div v-loading.body="listLoading">加载中...</div>
        <el-button @click="centerDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
      </span>-->
    </el-dialog>

  </div>
</template>

<script type="text/ECMAScript-6">
  //var Highcharts = require('highcharts/highstock');
  import Highcharts from 'highcharts/highstock';
  import HighchartsMore from 'highcharts/highcharts-more';
  import HighchartsDrilldown from 'highcharts/modules/drilldown';
  import Highcharts3D from 'highcharts/highcharts-3d';
  //import darkBlue from 'highcharts/themes/dark-blue';
  import darkBlue from 'highcharts/themes/sand-signika';
  import Map from './map';

  HighchartsMore(Highcharts)
  HighchartsDrilldown(Highcharts);
  Highcharts3D(Highcharts);
  darkBlue(Highcharts);
export default {
  name: 'HelloWorld',
  components: { Map },
  data () {
    const yearOptions = () => {
      let arr = [];
      for (let i = 1995;i <= 2016;i++) {
        let obj = {};
        if (i == 1995) {
          obj.value = 'all';
          obj.label = '全部年份';
          arr.push(obj);
        } else {
          obj.value = i.toString();
          obj.label = i.toString() + '年';
          arr.push(obj);
        }
      }
      //console.log(arr);
      return arr;
    };
    return {
      listLoading: true,
      centerDialogVisible: false,
      hydm: 'A',
      year: '1996',
      dq: 'all',
      yearOptions: yearOptions() ,
      areaOptions: [{
        value: 'all',
        label: '全部地区'
      },{
        value: '宝安区',
        label: '宝安区'
      },{
        value: '龙岗区',
        label: '龙岗区'
      },{
        value: '福田区',
        label: '福田区'
      },{
        value: '罗湖区',
        label: '罗湖区'
      },{
        value: '南山区',
        label: '南山区'
      },{
        value: '龙华新区',
        label: '龙华新区'
      },{
        value: '前海深港合作区',
        label: '前海深港合作区'
      },{
        value: '光明新区',
        label: '光明新区'
      },{
        value: '坪山新区',
        label: '坪山新区'
      },{
        value: '盐田区',
        label: '盐田区'
      },{
        value: '大鹏新区',
        label: '大鹏新区'
      }],
      businessOptions: [{
        value: 'A',
        label: '农、林、牧、渔业'
      },{
        value: 'B',
        label: '采矿业'
      },{
        value: 'C',
        label: '制造业'
      },{
        value: 'D',
        label: '电力、热力、燃气及水生产和供应业'
      },{
        value: 'E',
        label: '建筑业'
      },{
        value: 'F',
        label: '批发和零售业'
      },{
        value: 'G',
        label: '交通运输、仓储和邮政业'
      },{
        value: 'H',
        label: '住宿和餐饮业'
      },{
        value: 'I',
        label: '信息传输、软件和信息技术服务业'
      },{
        value: 'J',
        label: '金融业'
      },{
        value: 'K',
        label: '房地产业'
      },{
        value: 'L',
        label: '租赁和商务服务业'
      },{
        value: 'M',
        label: '科学研究和技术服务业'
      },{
        value: 'N',
        label: '水利、环境和公共设施管理业'
      },{
        value: 'O',
        label: '居民服务、修理和其他服务业'
      },{
        value: 'P',
        label: '教育'
      },{
        value: 'Q',
        label: '卫生和社会工作'
      },{
        value: 'R',
        label: '文化、体育和娱乐业'
      },{
        value: 'S',
        label: '公共管理、社会保障和社会组织'
      },{
        value: 'T',
        label: '国际组织'
      }],
      selectBusiness: 'A',
      selectYear: '全部年份',
      selectArea: '全部地区',
      selectWorkYear: '全部年份',
      selectWorkArea: '全部地区',
      selectMoneyYear: '全部年份',
      selectMoneyArea: '全部地区',
      msg: 'Welcome to Your Vue.js App',
      dataX: [],
      dataSum: [],
      dateString: ''
    }
  },
  created () {
    //this.time();
    //this.hydm = 'B';
  },
  watch: {
    "selectYear" (newval,oldval) {
      this.time(newval);
    },
    "selectArea" (newval,oldval) {
      this.dq = newval;
      this.area(newval);
    },
    "selectWorkYear" (newval,oldval) {
      this.workTime(newval);
    },
    "selectWorkArea" (newval,oldval) {
      this.workArea(newval);
    },
    "selectMoneyYear" (newval,oldval) {
      this.moneyTime(newval);
    },
    "selectMoneyArea" (newval,oldval) {
      this.moneyArea(newval);
    },
    "selectBusiness" (newval,oldval) {
      this.hydm = newval;
      this.time('all');
      this.area('all');
      this.workTime('all');
      this.workArea('all');
      this.moneyTime('all');
      this.moneyArea('all');
    }
  },
  mounted(){
    this.time('all');
    this.area('all');
    this.workTime('all');
    this.workArea('all');
    this.moneyTime('all');
    this.moneyArea('all');
    this.drawLine();
    this.drawLine1();
    this.drawLineWork();
    this.drawLineWorks();
    this.drawLineMoney();
    this.drawLineMoneys();
  },
  methods: {
    time (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'snum',
        hydm: this.selectBusiness,
        year: newval
      }}).then(response => {
          console.log(response.data);
          if (this.dataX) {
            this.dataX = [];
          }
          if (this.dataSum) {
            this.dataSum = [];
          }
           response.data.map(arr=>{
             this.dataX.push(arr.sdq);
             this.dataSum.push(arr.num);
            })
          this.drawLine();
        })
        .catch(function (response) {
          console.log(response);
        });
    },
    area (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'snum',
        hydm: this.selectBusiness,
        dq: newval
      }}).then(response => {
          console.log(response.data);
          if (this.dataX) {
            this.dataX = [];
          }
          if (this.dataSum) {
            this.dataSum = [];
          }
          response.data.map(arr=>{
            this.dataX.push(arr.syear);
            this.dataSum.push(arr.num);
          })
          this.drawLine1();
        })
        .catch(function (response) {
          console.log(response);
        });
    },
    workTime (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'renshu',
        hydm: this.selectBusiness,
        year: newval
      }}).then(response => {
          console.log(response.data);
          if (this.dataX) {
            this.dataX = [];
          }
          if (this.dataSum) {
            this.dataSum = [];
          }
          response.data.map(arr=>{
            this.dataX.push(arr.cdq);
            this.dataSum.push(arr.num);
          })
          this.drawLineWork();
        })
        .catch(function (response) {
          console.log(response);
        });
    },
    workArea (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'renshu',
        hydm: this.selectBusiness,
        dq: newval
      }}).then(response => {
          console.log(response.data);
          if (this.dataX) {
            this.dataX = [];
          }
          if (this.dataSum) {
            this.dataSum = [];
          }
          response.data.map(arr=>{
            this.dataX.push(arr.cyear);
            this.dataSum.push(arr.num);
          })
          this.drawLineWorks();
        })
        .catch(function (response) {
          console.log(response);
        });
    },
    moneyTime (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'zczb',
        hydm: this.selectBusiness,
        year: newval
      }}).then(response => {
          console.log(response.data);
          if (this.dataX) {
            this.dataX = [];
          }
          if (this.dataSum) {
            this.dataSum = [];
          }
          response.data.map(arr=>{
            this.dataX.push(arr.sdq);
            this.dataSum.push(arr.num);
          })
          this.drawLineMoney();
        })
        .catch(function (response) {
          console.log(response);
        });
    },
    moneyArea (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'zczb',
        hydm: this.selectBusiness,
        dq: newval
      }}).then(response => {
          console.log(response.data);
          if (this.dataX) {
            this.dataX = [];
          }
          if (this.dataSum) {
            this.dataSum = [];
          }
          response.data.map(arr=>{
            this.dataX.push(arr.syear);
            this.dataSum.push(arr.num);
          })
          this.drawLineMoneys();
        })
        .catch(function (response) {
          console.log(response);
        });
    },
    drawLine(){
      let tt = this.dataX;
      var chart = Highcharts.chart('containerA', {
        chart: {
          polar: true,
          type: 'line'
        },
        title: {
          text: '注册数量',
          x: -80
        },
        pane: {
          size: '80%'
        },
        xAxis: {
          categories: tt,
          tickmarkPlacement: 'on',
          lineWidth: 0,
          lineColor: 'red',
          labels: {
            style: {
              "color": "#666666", "cursor": "default", "fontSize": "14px","fontWeight": "bold"
            }
          },
        },
        yAxis: {
          gridLineInterpolation: 'polygon',
          lineWidth: 0,
          min: 0,
          gridLineColor: '#ccc'
          /*labels: {
            style: {
              "color": "#666666", "cursor": "default", "fontSize": "12px"
            }
          },
          lineColor: '#ccc'*/
        },
        tooltip: {
          shared: true,
          //pointFormat: '<span style="color:{series.color}">{series.name}: <b>${point.y:,.0f}</b><br/>'
        },
        legend: {
          align: 'right',
          verticalAlign: 'top',
          y: 70,
          layout: 'vertical'
        },
        series: [{
          name: '注册数量',
          data: this.dataSum,
          /*dataLabels: {
            color: 'red'
          },*/
          pointPlacement: 'on'
        }]
      });
      /*let tt = this.dataX;
      var chart = new Highcharts.Chart({
        chart: {
          renderTo: 'container',
          type: 'column',
          /!*backgroundColor: {
            linearGradient: [0, 0, 500, 500],
            stops: [
              [0, 'rgb(255, 255, 255)'],
              [1, 'rgb(200, 200, 255)']
            ]
          },*!/
          options3d: {
            enabled: true,
            alpha: 0,
            beta: 0,
            depth: 50,
            viewDistance: 25
          }
        },
        xAxis: {
          categories: tt
        },
        legend: {
          //backgroundColor: '#ccc'
        },
        colors: ['#7cb5ec','#90ed7d'],
        title: {
          text: '注册数量'
        },
        subtitle: {
          //text: '可通过滑动下方滑块测试'
        },
        plotOptions: {
          column: {
            depth: 25
          }
        },
        series: [{
          name:'图例1',
          type: 'column',
          data: this.dataSum
        }, {
            name:'图例1',
            type: 'line',
            data: this.dataSum
          }]
      });*/
      // 基于准备好的dom，初始化echarts实例
      /*let myChart = this.$echarts.init(document.getElementById('myChart'))
      // 绘制图表
      myChart.setOption({
        title: { text: '深圳市南山区' },
        tooltip: {},
        xAxis: {
          nameTextStyle: {
            color: 'green ',
            nameTextStyle: 'oblique'
          },
          //data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
          data: [{
            value: "衬衫",
            textStyle: {
              color: 'green'
            }
          },{
            value: "羊毛衫",
            textStyle: {
              color: 'green'
            }
          },{
            value: "雪纺衫",
            textStyle: {
              color: 'green'
            }
          },{
            value: "裤子",
            textStyle: {
              color: 'green'
            }
          },{
            value: "高跟鞋",
            textStyle: {
              color: 'green'
            }
          },{
            value: "袜子",
            textStyle: {
              color: 'green'
            }
          }]
        },
        yAxis: {},
        series: [{
          name: '销量',
          type: 'bar',
          data: [5, 20, 36, 10, 10, 20]
        },{
          name: '销量',
          type: 'line',
          data: [5, 50, 36, 10, 30, 20]
        }]
      });*/
    },
    drawLine1(){
      let tt = this.dataX;
      let growth = [];
      for (let i=0; i<this.dataSum.length; i++) {
        let temp;
        temp = (this.dataSum[i+1] - this.dataSum[i])/this.dataSum[i];
        growth.push(temp);
      }
      /*var chart = Highcharts.chart('containers', {
        chart: {
          type: 'column'
        },
        title: {
          text: '堆叠柱形图'
        },
        xAxis: {
          categories: tt
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
      });*/
      let _this = this;
      /*var chart = new Highcharts.Chart({
        chart: {
          renderTo: 'containers',
          type: 'column',
          /!*backgroundColor: {
           linearGradient: [0, 0, 500, 500],
           stops: [
           [0, 'rgb(255, 255, 255)'],
           [1, 'rgb(200, 200, 255)']
           ]
           },*!/
          options3d: {
            enabled: true,
            alpha: 0,
            beta: 0,
            depth: 50,
            viewDistance: 25
          }
        },
        xAxis: {
          categories: tt
        },
        legend: {
          //backgroundColor: '#ccc'
        },
        colors: ['#7cb5ec', '#90ed7d'],
        title: {
          text: '注册数量'
        },
        subtitle: {
          //text: '可通过滑动下方滑块测试'
        },
        //点击事件
        plotOptions: {
          column: {
            depth: 25
          },
          series: {
            cursor: 'pointer',
            point: {
              events: {
                click: function () {
                  _this.centerDialogVisible = true;
                  _this.year = this.category;
                  console.log(this)
                }
              }
            }
          }
        },
        series: [{
          name: '注册数量',
          type: 'column',
          data: this.dataSum
        }, {
          name: '注册数量',
          type: 'line',
          data: this.dataSum
        }]
      });*/
      var chart = Highcharts.chart('containers', {
        chart: {
          zoomType: 'xy'
        },
        title: {
          text: '注册数量'
        },
        subtitle: {
          text: ''
        },
        plotOptions: {
          column: {
            depth: 25
          },
          series: {
            cursor: 'pointer',
            point: {
              events: {
                click: function () {
                  _this.centerDialogVisible = true;
                  _this.year = this.category;
                  console.log(this)
                }
              }
            }
          }
        },
        xAxis: [{
          categories: tt,
          crosshair: true
        }],
        yAxis: [{ // Primary yAxis
          labels: {
            //format: '{value}°C',
            style: {
              color: Highcharts.getOptions().colors[1]
            }
          },
          title: {
            text: '注册总数',
            style: {
              color: Highcharts.getOptions().colors[1]
            }
          }
        }, { // Secondary yAxis
          title: {
            text: '增长率',
            style: {
              color: Highcharts.getOptions().colors[0]
            }
          },
          labels: {
            //format: '{value} mm',
            style: {
              color: Highcharts.getOptions().colors[0]
            }
          },
          opposite: true
        }],
        tooltip: {
          shared: true
        },
        legend: {
          layout: 'vertical',
          align: 'left',
          x: 120,
          verticalAlign: 'top',
          y: 100,
          floating: true,
          backgroundColor: (Highcharts.theme && Highcharts.theme.legendBackgroundColor) || '#FFFFFF'
        },
        series: [{
          name: '注册总数',
          type: 'column',
          yAxis: 1,
          data: this.dataSum,
          tooltip: {
            valueSuffix: ' '
          }
        }, {
          name: '增长率',
          type: 'spline',
          data: growth,
          tooltip: {
            valueSuffix: ''
          }
        }]
      });
    },
    drawLineWork(){
      let tt = this.dataX;
      let sum = this.dataSum;
      let data = [];
      for(let i=0; i<tt.length; i++) {
        let temp = [];
        temp.push(tt[i],sum[i]);
        data.push(temp)
      }
      /*var chart = new Highcharts.Chart({
        chart: {
          renderTo: 'containerWork',
          type: 'column',
          /!*backgroundColor: {
           linearGradient: [0, 0, 500, 500],
           stops: [
           [0, 'rgb(255, 255, 255)'],
           [1, 'rgb(200, 200, 255)']
           ]
           },*!/
          options3d: {
            enabled: true,
            alpha: 0,
            beta: 0,
            depth: 50,
            viewDistance: 25
          }
        },
        xAxis: {
          categories: tt
        },
        legend: {
          //backgroundColor: '#ccc'
        },
        colors: ['#7cb5ec', '#90ed7d'],
        title: {
          text: '注册数量'
        },
        subtitle: {
          //text: '可通过滑动下方滑块测试'
        },
        plotOptions: {
          column: {
            depth: 25
          }
        },
        series: [{
          name: '图例1',
          type: 'column',
          data: this.dataSum
        }, {
          name: '图例1',
          type: 'line',
          data: this.dataSum
        }]
      });*/
      var chart = Highcharts.chart('containerWork', {
        chart: {
          type: 'pie',
          options3d: {
            enabled: true,
            alpha: 45
          },
          borderColor: 'none'
        },
        title: {
          text: '就业人数'
        },
        subtitle: {
          //text: 'Highcharts 中的3D环形图'
        },
        plotOptions: {
          pie: {
            innerSize: 100,
            depth: 45
          }
        },
        series: [{
          name: '就业人数',
          data: data,
          dataLabels: {
            style: {
              "color": "contrast",
              "fontSize": "14px",
              "fontWeight": "bold",
              "textOutline": "1px 1px contrast"
            }
          },
          /*borderColor: 'red',
          borderWidth: 10*/
        }]
      });
    },
    drawLineWorks(){
      let tt = this.dataX;
      var chart = new Highcharts.Chart({
        chart: {
          renderTo: 'containerWorks',
          type: 'column',
          /*backgroundColor: {
           linearGradient: [0, 0, 500, 500],
           stops: [
           [0, 'rgb(255, 255, 255)'],
           [1, 'rgb(200, 200, 255)']
           ]
           },*/
          options3d: {
            enabled: true,
            alpha: 0,
            beta: 0,
            depth: 50,
            viewDistance: 25
          }
        },
        xAxis: {
          categories: tt
        },
        legend: {
          //backgroundColor: '#ccc'
        },
        colors: ['#7cb5ec', '#90ed7d'],
        title: {
          text: '就业人数'
        },
        subtitle: {
          //text: '可通过滑动下方滑块测试'
        },
        plotOptions: {
          column: {
            depth: 25
          }
        },
        series: [{
          name: '就业人数',
          type: 'column',
          data: this.dataSum
        }, {
          name: '就业人数',
          type: 'line',
          data: this.dataSum
        }]
      });
    },
    drawLineMoney () {
      let tt = this.dataX;
      var chart = new Highcharts.Chart({
        chart: {
          renderTo: 'containerMoney',
          type: 'column',
          /*backgroundColor: {
           linearGradient: [0, 0, 500, 500],
           stops: [
           [0, 'rgb(255, 255, 255)'],
           [1, 'rgb(200, 200, 255)']
           ]
           },*/
          options3d: {
            enabled: true,
            alpha: 0,
            beta: 0,
            depth: 50,
            viewDistance: 25
          }
        },
        xAxis: {
          categories: tt
        },
        legend: {
          //backgroundColor: '#ccc'
        },
        colors: ['#7cb5ec','#90ed7d'],
        title: {
          text: '注册资本'
        },
        subtitle: {
          //text: '可通过滑动下方滑块测试'
        },
        plotOptions: {
          column: {
            depth: 25
          }
        },
        series: [{
          name:'注册资本',
          type: 'column',
          data: this.dataSum
        }, {
          name:'注册资本',
          type: 'line',
          data: this.dataSum
        }]
      });
      /*let tt = this.dataX;
      var chart = Highcharts.chart('containerMoney', {
        chart: {
          polar: true,
          type: 'line'
        },
        title: {
          text: '预算与支出',
          x: -80
        },
        pane: {
          size: '80%'
        },
        xAxis: {
          categories: tt,
          tickmarkPlacement: 'on',
          lineWidth: 0
        },
        yAxis: {
          gridLineInterpolation: 'polygon',
          lineWidth: 0,
          min: 0
        },
        tooltip: {
          shared: true,
          pointFormat: '<span style="color:{series.color}">{series.name}: <b>${point.y:,.0f}</b><br/>'
        },
        legend: {
          align: 'right',
          verticalAlign: 'top',
          y: 70,
          layout: 'vertical'
        },
        series: [{
          name: '预算拨款',
          data: this.dataSum,
          pointPlacement: 'on'
        }]
      });*/
    },
    drawLineMoneys () {
      let tt = this.dataX;
      var chart = new Highcharts.Chart({
        chart: {
          renderTo: 'containerMoneys',
          type: 'column',
          /*backgroundColor: {
           linearGradient: [0, 0, 500, 500],
           stops: [
           [0, 'rgb(255, 255, 255)'],
           [1, 'rgb(200, 200, 255)']
           ]
           },*/
          options3d: {
            enabled: true,
            alpha: 0,
            beta: 0,
            depth: 50,
            viewDistance: 25
          }
        },
        xAxis: {
          categories: tt
        },
        legend: {
          //backgroundColor: '#ccc'
        },
        colors: ['#7cb5ec','#90ed7d'],
        title: {
          text: '注册资本'
        },
        subtitle: {
          //text: '可通过滑动下方滑块测试'
        },
        plotOptions: {
          column: {
            depth: 25
          }
        },
        series: [{
          name:'注册资本',
          type: 'column',
          data: this.dataSum
        }, {
          name:'注册资本',
          type: 'line',
          data: this.dataSum
        }]
      });
      /*let tt = this.dataX;
       var chart = Highcharts.chart('containerMoney', {
       chart: {
       polar: true,
       type: 'line'
       },
       title: {
       text: '预算与支出',
       x: -80
       },
       pane: {
       size: '80%'
       },
       xAxis: {
       categories: tt,
       tickmarkPlacement: 'on',
       lineWidth: 0
       },
       yAxis: {
       gridLineInterpolation: 'polygon',
       lineWidth: 0,
       min: 0
       },
       tooltip: {
       shared: true,
       pointFormat: '<span style="color:{series.color}">{series.name}: <b>${point.y:,.0f}</b><br/>'
       },
       legend: {
       align: 'right',
       verticalAlign: 'top',
       y: 70,
       layout: 'vertical'
       },
       series: [{
       name: '预算拨款',
       data: this.dataSum,
       pointPlacement: 'on'
       }]
       });*/
    },
    getMap () {
      var map = Loca.create('map1', {
        mapStyle: 'amap://styles/grey',
        features: ['bg', 'road','building'],
        center: [114.00252, 22.554134],
        viewMode: '3D',
        pitch: 50,
        pitchEnable: true,
        zoom: 12
      });

      var map1 = Loca.create('map2', {
        features: ['bg', 'road','building'],
        center: [114.00252, 22.554134],
        viewMode: '3D',
        pitch: 50,
        pitchEnable: true,
        zoom: 12
      });

      //控制器
      map.on('mapload', function() {
        map.getMap().plugin(['AMap.ControlBar'], function () {
          var controlBar = new AMap.ControlBar();
          map.getMap().addControl(controlBar);
        });
      });

      map1.on('mapload', function() {
        map1.getMap().plugin(['AMap.ControlBar'], function () {
          var controlBar = new AMap.ControlBar();
          map1.getMap().addControl(controlBar);
        });
      });

      var layer = Loca.visualLayer({
        container: map,
        type: 'point',
        shape: 'circle'
      });


      layer.setOptions({
        style: {
          radius: 4,
          fill: '#b7eff7',
          lineWidth: 0.5,
          stroke: '#ffffff',
          opacity: 0.5,
        },
      });


      var layer1 = Loca.visualLayer({
        container: map1,
        type: 'heatmap',
        shape: 'normal'
      });

      layer1.setOptions({
        style: {
          radius: 20,
          opacity: [0, 0.7]
        },
        gradient: {
          0.5: 'blue',
          0.65: 'rgb(117,211,248)',
          0.7: 'rgb(0, 255, 0)',
          0.9: '#ffea00',
          1.0: 'red'
        }
      });
      /*$.get('http://10.0.10.253:8000/api/LnglatH', function (data) {


       layer.setData(data.point, {
       lnglat: 'loc',
       });

       layer1.setData(data.heatmap, {
       lnglat: 'loc',
       max:20,
       min:0,
       value: 'c'
       });

       layer.render();
       layer1.render();
       alert()

       });*/
      this.$http.get('http://10.0.10.253:8000/api/LnglatH',{params: {
        hydm: 'A',
        dq: 'all',
        year: '2015'
      }}).then(response => {
          console.log(response);
          layer.setData(response.data.point, {
            lnglat: 'loc',
          });

          layer1.setData(response.data.heatmap, {
            lnglat: 'loc',
            max:20,
            min:0,
            value: 'c'
          });

          layer.render();

          layer1.render();

        })
        .catch(function (response) {
          console.log(response);
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #myChart {
    /*background: #ccc;*/
  }
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
  .select {
    margin-bottom: 20px;
    text-align: left;
  }
  .select-info {

  }
  .select-info-option {
    /*background: red;*/
  }
  #container #containers {
    /*opacity: 0.9;*/
    /*border: 10px solid rgba(17, 17, 36, 0.5)*/
    /*display: inline-block;*/
  }
</style>
