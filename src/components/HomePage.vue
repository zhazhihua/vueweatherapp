<template>
  <div class="cloudy">
    <div class="location" @click="showweather">{{city}}</div>
    <div class="temperature">{{nowweather.tem}}°</div>
    <div class="wind">{{nowweather.wea}}|{{nowweather.win}}{{nowweather.win_speed}}</div>
    <div class="air">{{nowweather.air}}{{temperature.air_level}}></div>
    <div class="todayweather">
      <span> 今天：{{nowweather.wea}}&nbsp;&nbsp;{{nowweather.tem2}}至{{nowweather.tem1}}℃&nbsp;&nbsp;{{nowweather.win}}{{nowweather.win_speed}}</span>
    </div>
    <div class="charts"></div>
    <div class="date">
      <ul>
        <li>
          <p>昨天</p>
          <p>10/08</p>
        </li>
        <li>
          <p>今天</p>
          <p>10/09</p>
        </li>
        <li>
          <p>明天</p>
          <p>10/10</p>
        </li>
        <li>
          <p>周二</p>
          <p>10/11</p>
        </li>
        <li>
          <p>周三</p>
          <p>10/12</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import * as echarts from "echarts";
import axios from 'axios'
import {nextTick} from 'vue'
export default {
  name: "HomePage",
  data() {
    return {
      city:'南昌',
      time:[],
      temperature:[],
      nowweather:{},
      flag:true
    };
  },
  methods: {
    showweather(){
      this.getWeatherData();
      //this.getnowWeatherData();
    },
    getWeatherData(){
      axios.get(`https://v0.yiketianqi.com/api/worldchina?appid=24831698&appsecret=p8sIVJ6B&city=${this.city}`)
      .then((res)=>{
        if(this.flag){
          res.data.hours.slice(0,5).forEach((item)=>{
            this.time.push(item.time)
          })
        }
      })
    },
    // getnowWeatherData(){
    //   axios.get(`https://v0.yiketianqi.com/api?unescape=1&version=v61&appid=24831698&appsecret=p8sIVJ6B&city=${this.city}`)
    //   .then((res)=>{
    //     this.nowweather = res.data
    //   })
    // },
    showecharts() {
      var chartDom = document.querySelector(".charts");
      var myChart = echarts.init(chartDom);
      var option;
      option = {
        xAxis: {
          type: "category",
          data: this.time,
          axisTick: {
            show: false,
          },
          axisLabel: {
            show: true,
            textStyle: {
              color: "#fff",
            },
          },
        },
        yAxis: {
          show: false,
          type: "value",
        },
        series: [
          {
            data: [15, 16, 18, 18, 13, 14, 26],
            type: "line",
            label: {
              show: true,
              formatter(data) {
                return data.value + "°";
              },
            },
            itemStyle: {
              normal: {
                color: "#fff", //改变折线点的颜色
                lineStyle: {
                  color: "#fff", //改变折线颜色
                },
              },
            },
          },
        ],
      };

      option && myChart.setOption(option);
    },
  },
  mounted() {
    
    this.showecharts();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cloudy {
  height: 100vh;
  background-image: linear-gradient(
    to bottom,
    rgb(75, 86, 98),
    rgb(165, 183, 200)
  );
}

.temperature {
  height: 25vh;
  line-height: 25vh;
  font-size: 12vh;
  text-align: center;
}

.wind {
  text-align: center;
}

.air {
  width: 20vw;
  margin: 0 auto;
  border-radius: 10vw;
  background-color: rgb(58, 179, 98);
  text-align: center;
  margin-top: 2vh;
}

.todayweather {
  margin-top: 2vh;
  margin-bottom: -4vh;
}

.todayweather span {
  font-size: 2vw;
}

.charts {
  height: 40vh;
  margin-top: 5vh;
}
.date {
  background-color: #fff;
  height: 18vh;
}
.date ul {
  display: flex;
  padding: 0;
}
.date ul li {
  width: 20vw;
  height: 18vh;
  justify-content: space-around;
  list-style: none;
}
.date ul li p {
  color: #000;
  text-align: center;
  margin-top: 2vh;
  font-size: 2vh;
}
</style>
