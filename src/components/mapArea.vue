<template>
  <div >
    <div id="container" style="width: 1920px;height:930px;margin-top: 80px;z-index: 0"></div>

    <el-dialog
      title="存亡信息"
      :visible.sync="centerDialogVisibleMap"
      width="54%"
      :fullscreen='full'
      center>
      <survivalUpInfo style="margin-left: 100px" :dialog="centerDialogVisibleMap"></survivalUpInfo>
      <!--<span slot="title">
        <span style="color: #ccc;font-size: 24px;display:inline-block;margin-right:400px">消亡</span>
        <span style="color: red;font-size: 24px;display:inline-block;margin-left:400px">存活</span>
      </span>-->
    </el-dialog>

  </div>
</template>

<script type="text/ECMAScript-6">
  import Highcharts from 'highcharts/highstock';
  import HighchartsMore from 'highcharts/highcharts-more';
  import HighchartsDrilldown from 'highcharts/modules/drilldown';
  import Highcharts3D from 'highcharts/highcharts-3d';
  import survivalUpInfo from './survivalRate/survivalUpInfo';
  HighchartsMore(Highcharts)
  HighchartsDrilldown(Highcharts);
  Highcharts3D(Highcharts);
  import map from './map';
  //import liveMap from './liveMap';
  export default {
    name: 'HelloWorld',
    components: { survivalUpInfo },
    data () {
      return {
        pro: '',
        centerDialogVisibleMap: false,
        qdate: '',
        qdq: '',
        full: false,
        loading: false
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
        //创建地图
        var map = new AMap.Map('container', {
          cursor: 'default',
          //center: [114.00252, 22.654134],//地图中心点
          center: [114.15252, 22.584134],//地图中心点
          zoom: 6
        });
        let _this = this;
        //just some colors
        var colors = [
          "#3366cc", "#dc3912", "#ff9900", "#109618", "#990099", "#0099c6", "#dd4477", "#66aa00",
          "#b82e2e", "#316395", "#994499", "#22aa99", "#aaaa11", "#6633cc", "#e67300", "#8b0707",
          "#651067", "#329262", "#5574a6", "#3b3eac"
        ];

        AMapUI.loadUI(['geo/DistrictExplorer'], function (DistrictExplorer) {

          //创建一个实例
          var districtExplorer = new DistrictExplorer({
            eventSupport: true, //打开事件支持
            map: map
          });
          //定位点Marker
          var locMarker = new AMap.Marker();
          listenMouseEvents();
          function listenMouseEvents() {

            var isLocating = false;

            map.on('click', function(e) {

              if (isLocating) {
                return;
              }

              isLocating = true;

              districtExplorer.locatePosition(e.lnglat, function(err, features) {
                console.log(features)

                isLocating = false;

                if (err) {
                  console.error(err);
                  return;
                }

                /*renderFeatures(features);

                refreshLocTip(e.lnglat, features);*/

                locMarker.setPosition(e.lnglat);
                locMarker.setMap(map);
              }, {
                levelLimit: 4
              });

            });
          }

          function renderAreaNode(areaNode) {

            //绘制子区域
            districtExplorer.renderSubFeatures(areaNode, function (feature, i) {

              var fillColor = colors[i % colors.length];
              var strokeColor = colors[colors.length - 1 - i % colors.length];

              return {
                cursor: 'default',
                bubble: true,
                strokeColor: strokeColor, //线颜色
                strokeOpacity: 1, //线透明度
                strokeWeight: 1, //线宽
                fillColor: fillColor, //填充色
                fillOpacity: 0.7, //填充透明度
              };
            });

            //绘制父区域
            districtExplorer.renderParentFeature(areaNode, {
              cursor: 'default',
              bubble: true,
              strokeColor: 'black', //线颜色
              strokeOpacity: 1, //线透明度
              strokeWeight: 1, //线宽
              fillColor: null, //填充色
              fillOpacity: 0.35, //填充透明度
            });
            //feature被点击
            districtExplorer.on('featureClick', function(e, feature) {
              _this.centerDialogVisibleMap = true;
              console.log("this",this);
              console.log("areaNode",areaNode);
              var props = feature.properties;
              console.log('feature',feature)

              //如果存在子节点
              if (props.childrenNum > 0) {
                //切换聚焦区域
                switch2AreaNode(props.adcode);
              }
            });
          }

          var adcodes = [440300];

          districtExplorer.loadMultiAreaNodes(adcodes, function (error, areaNodes) {

            //清除已有的绘制内容
            districtExplorer.clearFeaturePolygons();


            for (var i = 0, len = areaNodes.length; i < len; i++) {
              renderAreaNode(areaNodes[i]);
            }

            //更新地图视野
            map.setFitView(districtExplorer.getAllFeaturePolygons());
          });

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
