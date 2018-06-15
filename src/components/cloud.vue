<template>
  <div >
    <!--<div id="containerCloud" style="width: 400px;height: 225px;display: inline-block;margin-top: -52px;box-shadow: 2px 2px 2px #888888;"></div>-->
    <div style="background: rgb(27, 31, 48);width: 400px;height: 225px;display: inline-block;margin-top: -52px;box-shadow: 2px 2px 2px #888888;cursor:pointer">
      <span style="display: inline-block;position:relative;top: 20px;color: #C0C0C0;">经营范围词云</span>
      <img src="../../static/word.png" alt="" style="width: 400px;height: 200px;display: inline-block;" @click="zoom">
    </div>
    <el-dialog
      title="经营范围词云"
      :visible.sync="dialogVisible"
      width="70%"
      top="4vh"
      :fullscreen="full"
      :modal="modal"
      :before-close="handleClose">
      <img src="../../static/wordBig.jpg" alt="" style="width: 1228px;height: 787px;display: inline-block;">
      <!--<span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
      </span>-->
    </el-dialog>
  </div>
</template>

<script type="text/ECMAScript-6">
  import Highcharts from 'highcharts/highstock';
  import HighchartsMore from 'highcharts/highcharts-more';
  import HighchartsDrilldown from 'highcharts/modules/drilldown';
  import Highcharts3D from 'highcharts/highcharts-3d';
  //import exporting from 'highcharts/modules/exporting';
  import wordcloud from 'highcharts/modules/wordcloud';
  HighchartsMore(Highcharts);
  HighchartsDrilldown(Highcharts);
  Highcharts3D(Highcharts);
  //exporting(Highcharts);
  wordcloud(Highcharts);
  export default {
    name: 'HelloWorld',
    components: {  },
    data () {
      return {
        pro: '',
        centerDialogVisibleMap: false,
        qdate: '',
        qdq: '',
        full: false,
        modal: false,
        dialogVisible: false
      }
    },
    created () {
      //this.time();
    },
    mounted(){
      //this.init();
      //this.drawLineLiveArea()
    },
    methods: {
      zoom () {
        this.dialogVisible = true;
      },
      time () {
        this.$http.get('http://10.0.10.253:8000/api/generalWordCloud').then(response => {
            console.log('response.data1',response.data);
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
        var text = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean bibendum erat ac justo sollicitudin, quis lacinia ligula fringilla. Pellentesque hendrerit, nisi vitae posuere condimentum, lectus urna accumsan libero, rutrum commodo mi lacus pretium erat. Phasellus pretium ultrices mi sed semper. Praesent ut tristique magna. Donec nisl tellus, sagittis ut tempus sit amet, consectetur eget erat. Sed ornare gravida lacinia. Curabitur iaculis metus purus, eget pretium est laoreet ut. Quisque tristique augue ac eros malesuada, vitae facilisis mauris sollicitudin. Mauris ac molestie nulla, vitae facilisis quam. Curabitur placerat ornare sem, in mattis purus posuere eget. Praesent non condimentum odio. Nunc aliquet, odio nec auctor congue, sapien justo dictum massa, nec fermentum massa sapien non tellus. Praesent luctus eros et nunc pretium hendrerit. In consequat et eros nec interdum. Ut neque dui, maximus id elit ac, consequat pretium tellus. Nullam vel accumsan lorem.';
        var data = text
          .split(/[,\. ]+/g)
          .reduce(function (arr, word) {
            var obj = arr.find(function (obj) {
              return obj.name === word;
            });
            if (obj) {
              obj.weight += 1;
            } else {
              obj = {
                name: word,
                weight: 1
              };
              arr.push(obj);
            }
            return arr;
          }, []);
        Highcharts.chart('containerCloud', {
          series: [{
            type: 'wordcloud',
            data: data
          }],
          title: {
            text: '词云图'
          }
        });
      }
    }
  }
</script>

<style>
  /*.v-modal {
    z-index: 0 !important;
  }*/
  /*.el-dialog {
    background: rgb(27, 31, 48);
  }*/
</style>
