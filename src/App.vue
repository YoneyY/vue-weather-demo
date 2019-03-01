<template>
    <div id="weather">
        <el-amap v-show="positioning" vid="amap" :plugin="plugin" class="amap-demo" :center="center">
        </el-amap>
        <!-- lbs定位 -->
        <el-row>
          <el-col :span="24">
              <h3 class="districtfont" v-show="show">
                <i class="el-icon-location-outline showi"></i>
                <span v-if="loaded" @click="positioning = true">{{district}}</span>
                <span v-else>正在定位</span>
              </h3>
          </el-col>
        </el-row>
        <el-row>
          <el-col>
            <div class="condition">
              <h1>{{condition.condition}}</h1>
              <p>口袋小提示：{{condition.tips}}</p>
              <p class="conTemp">{{condition.temp}}°</p>
            </div>
          </el-col>
          <el-row class="sun">
            <el-col :span="12">
              <i class="iconfont icon-richu"></i>
              <div >{{condition.sunRise}}</div>
            </el-col>
            <el-col :span="12">
              <i class="iconfont icon-rila"></i>
              <div>{{condition.sunSet}}</div>
            </el-col>
          </el-row>
        </el-row>
        <!-- 24小时天气展示 -->
        <transition name="el-zoom-in-bottom">
          <el-card v-show="show">
            <el-table :data="hourly" style="width: 100%" :show-header="false">
              <!-- <el-table-column type="expand">
                666
              </el-table-column> -->
              <el-table-column label="时" align="center">
                <template slot-scope="info">
                  <el-tag>{{info.row.hour}}时</el-tag> 
                </template>
              </el-table-column>
              <el-table-column
                prop="condition"
                label="天气" align="center">
              </el-table-column>
              <el-table-column label="温度" align="center">
                <template slot-scope="info">
                  <el-tag>{{info.row.temp}}°</el-tag> 
                </template>
              </el-table-column>
            </el-table>
          </el-card>
        </transition>
    </div>
</template>

<script>
export default {
  mounted() {
    this.show = true;
  },
  created() {
    // this.getWeather();
    // this.getWeather15();
  },
  data() {
    let self = this;
    return {
      show:false, // 显示效果
      center: [116.627467, 40.163373], // 地图中心 如果定位失败 将自动定位到这里
      lng: 0,
      lat: 0,
      loaded: false,
      result:'',
      district:'',
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
                self.district = result.addressComponent.district;
                self.$nextTick();
                self.getWeather(); //请求成功后执行
                self.getCondition();
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
      forecast:[],
      // 实况天气
      condition:{},

      // 显示地图定位
      positioning:false
    };
  },
  methods: {
    // 24小时天气
    async getWeather() {
      //  api接口 http://aliv8.data.moji.com/whapi/json/aliweather/shortforecast
      // 传参 lat(纬度) lon(经度)   经纬度 
      // const ret = await this.$http.post('http://aliv8.data.moji.com/whapi/json/aliweather/shortforecast',{lat:this.lat,lon:this.lng});
      // console.log(ret);
      const ret = await this.$http.post('http://aliv8.data.moji.com/whapi/json/aliweather/forecast24hours',{lat:this.lat,lon:this.lng});
      console.log(ret.data);
      this.cty = ret.body.data.city
      this.hourly = ret.data.data.hourly;
    },
    // 未来15天
    async getWeather15() {
      const ret = await this.$http.post('http://aliv8.data.moji.com/whapi/json/aliweather/forecast15days',{lat:this.lat,lon:this.lng})
      console.log(ret.body.data.forecast);
      this.forecast = ret.body.data.forecast;
    },
    // 实况天气 http://aliv8.data.moji.com/whapi/json/aliweather/condition
    async getCondition() {
      const ret = await this.$http.post('http://aliv8.data.moji.com/whapi/json/aliweather/condition',{lat:this.lat,lon:this.lng});
      console.log(ret.body.data.condition);
      this.condition = ret.body.data.condition;
    }
  },
}
</script>

<style lang="less" scoped>
  // .amap-demo{
  //   display: none;
  // }
  #weather{
    width: 100%;
    background-image: linear-gradient(
      to bottom,
      #1e88e5,
      #bbdefb
    );
    color: #fff;
    .districtfont{
      // text-align: center;
    }
    .showi{
      margin:0 5px;
    }
    .el-card{
      margin-top: 70px;
      box-shadow: 0 0 20px #eee;
    }
    .condition{
      text-align: center;
      h1{
        font-size: 42px;
      }
      .conTemp{
        font-size: 30px;
      }
    }
    .sun {
      text-align: center;
      i{
        font-size: 32px;
      }
    }
  }
  // 特效动画
</style>

