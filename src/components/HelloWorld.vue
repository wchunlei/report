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
    <div style="width:100%;height: 80px;background: #0074D9;margin-bottom:50px;text-align: left;line-height: 80px">
      <img src="../../static/logo.png" alt="" style="display:inline-block;width:124px;height: 42px;margin: 16px 0px 0 100px;float:left">
      <div style="font-size: 30px;font-family: Microsoft Yahei; font-weight: 900; color: #ffffff;letter-spacing: 3px;display:inline-block;">深圳市行业态势发展系统</div>
    </div>
    <!--<div style="margin-top: -50px">
      <el-tabs v-model="tab" type="card" @tab-click="tabClick" style="width:100%;background: #343434;">
        <el-tab-pane label="首页" name="first"></el-tab-pane>
        <el-tab-pane label="选择行业" name="second"></el-tab-pane>
        <el-tab-pane label="选择地区" name="third"></el-tab-pane>
      </el-tabs>
    </div>-->

    <div v-if="showHomes">
      <el-carousel :interval="30000000" indicator-position="outside" height="800px"  @change="goToContent">
        <el-carousel-item v-for="item in homes" :key="item" >
          <div style="display:inline-block;margin-right:50px">
            <div>
              <img style="width: auto;height: 800px;" :src=item alt="" @click="goOn(item)"/>
            </div>
          </div>
        </el-carousel-item>
      </el-carousel>
    </div>

    <div v-show="showContent">
      <div class="select" style="margin-left: 128px">
        <!--<el-select v-model="selectBusiness" placeholder="请选择" class="select-info">
          <el-option
            v-for="item in businessOptions"
            :key="item.value"
            :label="item.label"
            :value="item.value"
            class="select-info-option">
          </el-option>
        </el-select>-->
        <el-select v-model="type" placeholder="请选择">
          <el-option
            v-for="item in typeOptions"
            :key="item.value"
            :label="item.label"
            :value="item.value">
          </el-option>
        </el-select>
        <el-select v-if="showArea" v-model="selectAllArea" placeholder="请选择">
          <el-option
            v-for="item in areaOptions"
            :key="item.value"
            :label="item.label"
            :value="item.value">
          </el-option>
        </el-select>
        <el-select v-if="showBusiness" v-model="selectBusiness" placeholder="请选择">
          <el-option-group
            v-for="group in allBusinessOptions"
            :key="group.label"
            :label="group.label">
            <el-option
              v-for="item in group.options"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-option-group>
        </el-select>
      </div>

      <el-carousel :interval="30000000" indicator-position="outside" height="700px" @change="gifPage">

        <el-carousel-item :key="item1" label="注册数量">
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
              <el-switch
                v-model="switchs"
                active-text="自动播放"
                @change="autoPlay"
                style="margin-left:20px;">
              </el-switch>
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
              <el-select v-if="showBusiness" v-model="selectArea" placeholder="请选择" class="select-info">
                <el-option
                  v-for="item in areaOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                  class="select-info-option">
                </el-option>
              </el-select>
              <el-select v-if="showArea" v-model="selectBusinessArea" placeholder="请选择">
                <el-option-group
                  v-for="group in allBusinessOptions"
                  :key="group.label"
                  :label="group.label">
                  <el-option
                    v-for="item in group.options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-option-group>
              </el-select>
            </div>
            <div id="containers" :style="{width: '800px', height: '600px'}"></div>
          </div>
        </el-carousel-item>

        <el-carousel-item :key="item2" label="参保人数">
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
              <!--<el-button v-show="auto" type="primary" round @click="autoPlay">自动播放</el-button>
              <el-button v-show="cancel" type="primary" round @click="cancelPlay">取消播放</el-button>-->
              <el-switch
                v-model="switchsWork"
                active-text="自动播放"
                @change="autoPlayWork"
                style="margin-left:20px;">
              </el-switch>
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
              <el-select v-if="showBusiness" v-model="selectWorkArea" placeholder="请选择" class="select-info">
                <el-option
                  v-for="item in areaOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                  class="select-info-option">
                </el-option>
              </el-select>
              <el-select v-if="showArea" v-model="selectWorkBusinessArea" placeholder="请选择">
                <el-option-group
                  v-for="group in allBusinessOptions"
                  :key="group.label"
                  :label="group.label">
                  <el-option
                    v-for="item in group.options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-option-group>
              </el-select>
            </div>
            <div id="containerWorks" :style="{width: '800px', height: '600px'}"></div>
          </div>
        </el-carousel-item>

        <el-carousel-item :key="item3" label="注册资本">
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
              <el-switch
                v-model="switchsMoney"
                active-text="自动播放"
                @change="autoPlayMoney"
                style="margin-left:20px;">
              </el-switch>
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
              <el-select v-if="showBusiness" v-model="selectMoneyArea" placeholder="请选择" class="select-info">
                <el-option
                  v-for="item in areaOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                  class="select-info-option">
                </el-option>
              </el-select>
              <el-select v-if="showArea" v-model="selectMoneyBusinessArea" placeholder="请选择">
                <el-option-group
                  v-for="group in allBusinessOptions"
                  :key="group.label"
                  :label="group.label">
                  <el-option
                    v-for="item in group.options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-option-group>
              </el-select>
            </div>
            <div id="containerMoneys" :style="{width: '800px', height: '600px'}"></div>
          </div>
        </el-carousel-item>

        <el-carousel-item :key="item4" label="时空变化">
          <!--<div id="myChart" :style="{width: '500px', height: '500px'}"></div>-->
          <div style="display:inline-block;margin-right:50px">
            <!--<div class="select">
              <el-select v-model="selectMoneyYear" placeholder="请选择" class="select-info">
                <el-option
                  v-for="item in yearOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                  class="select-info-option">
                </el-option>
              </el-select>
              <el-switch
                v-model="switchsMoney"
                active-text="自动播放"
                @change="autoPlayMoney"
                style="margin-left:20px;">
              </el-switch>
            </div>-->
            <div>
              <img v-if="cky" style="width: 1600px;height: 700px" src="../../static/cky.gif" alt="" :class="[isTestImg, isStop]" />
              <img v-if="dc" style="width: 1600px;height: 700px" src="../../static/dc.gif" alt="" class="testImg" />
              <img v-if="dsj" style="width: 1600px;height: 700px" src="../../static/dsj.gif" alt="" class="testImg" />
              <img v-if="jry" style="width: 1600px;height: 700px" src="../../static/jry.gif" alt="" class="testImg" />
              <img v-if="kjjr" style="width: 1600px;height: 700px" src="../../static/kjjr.gif" alt="" class="testImg" />
              <img v-if="kxyj" style="width: 1600px;height: 700px" src="../../static/kxyj.gif" alt="" class="testImg" />
              <img v-if="rgzn" style="width: 1600px;height: 700px" src="../../static/rgzn.gif" alt="" class="testImg" />
              <img v-if="ws" style="width: 1600px;height: 700px" src="../../static/ws.gif" alt="" class="testImg" />
              <img v-if="xls" style="width: 1600px;height: 700px" src="../../static/xls.gif" alt="" class="testImg" />
              <img v-if="xxcs" style="width: 1600px;height: 700px" src="../../static/xxcs.gif" alt="" class="testImg" />
              <img v-if="zl" style="width: 1600px;height: 700px" src="../../static/zl.gif" alt="" class="testImg" />
            </div>
          </div>
        </el-carousel-item>

      </el-carousel>
    </div>
    <!--<el-button v-if="showPlay" type="primary" @click="playOrPause">播放</el-button>
    <el-button v-if="showPause" type="primary"  @click="playOrPause">暂停</el-button>-->

    <el-dialog
      title="详情"
      :visible.sync="centerDialogVisible"
      width="1800px"
      :fullscreen='full'
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
      tab: 'first',
      isTestImg: 'testImg',
      isStop: 'stop',
      listLoading: true,
      centerDialogVisible: false,
      auto: true,
      cancel: false,
      switchs: false,
      switchsWork: false,
      switchsMoney: false,
      showHomes: true,
      showContent: false,
      showBusiness: true,
      showArea: false,
      showGif: false,
      showPlay: true,
      showPause: false,
      item1: 'item1',
      item2: 'item2',
      item3: 'item3',
      item4: 'item4',
      homes: ['../../static/home1.png','../../static/home2.png'],
      hydm: 'A',
      year: '1996',
      dq: 'all',
      type: '0',
      cky: false,
      dc: false,
      dsj: false,
      jry: false,
      kjjr: false,
      kxyj: false,
      rgzn: false,
      ws: false,
      xls: false,
      xxcs: true,
      zl: false,
      yearOptions: yearOptions() ,
      typeOptions: [{
        value: '0',
        label: '行业'
      },{
        value: '1',
        label: '地区'
      }],
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
      allBusinessOptions: [{
        label: '全部产业',
        options: [{
          value: 'all',
          label: '全部行业'
        },{
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
        }]
      }, {
        label: '关注产业',
        options: [{
          value: 'rgzn',
          label: '人工智能'
        }, {
          value: 'dsj',
          label: '大数据'
        }, {
          value: 'kjjr',
          label: '科技金融'
        }, {
          value: 'xls',
          label: '新零售'
        }]
      }],
      businessOptions: [{
        value: 'all',
        label: '全部行业'
      },{
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
      selectAllArea: 'all',
      selectBusiness: 'all',
      selectBusinessArea: 'all',
      selectYear: 'all',
      selectArea: 'all',
      selectWorkYear: 'all',
      selectWorkArea: 'all',
      selectWorkBusinessArea:'all',
      selectMoneyYear: 'all',
      selectMoneyArea: 'all',
      selectMoneyBusinessArea: 'all',
      msg: 'Welcome to Your Vue.js App',
      dataX: [],
      dataSum: [],
      registTotal: 0,
      dateString: '',
      full: true
    }
  },
  created () {
    //this.time();
    //this.hydm = 'B';
  },
  watch: {
    "type" (newval,oldval) {
      if (newval == '0') {
        this.showBusiness = true;
        this.showArea = false;
      } else {
        this.showBusiness = false;
        this.showArea = true;
      }
    },
    "selectYear" (newval,oldval) {
      if(this.type == '0') {
        this.time(newval);
        this.workTime(newval);
        this.moneyTime(newval);
        this.selectWorkYear = newval;
        this.selectMoneyYear = newval;
      } else {
        this.time1(newval);
        this.workTime1(newval);
        this.moneyTime1(newval);
        this.selectWorkYear = newval;
        this.selectMoneyYear = newval;
      }
    },
    "selectArea" (newval,oldval) {
      this.area(newval);
      this.workArea(newval);
      this.moneyArea(newval);
      this.selectWorkArea = newval;
      this.selectMoneyArea = newval;
    },
    "selectBusinessArea" (newval,oldval) {
      this.area1(newval);
      this.workArea1(newval);
      this.moneyArea1(newval);
      this.selectWorkBusinessArea = newval;
      this.selectMoneyBusinessArea = newval;
    },
    "selectWorkYear" (newval,oldval) {
      if(this.type == '0') {
        this.time(newval);
        this.workTime(newval);
        this.moneyTime(newval);
        this.selectYear = newval;
        this.selectMoneyYear = newval;
      } else {
        this.time1(newval);
        this.workTime1(newval);
        this.moneyTime1(newval);
        this.selectYear = newval;
        this.selectMoneyYear = newval;
      }
    },
    "selectWorkArea" (newval,oldval) {
      this.area(newval);
      this.workArea(newval);
      this.moneyArea(newval);
      this.selectArea = newval;
      this.selectMoneyArea = newval;
    },
    "selectWorkBusinessArea" (newval,oldval) {
      this.area1(newval);
      this.workArea1(newval);
      this.moneyArea1(newval);
      this.selectBusinessArea = newval;
      this.selectMoneyBusinessArea = newval;
    },
    "selectMoneyYear" (newval,oldval) {
      if(this.type == '0') {
        this.time(newval);
        this.workTime(newval);
        this.moneyTime(newval);
        this.selectYear = newval;
        this.selectWorkYear = newval;
      } else {
        this.time1(newval);
        this.workTime1(newval);
        this.moneyTime1(newval);
        this.selectYear = newval;
        this.selectWorkYear = newval;
      }
    },
    "selectMoneyArea" (newval,oldval) {
      this.area(newval);
      this.workArea(newval);
      this.moneyArea(newval);
      this.selectArea = newval;
      this.selectWorkArea = newval;
    },
    "selectMoneyBusinessArea" (newval,oldval) {
      this.area1(newval);
      this.workArea1(newval);
      this.moneyArea1(newval);
      this.selectWorkBusinessArea = newval;
      this.selectMoneyBusinessArea = newval;
    },
    "selectAllArea" (newval,oldval) {
      console.log(newval)
      //this.dq = newval;
      if (this.selectYear == 'all') {
        this.time1('all');
      } else {
        this.time1(this.selectYear);
      }
      if (this.selectBusinessArea == 'all') {
        this.area1('all');
      } else {
        this.area1(this.selectBusinessArea);
      }
      if (this.selectWorkYear == 'all') {
        this.workTime1('all');
      } else {
        this.workTime1(this.selectWorkYear);
      }
      if (this.selectWorkBusinessArea == 'all') {
        this.workArea1('all');
      } else {
        this.workArea1(this.selectWorkBusinessArea);
      }
      if (this.selectMoneyYear == 'all') {
        this.moneyTime1('all');
      } else {
        this.moneyTime1(this.selectMoneyYear);
      }
      if (this.selectMoneyBusinessArea == 'all') {
        this.moneyArea1('all');
      } else {
        this.moneyArea1(this.selectMoneyBusinessArea);
      }
    },
    "selectBusiness" (newval,oldval) {
      console.log(newval)
      //this.hydm = newval;
      if (this.selectYear == 'all') {
        this.time('all');
      } else {
        this.time(this.selectYear);
      }
      if (this.selectArea == 'all') {
        this.area('all');
      } else {
        this.time(this.selectArea);
      }
      if (this.selectWorkYear == 'all') {
        this.workTime('all');
      } else {
        this.workTime(this.selectWorkYear);
      }
      if (this.selectWorkArea == 'all') {
        this.workArea('all');
      } else {
        this.workArea(this.selectWorkArea);
      }
      if (this.selectMoneyYear == 'all') {
        this.moneyTime('all');
      } else {
        this.moneyTime(this.selectMoneyYear);
      }
      if (this.selectMoneyArea == 'all') {
        this.moneyArea('all');
      } else {
        this.moneyArea(this.selectMoneyArea);
      }
      //this.intelTime('all');
      if (newval == 'B') {
        this.cky = true;
        this.dc = false;
        this.dsj = false;
        this.jry = false;
        this.kjjr = false;
        this.kxyj = false;
        this.rgzn = false;
        this.ws = false;
        this.xls = false;
        this.xxcs = false;
        this.zl = false;
      }
      if (newval == 'K') {
        this.cky = false;
        this.dc = true;
        this.dsj = false;
        this.jry = false;
        this.kjjr = false;
        this.kxyj = false;
        this.rgzn = false;
        this.ws = false;
        this.xls = false;
        this.xxcs = false;
        this.zl = false;
      }
      if (newval == 'I') {
        this.cky = false;
        this.dc = false;
        this.dsj = false;
        this.jry = false;
        this.kjjr = false;
        this.kxyj = false;
        this.rgzn = false;
        this.ws = false;
        this.xls = false;
        this.xxcs = true;
        this.zl = false;
      }
      if (newval == 'J') {
        this.cky = false;
        this.dc = false;
        this.dsj = false;
        this.jry = true;
        this.kjjr = false;
        this.kxyj = false;
        this.rgzn = false;
        this.ws = false;
        this.xls = false;
        this.xxcs = false;
        this.zl = false;
      }
      if (newval == 'M') {
        this.cky = false;
        this.dc = false;
        this.dsj = false;
        this.jry = false;
        this.kjjr = false;
        this.kxyj = true;
        this.rgzn = false;
        this.ws = false;
        this.xls = false;
        this.xxcs = false;
        this.zl = false;
      }
      if (newval == 'dsj') {
        this.cky = false;
        this.dc = false;
        this.dsj = true;
        this.jry = false;
        this.kjjr = false;
        this.kxyj = false;
        this.rgzn = false;
        this.ws = false;
        this.xls = false;
        this.xxcs = false;
        this.zl = false;
      }
      if (newval == 'rgzn') {
        this.cky = false;
        this.dc = false;
        this.dsj = false;
        this.jry = false;
        this.kjjr = false;
        this.kxyj = false;
        this.rgzn = true;
        this.ws = false;
        this.xls = false;
        this.xxcs = false;
        this.zl = false;
      }
      if (newval == 'kjjr') {
        this.cky = false;
        this.dc = false;
        this.dsj = false;
        this.jry = false;
        this.kjjr = true;
        this.kxyj = false;
        this.rgzn = false;
        this.ws = false;
        this.xls = false;
        this.xxcs = false;
        this.zl = false;
      }
      if (newval == 'xls') {
        this.cky = false;
        this.dc = false;
        this.dsj = false;
        this.jry = false;
        this.kjjr = false;
        this.kxyj = false;
        this.rgzn = false;
        this.ws = false;
        this.xls = true;
        this.xxcs = false;
        this.zl = false;
      }
      if (newval == 'L') {
        this.cky = false;
        this.dc = false;
        this.dsj = false;
        this.jry = false;
        this.kjjr = false;
        this.kxyj = false;
        this.rgzn = false;
        this.ws = false;
        this.xls = false;
        this.xxcs = false;
        this.zl = true;
      }
      if (newval == 'Q') {
        this.cky = false;
        this.dc = false;
        this.dsj = false;
        this.jry = false;
        this.kjjr = false;
        this.kxyj = false;
        this.rgzn = false;
        this.ws = true;
        this.xls = false;
        this.xxcs = false;
        this.zl = false;
      }
    }
  },
  mounted(){
    this.time('all');
    this.area('all');
    this.workTime('all');
    this.workArea('all');
    this.moneyTime('all');
    this.moneyArea('all');
    //this.intelTime('all');
    this.drawLine();
    this.drawLine1();
    this.drawLineWork();
    this.drawLineWorks();
    this.drawLineMoney();
    this.drawLineMoneys();
  },
  methods: {
    tabClick(tab, event) {
      console.log(tab,event);
    },
    gifPage (val) {
      if (val == '3') {
        this.showGif = true;
      } else {
        this.showGif = false;
      }
    },
    playOrPause() {
      if ('getContext' in document.createElement('canvas')) {
        HTMLImageElement.prototype.play = function() {
          if (this.storeCanvas) {
            // 移除存储的canvas
            this.storeCanvas.parentElement.removeChild(this.storeCanvas);
            this.storeCanvas = null;
            // 透明度还原
            image.style.opacity = '';
          }
          if (this.storeUrl) {
            this.src = this.storeUrl;
          }
        };
        HTMLImageElement.prototype.stop = function() {
          var canvas = document.createElement('canvas');
          // 尺寸
          var width = this.width, height = this.height;
          if (width && height) {
            // 存储之前的地址
            if (!this.storeUrl) {
              this.storeUrl = this.src;
            }
            // canvas大小
            canvas.width = width;
            canvas.height = height;
            // 绘制图片帧（第一帧）
            canvas.getContext('2d').drawImage(this, 0, 0, width, height);
            // 重置当前图片
            try {
              this.src = canvas.toDataURL("image/gif");
            } catch(e) {
              // 跨域
              this.removeAttribute('src');
              // 载入canvas元素
              canvas.style.position = 'absolute';
              // 前面插入图片
              this.parentElement.insertBefore(canvas, this);
              // 隐藏原图
              this.style.opacity = '0';
              // 存储canvas
              this.storeCanvas = canvas;
            }
          }
        };
      }
      let image = document.getElementsByClassName("testImg");
      if (this.showPlay) {
        $('.testImg').stop();
        this.showPlay = false;
        this.showPause =true;
      } else {
        image.play();
        this.showPlay = true;
        this.showPause =false;
      }
    },
    goOn(val) {
      if(val == this.homes[1]) {
        this.showHomes = false;
        this.showContent = true;
      }
    },
    goToContent(value) {
      if(value == 2) {
        let _this = this;
        setTimeout(function(){
          _this.showHomes = false;
          _this.showContent = true;
        },2000)
      }
    },
    autoPlay () {
      let _this = this;
      let year = 1995;
      let time = setInterval(function(){
        console.log('year1',year);
        if(_this.type == '0') {
          _this.time(year);
        } else{
          _this.time1(year);
        }
        _this.selectYear = parseInt(year) + 1;
        year = parseInt(year) + 1;
        console.log('year2',year);
        if (!_this.switchs || year>2015) {
          console.log(clearInterval(time));
          clearInterval(time);
        }
      },2000);
      /*this.auto = false;
       this.cancel = true;
       return function temp() {
       return time;
       }*/
    },
    autoPlayWork () {
      let _this = this;
      let year = 1995;
      let time = setInterval(function(){
        console.log('year1',year);
        if(_this.type == '0') {
          _this.workTime(year);
        } else{
          _this.workTime1(year);
        }
        _this.selectWorkYear = parseInt(year) + 1;
        year = parseInt(year) + 1;
        console.log('year2',year);
        if (!_this.switchsWork || year>2015) {
          console.log(clearInterval(time));
          clearInterval(time);
        }
      },2000);
      /*this.auto = false;
      this.cancel = true;
      return function temp() {
        return time;
      }*/
    },
    /*cancelPlay () {
      this.auto = true;
      this.cancel = false;
      let temp = this.autoPlay();
      clearInterval(temp);
    },*/
    autoPlayMoney () {
      let _this = this;
      let year = 1995;
      let time = setInterval(function(){
        console.log('year1',year);
        if(_this.type == '0') {
          _this.moneyTime(year);
        } else {
          _this.moneyTime1(year);
        }
        _this.selectMoneyYear = parseInt(year) + 1;
        year = parseInt(year) + 1;
        console.log('year2',year);
        if (!_this.switchsMoney || year>2015) {
          console.log(clearInterval(time));
          clearInterval(time);
        }
      },2000);
      /*this.auto = false;
       this.cancel = true;
       return function temp() {
       return time;
       }*/
    },
    time (newval) {
      for(let i=0; i<this.allBusinessOptions[0].options.length; i++) {
        if(this.allBusinessOptions[0].options[i].value == this.selectBusiness) {
          this.$http.get('http://10.0.10.253:8000/api/data',{params: {
            item: 'snum',
            hydm: this.selectBusiness,
            year: newval
          }}).then(response => {
              console.log('response.data',response.data);
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
        }
      }
      for(let i=0; i<this.allBusinessOptions[1].options.length; i++) {
        if(this.allBusinessOptions[1].options[i].value == this.selectBusiness) {
          this.$http.get('http://10.0.10.253:8000/api/gzcy',{params: {
            item: 'snum',
            hydm: this.selectBusiness,
            year: newval
          }}).then(response => {
              console.log('response.data',response.data);
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
        }
      }
    },
    time1 (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'snum',
        dq: this.selectAllArea,
        year: newval
      }}).then(response => {
          console.log('response.data',response.data);
          if (this.dataX) {
            this.dataX = [];
          }
          if (this.dataSum) {
            this.dataSum = [];
          }
          response.data.map(arr=>{
            this.dataX.push(arr.shydm);
            this.dataSum.push(arr.num);
          })
          this.drawLine();
        })
        .catch(function (response) {
          console.log(response);
        });
    },
    intelTime (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'snum',
        rgzn: this.selectBusiness,
        year: newval
      }}).then(response => {
          console.log('response.data',response.data);
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
      for(let i=0; i<this.allBusinessOptions[0].options.length; i++) {
        if(this.allBusinessOptions[0].options[i].value == this.selectBusiness) {
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
              if (this.registTotal) {
                this.registTotal = 0;
              }
              response.data.map(arr=>{
                this.dataX.push(arr.syear);
                this.dataSum.push(arr.num);
                this.registTotal += arr.num;
              })
            //console.log('all',this.registTotal)
              this.drawLine1();
            })
            .catch(function (response) {
              console.log(response);
            });
        }
      }
      for(let i=0; i<this.allBusinessOptions[1].options.length; i++) {
        if(this.allBusinessOptions[1].options[i].value == this.selectBusiness) {
          this.$http.get('http://10.0.10.253:8000/api/gzcy',{params: {
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
        }
      }
    },
    area1 (newval) {
      for(let i=0; i<this.allBusinessOptions[0].options.length; i++) {
        if(this.allBusinessOptions[0].options[i].value == newval) {
          this.$http.get('http://10.0.10.253:8000/api/data',{params: {
            item: 'snum',
            hydm: newval,
            dq: this.selectAllArea
          }}).then(response => {
              console.log(response.data);
              if (this.dataX) {
                this.dataX = [];
              }
              if (this.dataSum) {
                this.dataSum = [];
              }
              if (this.registTotal) {
                this.registTotal = 0;
              }
              response.data.map(arr=>{
                this.dataX.push(arr.syear);
                this.dataSum.push(arr.num);
                this.registTotal += arr.num;
              })
              //console.log('all',this.registTotal)
              this.drawLine1();
            })
            .catch(function (response) {
              console.log(response);
            });
        }
      }
      for(let i=0; i<this.allBusinessOptions[1].options.length; i++) {
        if(this.allBusinessOptions[1].options[i].value == newval) {
          this.$http.get('http://10.0.10.253:8000/api/gzcy',{params: {
            item: 'snum',
            hydm: newval,
            dq: this.selectAllArea
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
        }
      }
    },
    workTime (newval) {
      for(let i=0; i<this.allBusinessOptions[0].options.length; i++) {
        if(this.allBusinessOptions[0].options[i].value == this.selectBusiness) {
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
              });
              this.drawLineWork();
            })
            .catch(function (response) {
              console.log(response);
            });
        }
      }
      for(let i=0; i<this.allBusinessOptions[1].options.length; i++) {
        if(this.allBusinessOptions[1].options[i].value == this.selectBusiness) {
          this.$http.get('http://10.0.10.253:8000/api/gzcy',{params: {
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
              });
              this.drawLineWork();
            })
            .catch(function (response) {
              console.log(response);
            });
        }
      }
    },
    workTime1 (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'renshu',
        dq: this.selectAllArea,
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
            this.dataX.push(arr.chydm);
            this.dataSum.push(arr.num);
          });
          this.drawLineWork();
        })
        .catch(function (response) {
          console.log(response);
        });
    },
    workArea (newval) {
      for(let i=0; i<this.allBusinessOptions[0].options.length; i++) {
        if(this.allBusinessOptions[0].options[i].value == this.selectBusiness) {
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
        }
      }
      for(let i=0; i<this.allBusinessOptions[1].options.length; i++) {
        if(this.allBusinessOptions[1].options[i].value == this.selectBusiness) {
          this.$http.get('http://10.0.10.253:8000/api/gzcy',{params: {
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
        }
      }
    },
    workArea1 (newval) {
      for(let i=0; i<this.allBusinessOptions[0].options.length; i++) {
        if(this.allBusinessOptions[0].options[i].value == newval) {
          this.$http.get('http://10.0.10.253:8000/api/data',{params: {
            item: 'renshu',
            hydm: newval,
            dq: this.selectAllArea
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
        }
      }
      for(let i=0; i<this.allBusinessOptions[1].options.length; i++) {
        if(this.allBusinessOptions[1].options[i].value == newval) {
          this.$http.get('http://10.0.10.253:8000/api/gzcy',{params: {
            item: 'renshu',
            hydm: newval,
            dq: this.selectAllArea
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
        }
      }
    },
    moneyTime (newval) {
      for(let i=0; i<this.allBusinessOptions[0].options.length; i++) {
        if(this.allBusinessOptions[0].options[i].value == this.selectBusiness) {
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
        }
      }
      for(let i=0; i<this.allBusinessOptions[1].options.length; i++) {
        if(this.allBusinessOptions[1].options[i].value == this.selectBusiness) {
          this.$http.get('http://10.0.10.253:8000/api/gzcy',{params: {
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
        }
      }
    },
    moneyTime1 (newval) {
      this.$http.get('http://10.0.10.253:8000/api/data',{params: {
        item: 'zczb',
        dq: this.selectAllArea,
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
            this.dataX.push(arr.shydm);
            this.dataSum.push(arr.num);
          })
          this.drawLineMoney();
        })
        .catch(function (response) {
          console.log(response);
        });
    },
    moneyArea (newval) {
      for(let i=0; i<this.allBusinessOptions[0].options.length; i++) {
        if(this.allBusinessOptions[0].options[i].value == this.selectBusiness) {
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
        }
      }
      for(let i=0; i<this.allBusinessOptions[1].options.length; i++) {
        if(this.allBusinessOptions[1].options[i].value == this.selectBusiness) {
          this.$http.get('http://10.0.10.253:8000/api/gzcy',{params: {
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
        }
      }
    },
    moneyArea1 (newval) {
      for(let i=0; i<this.allBusinessOptions[0].options.length; i++) {
        if(this.allBusinessOptions[0].options[i].value == newval) {
          this.$http.get('http://10.0.10.253:8000/api/data',{params: {
            item: 'zczb',
            hydm: newval,
            dq: this.selectAllArea
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
        }
      }
      for(let i=0; i<this.allBusinessOptions[1].options.length; i++) {
        if(this.allBusinessOptions[1].options[i].value == newval) {
          this.$http.get('http://10.0.10.253:8000/api/gzcy',{params: {
            item: 'zczb',
            hydm: newval,
            dq: this.selectAllArea
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
        }
      }
    },
    drawLine(){
      let tt = this.dataX;
      let _this = this;
      var chart = Highcharts.chart('containerA', {
        chart: {
          polar: true,
          type: 'line'
        },
        title: {
          text: '注册数量',
          //x: -80
        },
        pane: {
          size: '80%'
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
                  if(_this.type == '0') {
                    _this.selectArea = this.category;
                    _this.area(this.category);
                  } else {
                    /*_this.selectBusinessArea = this.category;
                    _this.area1(this.category);*/
                  }
                  console.log(this)
                }
              }
            }
          }
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
      let growth = [0];
      for (let i=0; i<this.dataSum.length; i++) {
        let temp;
        if (this.dataSum[i+1]) {
          temp = (this.dataSum[i+1] - this.dataSum[i])/this.dataSum[i];
          growth.push(temp);
        }
      }
      //console.log(growth)
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
          text: '注册数量/总数：'+this.registTotal
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
            text: '增长率',
            style: {
              color: Highcharts.getOptions().colors[1]
            }
          }
        }, { // Secondary yAxis
          title: {
            text: '注册数量',
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
          name: '注册数量',
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
      let _this =this;
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
          text: '参保人数'
        },
        subtitle: {
          //text: 'Highcharts 中的3D环形图'
        },
        plotOptions: {
          pie: {
            innerSize: 100,
            depth: 45
          },
          /*series: {
            animation: false
          }*/
          series: {
            animation: false,
            cursor: 'pointer',
            point: {
              events: {
                click: function () {
                  if(_this.type == '0') {
                    _this.selectWorkArea = this.name;
                    _this.workArea(this.name);
                  } else {
                    /*_this.selectWorkArea = this.name;
                    _this.workArea1(this.name);*/
                  }
                }
              }
            }
          }
        },
        series: [{
          name: '参保人数',
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
      let growth = [0];
      for (let i=0; i<this.dataSum.length; i++) {
        let temp;
        if (this.dataSum[i+1]) {
          temp = (this.dataSum[i+1] - this.dataSum[i])/this.dataSum[i];
          growth.push(temp);
        }
      }
      //console.log(growth)
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
      var chart = Highcharts.chart('containerWorks', {
        chart: {
          zoomType: 'xy'
        },
        title: {
          text: '参保人数'
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
            /*point: {
              events: {
                click: function () {
                  _this.centerDialogVisible = true;
                  _this.year = this.category;
                  console.log(this)
                }
              }
            }*/
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
            text: '增长率',
            style: {
              color: Highcharts.getOptions().colors[1]
            }
          }
        }, { // Secondary yAxis
          title: {
            text: '参保人数',
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
          name: '参保人数',
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
    /*drawLineWorks(){
      let tt = this.dataX;
      var chart = new Highcharts.Chart({
        chart: {
          renderTo: 'containerWorks',
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
          text: '参保人数'
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
          name: '参保人数',
          type: 'column',
          data: this.dataSum
        }, {
          name: '参保人数',
          type: 'line',
          data: this.dataSum
        }]
      });
    },*/
    drawLineMoney () {
      let tt = this.dataX;
      let _this = this;
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
          },
          series: {
            animation: false,
            cursor: 'pointer',
            point: {
              events: {
                click: function () {
                  if(_this.type == '0') {
                    _this.selectMoneyArea = this.category;
                    _this.moneyArea(this.category);
                  } else {
                    console.log(this.category)
                  }
                }
              }
            }
          }
        },
        series: [{
          name:'注册资本',
          type: 'column',
          data: this.dataSum
        }, /*{
          name:'注册资本',
          type: 'line',
          data: this.dataSum
        }*/]
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
    drawLineMoneys(){
      let tt = this.dataX;
      let growth = [0];
      for (let i=0; i<this.dataSum.length; i++) {
        let temp;
        if (this.dataSum[i+1]) {
          temp = (this.dataSum[i+1] - this.dataSum[i])/this.dataSum[i];
          growth.push(temp);
        }
      }
      //console.log(growth)
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
      var chart = Highcharts.chart('containerMoneys', {
        chart: {
          zoomType: 'xy'
        },
        title: {
          text: '注册资本'
        },
        subtitle: {
          text: ''
        },
        plotOptions: {
          column: {
            depth: 25
          },
          /*series: {
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
          }*/
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
            text: '增长率',
            style: {
              color: Highcharts.getOptions().colors[1]
            }
          }
        }, { // Secondary yAxis
          title: {
            text: '注册资本',
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
          name: '注册资本',
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
    /*drawLineMoneys () {
      let tt = this.dataX;
      var chart = new Highcharts.Chart({
        chart: {
          renderTo: 'containerMoneys',
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
      /!*let tt = this.dataX;
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
       });*!/
    },*/
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
  .stop {
    animation-play-state: paused;
  }

</style>

<style>
  .highcharts-credits {
    display: none;
  }
</style>
