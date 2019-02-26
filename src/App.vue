<template>
    <div class="amap-page-container">
      <el-amap vid="amap" :plugin="plugin" class="amap-demo" :center="center">
      </el-amap>
  <!-- 作者：于天源  -->
      <h1>天气获取-Demo</h1>
      <div class="toolbar">
        <span v-if="loaded">
          location: lng = {{ lng }} lat = {{ lat }}
          <p>获取当前所在位置的经纬度</p>
        </span>
        <span v-else>正在定位</span>
        <!-- 按钮 -->
        <el-button @click="getWeather" type="primary">获取天气</el-button>
        <el-button @click="getWeather15" type="primary">获取未来15天气</el-button>
        <!-- info -->
        <div>所在位置：{{result}}</div>
        <div>所在城市：{{cty.pname}}&nbsp;{{cty.name}}</div>
        <!-- 天气 -->
        <el-table :data="hourly" border style="width:100%" >
          <el-table-column  label="时" align="center">
            <template slot-scope="info">
              <el-tag>{{info.row.hour}}时</el-tag>
            </template>
          </el-table-column>
          <el-table-column prop="condition" label="天气" align="center"></el-table-column>
        </el-table>
        <el-row>
          <h2>未来十五天天气</h2>
        </el-row>
        <el-table :data="forecast" border style="width: 50%">
          <el-table-column prop="conditionDay" label="天气状况"  width="180" align="center"></el-table-column>
          <el-table-column prop="tempDay" label="白天最高温度"  width="180" align="center"></el-table-column>
          <el-table-column prop="tempNight" label="夜间最高温度"  width="180" align="center"></el-table-column>
          <el-table-column prop="predictDate" label="日期"  width="180" align="center"></el-table-column>
          <el-table-column prop="updatetime" label="上次天气更新时间" align="center"></el-table-column>
        </el-table>
      </div>
    </div>
  </template>

  <style>
    .amap-demo {
      height: 300px;
      /* display: none; */
    }
  </style>

  <script>
    export default {
      created() {
        // this.getWeather();
        // this.getWeather15();
      },
      data() {
        let self = this;
        return {
          center: [121.59996, 31.197646],
          lng: 0,
          lat: 0,
          loaded: false,
          result:'',
          plugin: [{
            pName: 'Geolocation',
            events: {
              init(o) {
                // o 是高德地图定位插件实例
                o.getCurrentPosition((status, result) => {
                  console.log(status,result);
                  if (result && result.position) {
                    self.lng = result.position.lng;
                    self.lat = result.position.lat;
                    self.center = [self.lng, self.lat];
                    self.loaded = true;
                    self.result = result.formattedAddress;
                    self.$nextTick();
                  }
                });
              }
            }
          }],
          // 实况天气
          hourly:[],
          cty:{
            pname:'',
            name:''
          },
          sfc:{
            banner:''
          },
          // 未来15天
          forecast:[]
        };
      },
      methods: {
        async getWeather() {
          //  api接口 http://aliv8.data.moji.com/whapi/json/aliweather/shortforecast
          // 传参 lat(纬度) lon(经度)   经纬度 
          // const ret = await this.$http.post('http://aliv8.data.moji.com/whapi/json/aliweather/shortforecast',{lat:this.lat,lon:this.lng});
          // console.log(ret);
          const ret = await this.$http.post('http://aliv8.data.moji.com/whapi/json/aliweather/forecast24hours',{lat:this.lat,lon:this.lng});
          console.log(ret.data);
          this.cty = ret.body.data.city
          // this.sfc = ret.body.data.sfc
          this.hourly = ret.data.data.hourly;
        },
        async getWeather15() {
          const ret = await this.$http.post('http://aliv8.data.moji.com/whapi/json/aliweather/forecast15days',{lat:this.lat,lon:this.lng})
          console.log(ret.body.data.forecast);
          this.forecast = ret.body.data.forecast;
          
        }
      },
    }
    </script>