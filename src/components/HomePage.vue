<template>
  <div class="cloudy">
    <div class="location">
      南昌
    </div>
    <div class="temperature">
      16°
    </div>
    <div class="wind">
      阴|北风三级
    </div>
    <div class="air">
      9优>
    </div>
    <div class="todayweather">
      <span>
        今天：阴转多云 14至20℃ 北风4-5级
      </span>
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
import * as echarts from 'echarts'
export default {
  name: 'HomePage',
  methods: {
    showecharts() {
      var chartDom = document.querySelector('.charts');
      var myChart = echarts.init(chartDom);
      var option;
      option = {
        xAxis: {
          type: 'category',
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            data: [150, 230, 224, 218, 135, 147, 260],
            type: 'line'
          }
        ]
      };

      option && myChart.setOption(option);
    }
  },
  mounted(){
    this.showecharts()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cloudy {
  height: 100vh;
  background-image: linear-gradient(to bottom, rgb(75, 86, 98), rgb(165, 183, 200));
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
.date{
  background-color: #fff;
  height: 18vh;
}
.date ul{
  display: flex;
  padding: 0;
}
.date ul li {
  width: 20vw;
  height: 18vh;
  justify-content: space-around;
  list-style: none;
}
.date ul li p{
  color: #000;
  text-align: center;
  margin-top: 2vh;
  font-size: 2vh;
}
</style>
