<template>
    <div id="weather">
        <el-amap vid="amap" :plugin="plugin" class="amap-demo" :center="center">
        </el-amap>
        <el-row>
          <el-col :span="24">
              <h1 class="districtfont" v-show="show"><i class="el-icon-location-outline showi"></i>{{district}}</h1>
          </el-col>
        </el-row>
        <!-- 24小时天气展示 -->
        <transition name="el-zoom-in-bottom">
          <el-card v-show="show">
            <el-table :data="hourly" style="width: 100%" :show-header="false">
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
    this.getWeather();
    // this.getWeather15();
  },
  data() {
    let self = this;
    return {
      show:false, // 显示效果
      center: [121.59996, 31.197646], // 地图中心 如果定位失败 将自动定位到这里
      lng: 116.627467,
      lat: 40.163373,
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

<style lang="less" scoped>
  .amap-demo{
    display: none;
  }
  #weather{
    width: 100%;
    background-image: linear-gradient(
      to bottom,
      #1e88e5,
      #bbdefb
    );
    color: #fff;
    .districtfont{
      text-align: center;
    }
    .showi{
      margin-right: 5px;
    }
    .el-card{
      margin-top: 200px;
      box-shadow: 0 0 20px #eee;
    }
  }
  // 特效动画
</style>

