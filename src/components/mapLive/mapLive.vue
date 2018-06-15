<template>
  <div class="hello">
    <div style="text-align: center; ">
      <!--<img v-show="loading" src="../../static/timg.gif"/>-->
      <!--<i class="el-icon-loading"></i>-->
      <div v-show="loading" style="background: #fff;width: 1300px; height: 680px;z-index: 998;position:absolute;opacity: 0.5;">
        <div v-show="loading" style="position:absolute;z-index: 999; width: 1300px;height:680px;opacity: 0.8;background: url(../../static/timg.gif) no-repeat center center fixed;"></div>
      </div>
      <div id="map1" style="width: 600px;height:680px;display:inline-block"></div>
      <div id="map2" style="width: 600px;height:680px;display:inline-block"></div>
    </div>
  </div>
</template>

<script type="text/ECMAScript-6">
  export default {
    name: 'HelloWorld',
    props: ['qdate', 'qdq', 'dialog', 'type' ],
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
        yearOptions: yearOptions(),
        loading: true,
        mapShow1: false,
        mapShow2: false
      }
    },
    created () {
      //alert(this.hydm)
    },
    mounted () {
      //this.initMap();
      this.getMapInfo();
    },
    watch: {
      "dialog" (newval,oldval) {
        if (newval) {
          this.loading = true;
          this.getMapInfo();
        }
      }
    },
    methods: {
      initMap () {
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
          mapStyle: 'amap://styles/grey',
          features: ['bg', 'road','building'],
          center: [114.00252, 22.554134],
          viewMode: '3D',
          pitch: 50,
          pitchEnable: true,
          zoom: 12
        });

        /*var map1 = Loca.create('map2', {
          features: ['bg', 'road','building'],
          center: [114.00252, 22.554134],
          viewMode: '3D',
          pitch: 50,
          pitchEnable: true,
          zoom: 12
        });*/

        //控制器
        map.on('mapload', function() {
          map.getMap().plugin(['AMap.ControlBar'], function () {
            var controlBar = new AMap.ControlBar();
            map.getMap().addControl(controlBar);
          });
        });
        map1.on('mapload', function() {
          map.getMap().plugin(['AMap.ControlBar'], function () {
            var controlBar = new AMap.ControlBar();
            map.getMap().addControl(controlBar);
          });
        });

        /*map1.on('mapload', function() {
          map1.getMap().plugin(['AMap.ControlBar'], function () {
            var controlBar = new AMap.ControlBar();
            map1.getMap().addControl(controlBar);
          });
        });*/

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
          container: map,
          type: 'point',
          shape: 'circle'
        });
        layer1.setOptions({
          style: {
            radius: 4,
            fill: '#b7eff7',
            lineWidth: 0.5,
            stroke: '#ffffff',
            opacity: 0.5,
          },
        });

        /*var layer1 = Loca.visualLayer({
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
        });*/
      },
      getMapInfo () {
        var map = Loca.create('map1', {
          mapStyle: 'amap://styles/grey',
          features: ['bg', 'road','building'],
          //center: [114.119593, 22.626881],
          center: [114.00252, 22.554134],
          /*viewMode: '3D',
          pitch: 50,
          pitchEnable: true,*/
          zoom: 12
          //zoom: 11
        });
        var map1 = Loca.create('map2', {
          mapStyle: 'amap://styles/grey',
          features: ['bg', 'road','building'],
          //center: [114.119593, 22.626881],
          center: [114.00252, 22.554134],
          /*viewMode: '3D',
           pitch: 50,
           pitchEnable: true,*/
          zoom: 12
          //zoom: 11
        });

        /*var map1 = Loca.create('map2', {
          features: ['bg', 'road','building'],
          center: [114.00252, 22.554134],
          viewMode: '3D',
          pitch: 50,
          pitchEnable: true,
          zoom: 12
        });*/

        //控制器
        /*map.on('mapload', function() {
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
        });*/

        var layer = Loca.visualLayer({
          container: map,
          type: 'point',
          shape: 'circle'
        });
        layer.setOptions({
          style: {
            radius: 1,
            fill: 'red',
            /*lineWidth: 0.5,
            stroke: '#ffffff',*/
            opacity: 1
          },
        });
        var layer1 = Loca.visualLayer({
          container: map1,
          type: 'point',
          shape: 'circle'
        });
        layer1.setOptions({
          style: {
            radius: 1,
            fill: 'green',
            /*lineWidth: 0.5,
             stroke: '#ffffff',*/
            opacity: 1
          },
        });

        /*var layer1 = Loca.visualLayer({
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
        });*/
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
        let urlLive = 'http://10.0.10.253:8000/api/liveL';
        let urlAbnormal = 'http://10.0.10.253:8000/api/abnormalL';
        if (this.type == 1) {
          urlLive = 'http://10.0.10.253:8000/api/liveL';
          urlAbnormal = 'http://10.0.10.253:8000/api/abnormalL';
        } else {
          urlLive = 'http://10.0.10.253:8000/api/liveLZ';
          urlAbnormal = 'http://10.0.10.253:8000/api/abnormalLZ';
        }
        this.$http.get(urlAbnormal,{params: {
          qdate: this.qdate,
          qdq: this.qdq
        }}).then(response => {
          console.log(response);
          layer.setData(response.data.point, {
            lnglat: 'loc',
          });
          /*layer1.setData(response.data.heatmap, {
            lnglat: 'loc',
            max:20,
            min:0,
            value: 'c'
          });*/
          layer.render();
          //layer1.render();
          this.loading = false;
          /*if (!this.loading) {
            this.mapShow1 = true;
            this.mapShow2 = true;
          }*/
        })
        .catch(function (response) {
          console.log(response);
        });
        this.$http.get(urlLive,{params: {
          qdate: this.qdate,
          qdq: this.qdq
        }}).then(response => {
            console.log(response);
            layer1.setData(response.data.point, {
              lnglat: 'loc',
            });
            /*layer1.setData(response.data.heatmap, {
              lnglat: 'loc',
              max:20,
              min:0,
              value: 'c'
            });
            layer.render();*/
            layer1.render();
            this.loading = false;
            /*if (!this.loading) {
             this.mapShow1 = true;
             this.mapShow2 = true;
             }*/
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
  html, body {
    margin: 0;
    height: 100%;
    width: 100%;
    position: absolute;
  }

  #container {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
  }

  .button-group {
    position: absolute;
    bottom: 20px;
    right: 20px;
    font-size: 12px;
    padding: 10px;
  }

  .button-group .button {
    height: 28px;
    line-height: 28px;
    background-color: #0D9BF2;
    color: #FFF;
    border: 0;
    outline: none;
    padding-left: 5px;
    padding-right: 5px;
    border-radius: 3px;
    margin-bottom: 4px;
    cursor: pointer;
  }
  .button-group .inputtext {
    height: 26px;
    line-height: 26px;
    border: 1px;
    outline: none;
    padding-left: 5px;
    padding-right: 5px;
    border-radius: 3px;
    margin-bottom: 4px;
    cursor: pointer;
  }
  /*
 .tip {
     position: absolute;
     bottom: 30px;
     right: 10px;
     background-color: #FFF;
     text-align: center;
     border: 1px solid #ccc;
     line-height: 30px;
     border-radius: 3px;
     padding: 0 5px;
     font-size: 12px;
 }
 */
  #tip {
    background-color: #fff;
    padding-left: 10px;
    padding-right: 10px;
    position: absolute;
    font-size: 12px;
    right: 10px;
    top: 20px;
    border-radius: 3px;
    border: 1px solid #ccc;
    line-height: 30px;
  }

  /*
  #tip input[type='button'] {
      margin-top: 10px;
      margin-bottom: 10px;
      background-color: #0D9BF2;
      height: 30px;
      text-align: center;
      line-height: 30px;
      color: #fff;
      font-size: 12px;
      border-radius: 3px;
      outline: none;
      border: 0;
  }
  */
  .amap-info-content {
    font-size: 12px;
  }

  #myPageTop {
    position: absolute;
    top: 5px;
    right: 10px;
    background: #fff none repeat scroll 0 0;
    border: 1px solid #ccc;
    margin: 10px auto;
    padding:6px;
    font-family: "Microsoft Yahei", "微软雅黑", "Pinghei";
    font-size: 14px;
  }
  #myPageTop label {
    margin: 0 20px 0 0;
    color: #666666;
    font-weight: normal;
  }
  #myPageTop input {
    width: 170px;
  }
  #myPageTop .column2{
    padding-left: 25px;
  }
</style>
