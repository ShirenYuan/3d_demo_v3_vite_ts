<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
import WeatherWidget from '../components/HelloWorld.vue';
import { ref,onMounted,defineComponent } from 'vue';
import { Vue3SeamlessScroll } from "vue3-seamless-scroll";
import * as echarts from 'echarts';
type EChartsOption = echarts.EChartsOption;



const animIndex = ref(0)
const cameraList = ref([
  {status:"0",id: "18",name:"全景",cameraPosition:{x:"25.41",y:"44.93",z:"5.9"},cameraRotation:{x:"-1.44",y:"0.51",z:"1.31"}},
  {status:"0",id: "1",name:"X射线衍射仪",cameraPosition:{x:"12.31",y:"2.93",z:"-32.63"},cameraRotation:{x:"-1.48",y:"-1.06",z:"-1.47"}},
  {status:"1",id: "2",name:"高频疲劳材料试验机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
  {status:"0",id: "3",name:"高温拉伸设备",cameraPosition:{x:"13.96",y:"4.66",z:"-21.76"},cameraRotation:{x:"-2.57",y:"-0.13",z:"-3.05"}},
  {status:"1",id: "4",name:"电子拉伸材料试验机",cameraPosition:{x:"11.22",y:"2.76",z:"-22.19"},cameraRotation:{x:"-2.88",y:"0.18",z:"3.09"}},
  // {id: "5",name:"注塑机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
  // {id: "6",name:"锥形双螺杆挤出机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
  {status:"0",id: "7",name:"焊接机器人",cameraPosition:{x:"1.72",y:"3.90",z:"-24.48"},cameraRotation:{x:"-1.53",y:"-0.94",z:"-1.52"}},
  // {id: "8",name:"激光清洗机",cameraPosition:{x:"1.72",y:"3.90",z:" -24.48"},cameraRotation:{x:"-1.53",y:"-0.94",z:"-1.52"}},
  {status:"0",id: "9",name:"真空纤维炉",cameraPosition:{x:"-3.62",y:"3.56",z:"-18.26"},cameraRotation:{x:"-2.65",y:"1.30",z:"2.66"}},
  // {id: "10",name:"伺服压力机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
  {status:"1",id: "11",name:"光纤激光加工控制系统",cameraPosition:{x:"-0.39",y:"2.97",z:"4.33"},cameraRotation:{x:"-1.61",y:"-1.37",z:"-1.61"}},
  // {id: "12",name:"连续激光机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
  {status:"0",id: "13",name:"CMT冷金属过渡焊接系统",cameraPosition:{x:"-4.34",y:"3.49",z:"3.80"},cameraRotation:{x:"-2.84",y:"-0.17",z:"-3.08"}},
  // {id: "14",name:"球磨机",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
  // {id: "15",name:"纳秒激光器",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
  // {id: "16",name:"三坐标",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
  {status:"1",id: "17",name:"蟠变试验机",cameraPosition:{x:"-1.12",y:"2.84",z:"28.70"},cameraRotation:{x:"3.02",y:"0.10",z:"3.12"}},
])


const parentMethod = (index:number) => {
  console.log(index)
  animIndex.value = index
};

const realList = ref([
  {
    roomName:"全景",
    roomId:"0",
    list:[
      {name:"全景",id:"0",status:"1",cameraPosition:{x:"25.41",y:"44.93",z:"5.9"},cameraRotation:{x:"-1.44",y:"0.51",z:"1.31"}}
    ]
  },
  {
    roomName:"X射线衍射实验室",
    roomId:"1",
    list:[
      {name:"X射线衍射仪",id:"1",status:"1",cameraPosition:{x:"12.31",y:"2.93",z:"-32.63"},cameraRotation:{x:"-1.48",y:"-1.06",z:"-1.47"}}
    ]
  },
  {
    roomName:"材料疲劳分析室",
    roomId:"2",
    list:[
      {name:"高频疲劳材料试验机",id:"2",status:"1",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}}
    ]
  },
  {
    roomName:"材料及构件可靠性测试分析实验室",
    roomId:"3",
    list:[
      {name:"高温拉伸设备",id:"3",status:"0",cameraPosition:{x:"13.96",y:"4.66",z:"-21.76"},cameraRotation:{x:"-2.57",y:"-0.13",z:"-3.05"}},
      {name:"电子拉伸材料试验机",id:"4",status:"0",cameraPosition:{x:"11.22",y:"2.76",z:"-22.19"},cameraRotation:{x:"-2.88",y:"0.18",z:"3.09"}}
    ]
  },
  {
    roomName:"塑料成形实验室",
    roomId:"4",
    list:[
      // {name:"注塑机",id:"5",status:"0",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
      // {name:"锥形双螺杆挤出机",id:"6",status:"1",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
    ]
  },
  {
    roomName:"焊接工程实验室",
    roomId:"5",
    list:[
      {name:"焊接机器人",id:"7",status:"1",cameraPosition:{x:"1.72",y:"3.90",z:"-24.48"},cameraRotation:{x:"-1.53",y:"-0.94",z:"-1.52"}},
    ]
  },
  {
    roomName:"试件设计加工中心/焊接及扩散焊室",
    roomId:"6",
    list:[
      // {name:"激光清洗机",id:"8",status:"0",cameraPosition:{x:"1.72",y:"3.90",z:" -24.48"},cameraRotation:{x:"-1.53",y:"-0.94",z:"-1.52"}},
      {name:"真空纤维炉",id:"9",status:"1",cameraPosition:{x:"-3.62",y:"3.56",z:"-18.26"},cameraRotation:{x:"-2.65",y:"1.30",z:"2.66"}},
    ]
  },
  {
    roomName:"压力成型实验室",
    roomId:"7",
    list:[
      // {name:"伺服压力机",id:"10",status:"1",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
    ]
  },
  {
    roomName:"激光工业技术研究所",
    roomId:"8",
    list:[
      {name:"光纤激光加工控制系统",id:"11",status:"0",cameraPosition:{x:"-0.39",y:"2.97",z:"4.33"},cameraRotation:{x:"-1.61",y:"-1.37",z:"-1.61"}},
      // {name:"连续激光机",id:"12",status:"1",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
      {name:"CMT冷金属过渡焊接系统",id:"13",status:"1",cameraPosition:{x:"-4.34",y:"3.49",z:"3.80"},cameraRotation:{x:"-2.84",y:"-0.17",z:"-3.08"}},
      // {name:"球磨机",id:"14",status:"0",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
      // {name:"纳秒激光器",id:"15",status:"0",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
      // {name:"三坐标",id:"16",status:"1",cameraPosition:{x:"11.92",y:"3.41",z:"-25.36"},cameraRotation:{x:"-2.52",y:"0.77",z:"2.68"}},
    ]
  }
  ,
  {
    roomName:"蟠变试验机研究室",
    roomId:"9",
    list:[
      {name:"蟠变试验机",id:"17",status:"0",cameraPosition:{x:"-1.12",y:"2.84",z:"28.70"},cameraRotation:{x:"3.02",y:"0.10",z:"3.12"}},
    ]
  }
])

const transformedArray = realList.value.flatMap(room => room.list.map(item => ({
  name: item.name,
  roomName: room.roomName,
  status: item.status,
  id: item.id,
  roomId: room.roomId,
  cameraPosition: item.cameraPosition,
  cameraRotation: item.cameraRotation,
})));

var option: EChartsOption;
option = {
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'none'
    },
    formatter: function (params: any) {
      return params[0].name + ': ' + params[0].value;
    }
  },
  xAxis: {
    data: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
    axisTick: { show: false },
    axisLine: { show: false },
    axisLabel: {
      color: '#0000ff'
    }
  },
  yAxis: {
    splitLine: { show: false },
    axisTick: { show: false },
    axisLine: { show: false },
    axisLabel: { show: false }
  },
  color: ['#0000ff'],
  series: [
    {
      name: 'hill',
      type: 'pictorialBar',
      barCategoryGap: '-130%',
      // symbol: 'path://M0,10 L10,10 L5,0 L0,10 z',
      symbol: 'path://M0,10 L10,10 C5.5,10 5.5,5 5,0 C4.5,5 4.5,10 0,10 z',
      itemStyle: {
        opacity: 0.5
      },
      emphasis: {
        itemStyle: {
          opacity: 1
        }
      },
      data: [13, 13, 8, 13, 18, 8, 13, 10, 13, 7, 15, 18],
      z: 10
    },
    
  ]
};


const timerData = ref<any>(null)
const dataDat = ref<any>({})


onMounted(() => {
  initChartFun("echarts4",option)
  if(timerData.value){
    clearInterval(timerData.value)
  }
  timerData.value = setInterval(()=>{
    dataDat.value = getCurrentTime();
  },1000)
})
function getCurrentTime() {
  const now = new Date();

  // 获取小时和分钟
  const hours = now.getHours().toString().padStart(2, '0');
  const minutes = now.getMinutes().toString().padStart(2, '0');

  // 获取年、月、日
  const year = now.getFullYear();
  const month = (now.getMonth() + 1).toString().padStart(2, '0'); // 月份从0开始，需要加1
  const day = now.getDate().toString().padStart(2, '0');

  // 获取星期
  const weekdays = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
  const weekDay = weekdays[now.getDay()];

  // 构造返回的对象
  const dateTime = `${hours}:${minutes}`;
  const years = `${year}.${month}.${day}`;
  const week = weekDay;

  return { dateTime, years, week };
}



function initChartFun(className:string,optionDatil:object){
  console.log(className)
  console.log(optionDatil)
  // 基于准备好的dom，初始化echarts实例
  var myChart = echarts.init(document.getElementById(className));
  // 绘制图表
  myChart.setOption(optionDatil);
}


</script>

<template>
  <main>
    <div class="main">
      <TheWelcome class="main_3d" :cameraList="transformedArray" :parentMethod="parentMethod" />
      <!-- detail -->
      <div class="main_detail" v-if="animIndex!=0">
        <div class="main_detail_title">{{ transformedArray[animIndex].name }}</div>
        <div v-if="transformedArray[animIndex].status=='0'" class="main_detail_status">未使用</div>
        <div v-if="transformedArray[animIndex].status=='1'" class="main_detail_status2">使用中</div>
      </div>
      <!-- top -->
      <div class="main_top">
        <div class="main_top_left">
          <div class="main_top_left_left">
            <div class="main_top_left_left_icon"></div>
            <div class="main_top_left_left_tianqi">
              <WeatherWidget />
            </div>
          </div>
          <div class="main_top_left_right">
            <div class="main_top_left_right_icon"></div>
            <div class="main_top_left_right_text">20%rh</div>
          </div>
          <div class="main_top_left_right">
            <div class="main_top_left_right_icon2"></div>
            <div class="main_top_left_right_text">20</div>
          </div>
        </div>
        <div class="main_top_right">
          <div class="main_top_right_date">{{ dataDat.dateTime }}</div>
          <div class="main_top_right_year">{{ dataDat.years }}</div>
          <div class="main_top_right_week">{{ dataDat.week }}</div>
        </div>
      </div>
      <!-- content -->
      <div class="main_content">
        <!-- content_left -->
        <div class="main_content_left">
          <!-- 监控状态 -->
          <div class="main_content_left_one">
            <div class="main_content_left_one_title">
              <div class="main_content_left_one_title_text">监控状态</div>
              <div class="main_content_left_one_title_icon"></div>
            </div>
            <div class="main_content_left_one_content">
              <div class="main_content_left_one_content_one">
                <div class="main_content_left_one_content_one_echarts">
                  <div class="main_content_left_one_content_one_echarts_top"></div>
                  <div class="main_content_left_one_content_one_echarts_bot"></div>
                  <div class="main_content_left_one_content_one_echarts_content">
                    <div class="main_content_left_one_content_one_echarts_content_title">10</div>
                    <div class="main_content_left_one_content_one_echarts_content_text">(台)</div>
                  </div>
                </div>
                <div class="main_content_left_one_content_one_text">使用中</div>
              </div>
              <div class="main_content_left_one_content_one">
                <div class="main_content_left_one_content_one_echarts2">
                  <div class="main_content_left_one_content_one_echarts_top"></div>
                  <div class="main_content_left_one_content_one_echarts_bot"></div>
                  <div class="main_content_left_one_content_one_echarts_content">
                    <div class="main_content_left_one_content_one_echarts_content_title">3692</div>
                    <div class="main_content_left_one_content_one_echarts_content_text">(小时)</div>
                  </div>
                </div>
                <div class="main_content_left_one_content_one_text">使用统计</div>
              </div>
              <div class="main_content_left_one_content_one">
                <div class="main_content_left_one_content_one_echarts3">
                  <div class="main_content_left_one_content_one_echarts_top"></div>
                  <div class="main_content_left_one_content_one_echarts_bot"></div>
                  <div class="main_content_left_one_content_one_echarts_content">
                    <div class="main_content_left_one_content_one_echarts_content_title">65%</div>
                  </div>
                </div>
                <div class="main_content_left_one_content_one_text">使用效率</div>
              </div>
            </div>
          </div>
          <!-- 设备使用率排名 -->
          <div class="main_content_left_one">
            <div class="main_content_left_one_title">
              <div class="main_content_left_one_title_text">设备使用率排名</div>
              <div class="main_content_left_one_title_icon2"></div>
            </div>
            <div class="main_content_left_one_content2">
              <div class="main_content_left_one_content_left"></div>
              <div class="main_content_left_one_content_right">
                <div class="main_content_left_one_content_right_one main_content_left_one_content_right_one1">
                  <div class="main_content_left_one_content_right_one_name">{{ transformedArray[1].name }}</div>
                  <div class="main_content_left_one_content_right_one_icon"></div>
                  <div class="main_content_left_one_content_right_one_text">
                    <div class="main_content_left_one_content_right_one_text_one">
                      <div class="main_content_left_one_content_right_one_text_one_left">数据</div>
                      <div class="main_content_left_one_content_right_one_text_one_right">(50%)</div>
                    </div>
                    <div class="main_content_left_one_content_right_one_text_one">
                      <div class="main_content_left_one_content_right_one_text_one_left">2390</div>
                      <div class="main_content_left_one_content_right_one_text_one_right2">次</div>
                    </div>
                  </div>
                </div>
                <div class="main_content_left_one_content_right_one main_content_left_one_content_right_one2">
                  <div class="main_content_left_one_content_right_one_name">{{ transformedArray[5].name }}</div>
                  <div class="main_content_left_one_content_right_one_icon2"></div>
                  <div class="main_content_left_one_content_right_one_text">
                    <div class="main_content_left_one_content_right_one_text_one">
                      <div class="main_content_left_one_content_right_one_text_one_left2">数据</div>
                      <div class="main_content_left_one_content_right_one_text_one_right">(30%)</div>
                    </div>
                    <div class="main_content_left_one_content_right_one_text_one">
                      <div class="main_content_left_one_content_right_one_text_one_left2">1250</div>
                      <div class="main_content_left_one_content_right_one_text_one_right2">次</div>
                    </div>
                  </div>
                </div>
                <div class="main_content_left_one_content_right_one main_content_left_one_content_right_one3">
                  <div class="main_content_left_one_content_right_one_name">{{ transformedArray[3].name }}</div>
                  <div class="main_content_left_one_content_right_one_icon3"></div>
                  <div class="main_content_left_one_content_right_one_text">
                    <div class="main_content_left_one_content_right_one_text_one">
                      <div class="main_content_left_one_content_right_one_text_one_left3">数据</div>
                      <div class="main_content_left_one_content_right_one_text_one_right">(20%)</div>
                    </div>
                    <div class="main_content_left_one_content_right_one_text_one">
                      <div class="main_content_left_one_content_right_one_text_one_left3">870</div>
                      <div class="main_content_left_one_content_right_one_text_one_right2">次</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <!-- content_right -->
        <div class="main_content_right">
          <!-- 设备使用时状态 -->
          <div class="main_content_right_one">
            <div class="main_content_right_one_title">
              <div class="main_content_right_one_title_text">设备使用时状态</div>
              <div class="main_content_right_one_title_icon"></div>
            </div>
            <div class="main_content_right_one_content">
              <div class="main_content_right_one_content_title">
                <div class="main_content_right_one_content_title_name">实验室</div>
                <div class="main_content_right_one_content_title_shebei">仪器名称</div>
                <div class="main_content_right_one_content_title_status">状态</div>
              </div>
              <div class="main_content_right_one_content_content">
                <div class="main_content_right_one_content_content_ul">
                  <vue3-seamless-scroll :list="transformedArray" class="scroll">
                    <template v-for="(item, index) in transformedArray" :key="index">
                      <div class="main_content_right_one_content_content_ul_li" v-if="index!=0">
                        <div class="main_content_right_one_content_content_ul_li_icon"></div>
                        <div class="main_content_right_one_content_content_ul_li_name">{{ item.roomName }}</div>
                        <div class="main_content_right_one_content_content_ul_li_shebei">{{ item.name }}</div>
                        <div v-if="item.status=='0'" class="main_content_right_one_content_content_ul_li_status">使用中</div>
                        <div v-if="item.status=='1'" class="main_content_right_one_content_content_ul_li_status2">未使用</div>
                      </div>
                    </template>
                  </vue3-seamless-scroll>
                </div>
              </div>
            </div>
          </div>
          <!-- 设备使用趋势（12个月） -->
          <div class="main_content_right_one">
            <div class="main_content_right_one_title">
              <div class="main_content_right_one_title_text">设备使用趋势（12个月）</div>
              <div class="main_content_right_one_title_icon2"></div>
            </div>
            <div class="main_content_right_one_content main_content_right_one_content2">
              <div id="echarts4" class="main_content_right_one_content_echarts"></div>
            </div>
          </div>
        </div>
      </div>
      <!-- bottom -->
      <div class="main_bottom">
        <div class="main_bottom_box">
          <div class="main_bottom_one">
            <div class="main_bottom_one_img1"></div>
            <div class="main_bottom_one_right">
              <div class="main_bottom_one_right_title">实验室</div>
              <div class="main_bottom_one_right_num">
                <div class="main_bottom_one_right_num_num">8</div>
                <div class="main_bottom_one_right_num_text">个</div>
              </div>
            </div>
          </div>
          <div class="main_bottom_one">
            <div class="main_bottom_one_img2"></div>
            <div class="main_bottom_one_right">
              <div class="main_bottom_one_right_title">实验设备</div>
              <div class="main_bottom_one_right_num">
                <div class="main_bottom_one_right_num_num">15</div>
                <div class="main_bottom_one_right_num_text">个</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.main {
  width: 100vw;
  height: 100vh;
  position: relative;
  overflow: hidden;
  .main_detail {
    /* width: 0px; */
    /* height: 50px; */
    background: rgba(255, 255, 255, 0.7);
    border-radius: 20px;
    position: absolute;
    top: 30%;
    left: 50%;
    transform: translate(-50%,-50%);
    padding: 20px;
    font-size: 20px;
    line-height: 1.5;
    text-align: center;
    .main_detail_title {
    }
    .main_detail_status {
      color: #00ff00;
    }
    .main_detail_status2 {
      color: #ff0000;
    }
  }
  .main_3d {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
  }
  .main_top {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 16%;
    background: url("../assets/img/014.png")0 0 / 100% 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 20px;
    font-family: SourceHanSansCN;
    font-weight: 500;
    color: #98B8D9;
    text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
    box-sizing: border-box;
    padding: 0 76.5px 0 75.5px;
    margin-top: -20px;
    .main_top_left {
      display: flex;
      align-items: center;
      .main_top_left_left {
        display: flex;
        align-items: center;
        .main_top_left_left_icon {
          width: 14.25px;
          height: 23.1px;
          background: url("../assets/img/001.png") 0 0 / 100% 100%;
          margin-right: 14.5px;
        }
        .main_top_left_left_tianqi {
          /* width: 100px; */
        }
      }
      .main_top_left_right {
        display: flex;
        align-items: center;
        margin-left: 20px;
        .main_top_left_right_icon {
          width: 16px;
          height: 21px;
          background: url("../assets/img/002.png") 0 0 / 100% 100%;
        }
        .main_top_left_right_icon2 {
          width: 24.5px;
          height: 24.5px;
          background: url("../assets/img/003.png") 0 0 / 100% 100%;
        }
        .main_top_left_right_text {
          margin-left: 19.5px;
        }
      }
    }
    .main_top_right {
      display: flex;
      align-items: center;
      
      .main_top_right_date {
        margin-right: 57px;
      }
      .main_top_right_year {
        margin-right: 74px;

      }
      .main_top_right_week {

      }
    }
  }
  .main_content {
    width: 100%;
    position: relative;
    margin-top: 163.5px;
    .main_content_left {
      width: 600px;
      position: absolute;
      left: 118px;
      top: 0;
      .main_content_left_one {
        width: 100%;
        height: 350px;
        margin-top: 50px;
        .main_content_left_one_title {
          width: 100%;
          height: 50px;
          display: flex;
          align-items: center;
          background: url(../assets/img/011.png) 0 0 / 100% 100%;
          box-sizing: border-box;
          padding-left: 70px;
          .main_content_left_one_title_text {
            font-size: 23px;
            font-family: SourceHanSansCN;
            font-weight: 500;
            line-height: 1;
            color: #FFFFFF;
            text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
          }
          .main_content_left_one_title_icon {
            width: 35px;
            height: 44px;
            background: url("../assets/img/004.png") 0 0 / 100% 100%;
            margin-left: 23.5px;
          }
          .main_content_left_one_title_icon2 {
            width: 50px;
            height: 43px;
            background: url("../assets/img/008.png") 0 0 / 100% 100%;
            margin-left: 23.5px;
          }
        }
        .main_content_left_one_content {
          width: 100%;
          height: 100%;
          display: flex;
          align-items: center;
          /* justify-content: center; */
        }
        .main_content_left_one_content_one {
          display: flex;
          flex-direction: column;
          align-items: center;
          margin-right: 25px;
          .main_content_left_one_content_one_echarts {
            width: 136px;
            height: 136px;
            position: relative;
            .main_content_left_one_content_one_echarts_top {
              width: 100%;
              height: 50%;
              border-radius: 68px 68px 0 0;
              border-top: 1px solid #FBAB20;
              border-left: 1px solid #FBAB20;
              border-right: 1px solid #FBAB20;
            }
            .main_content_left_one_content_one_echarts_bot {
              width: 100%;
              height: 50%;
              border-radius:  0 0 68px 68px;
              border-bottom: 3px solid #FBAB20;
              border-left: 3px solid #FBAB20;
              border-right: 3px solid #FBAB20;
            }
            .main_content_left_one_content_one_echarts_content {
              position: absolute;
              top: 50%;
              left: 50%;
              transform: translate(-50%,-50%);
              width: 114px;
              height: 114px;
              border-radius: 50%;
              border: 1px #FBAB20 dashed;
              display: flex;
              flex-direction: column;
              align-items: center;
              justify-content: center;
              .main_content_left_one_content_one_echarts_content_title {
                font-size: 30px;
                font-family: SourceHanSansCN;
                font-weight: bold;
                color: #FBB020;
                text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
              }
              .main_content_left_one_content_one_echarts_content_text {
                font-size: 16px;
                font-family: SourceHanSansCN;
                font-weight: 400;
                color: #E6E6E6;
                text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
              }
            }
          }
          .main_content_left_one_content_one_echarts2 {
            width: 136px;
            height: 136px;
            position: relative;
            .main_content_left_one_content_one_echarts_top {
              width: 100%;
              height: 50%;
              border-radius: 68px 68px 0 0;
              border-top: 3px solid #20FBF4;
              border-left: 3px solid #20FBF4;
              border-right: 3px solid #20FBF4;
            }
            .main_content_left_one_content_one_echarts_bot {
              width: 100%;
              height: 50%;
              border-radius:  0 0 68px 68px;
              border-bottom: 1px solid #20FBF4;
              border-left: 1px solid #20FBF4;
              border-right: 1px solid #20FBF4;
            }
            .main_content_left_one_content_one_echarts_content {
              position: absolute;
              top: 50%;
              left: 50%;
              transform: translate(-50%,-50%);
              width: 114px;
              height: 114px;
              border-radius: 50%;
              border: 1px #20FBF4 dashed;
              display: flex;
              flex-direction: column;
              align-items: center;
              justify-content: center;
              .main_content_left_one_content_one_echarts_content_title {
                font-size: 30px;
                font-family: SourceHanSansCN;
                font-weight: bold;
                color: #20FBF4;
                text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
              }
              .main_content_left_one_content_one_echarts_content_text {
                font-size: 16px;
                font-family: SourceHanSansCN;
                font-weight: 400;
                color: #E6E6E6;
                text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
              }
            }
          }
          .main_content_left_one_content_one_echarts3 {
            width: 136px;
            height: 136px;
            position: relative;
            .main_content_left_one_content_one_echarts_top {
              width: 100%;
              height: 50%;
              border-radius: 68px 68px 0 0;
              border-top: 1px solid #2177FD;
              border-left: 1px solid #2177FD;
              border-right: 1px solid #2177FD;
            }
            .main_content_left_one_content_one_echarts_bot {
              width: 100%;
              height: 50%;
              border-radius:  0 0 68px 68px;
              border-bottom: 3px solid #2177FD;
              border-left: 3px solid #2177FD;
              border-right: 3px solid #2177FD;
            }
            .main_content_left_one_content_one_echarts_content {
              position: absolute;
              top: 50%;
              left: 50%;
              transform: translate(-50%,-50%);
              width: 114px;
              height: 114px;
              border-radius: 50%;
              border: 1px #2177FD dashed;
              display: flex;
              flex-direction: column;
              align-items: center;
              justify-content: center;
              .main_content_left_one_content_one_echarts_content_title {
                font-size: 30px;
                font-family: SourceHanSansCN;
                font-weight: bold;
                color: #2177FD;
                text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
              }
            }
          }
          
          .main_content_left_one_content_one_text {
            font-size: 20px;
            font-family: SourceHanSansCN;
            font-weight: 500;
            color: #FEFEFE;
            text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
            margin-top: 10.5px;
          }
        }
        .main_content_left_one_content2 {
          width: 100%;
          height: 100%;
          display: flex;

        }
        .main_content_left_one_content_left {
          width: 260px;
          height: 250px;
          background: url("../assets/img/013.png") 0 0 / 100% 100%;
        }
        .main_content_left_one_content_right {
          .main_content_left_one_content_right_one1 {
            margin-left: -60px;
          }
          .main_content_left_one_content_right_one2 {
            margin-left: -30px;
          }
          .main_content_left_one_content_right_one3 {
            margin-left: 0px;
          }
          .main_content_left_one_content_right_one {
            display: flex;
            align-items: center;
            margin-top: 10px;
            .main_content_left_one_content_right_one_name {
              width: 163px;
              text-align: center;
              border-bottom: 1px dashed #fff;
              font-size: 22px;
              font-family: SourceHanSansCN;
              font-weight: 400;
              color: #C5D0D4;
              line-height: 1.4;
              text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
              display: flex;
              align-items: center;
              justify-content: center;
            }
            .main_content_left_one_content_right_one_icon {
              width: 0;
              height: 0;
              border-left: 8px solid transparent;
              border-right: 8px solid transparent;
              border-bottom: 8px solid #12E7E8; /* 三角形颜色 */
              margin-left: 8px;
              margin-right: 5px;
            }
            .main_content_left_one_content_right_one_icon2 {
              width: 0;
              height: 0;
              border-left: 8px solid transparent;
              border-right: 8px solid transparent;
              border-bottom: 8px solid #4DA3FF; /* 三角形颜色 */
              margin-left: 8px;
              margin-right: 5px;
            }
            .main_content_left_one_content_right_one_icon3 {
              width: 0;
              height: 0;
              border-left: 8px solid transparent;
              border-right: 8px solid transparent;
              border-bottom: 8px solid #FFFFFF; /* 三角形颜色 */
              margin-left: 8px;
              margin-right: 5px;
            }
            .main_content_left_one_content_right_one_text {
              .main_content_left_one_content_right_one_text_one {
                display: flex;
                align-items: center;
                margin-bottom: 10px;
                .main_content_left_one_content_right_one_text_one_left {
                  font-size: 18px;
                  font-family: SourceHanSansCN;
                  font-weight: 400;
                  color: #12E7E8;
                  line-height: 1;
                  text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
                }
                .main_content_left_one_content_right_one_text_one_left2 {
                  font-size: 18px;
                  font-family: SourceHanSansCN;
                  font-weight: 400;
                  color: #4DA3FF;
                  line-height: 1;
                  text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
                }
                .main_content_left_one_content_right_one_text_one_left3 {
                  font-size: 18px;
                  font-family: SourceHanSansCN;
                  font-weight: 400;
                  color: #fff;
                  line-height: 1;
                  text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
                }
                .main_content_left_one_content_right_one_text_one_right {
                  font-size: 18px;
                  font-family: SourceHanSansCN;
                  font-weight: 400;
                  color: #FFFFFF;
                  line-height: 1;
                  text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
                  margin-left: 10px;
                }
                .main_content_left_one_content_right_one_text_one_right2 {
                  font-size: 18px;
                  font-family: SourceHanSansCN;
                  font-weight: 400;
                  color: #FFFFFF;
                  line-height: 1;
                  text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
                }
              }
            }
          }
        }
      }
    }
    .main_content_right {
      width: 500px;
      position: absolute;
      right: 113px;
      top: 0;

      .main_content_right_one {
        margin-top: 50px;

        .main_content_right_one_title {
          width: 100%;
          height: 50px;
          display: flex;
          align-items: center;
          background: url(../assets/img/011.png) 0 0 / 100% 100%;
          box-sizing: border-box;
          padding-left: 70px;
          .main_content_right_one_title_text {
            font-size: 23px;
            font-family: SourceHanSansCN;
            font-weight: 500;
            color: #FFFFFF;
            line-height: 1;
            text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
            margin-right: 18px;
          }
          .main_content_right_one_title_icon {
            width: 41.5px;
            height: 41.5px;
            background: url("../assets/img/005.png") 0 0 / 100% 100%;
          }
          .main_content_right_one_title_icon2 {
            width: 60px;
            height: 44px;
            background: url("../assets/img/007.png") 0 0 / 100% 100%;
          }
        }
        .main_content_right_one_content {
          width: 100%;
          height: 300px;

          .main_content_right_one_content_title {
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: space-between;
            font-size: 16px;
            font-family: SourceHanSansCN;
            font-weight: bold;
            color: #FFFFFF;
            line-height: 38px;
            text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
            box-sizing: border-box;
            padding: 0 100px 0 0;
            .main_content_right_one_content_title_name {

            }
            .main_content_right_one_content_title_shebei {

            }
            .main_content_right_one_content_title_status {

            }
          }
          .main_content_right_one_content_content {
            width: 100%;
            .main_content_right_one_content_content_ul {
              width: 100%;
              height: 260px;
              overflow: hidden;
              .main_content_right_one_content_content_ul_li {
                width: 455px;
                height: 34px;
                background: url("../assets/img/016.png") 0 0 / 100% 100%;
                display: flex;
                align-items: center;
                box-sizing: border-box;
                padding: 0 30px 0 18px;

                .main_content_right_one_content_content_ul_li_icon {
                  width: 16px;
                  height: 16.5px;
                  background: url("../assets/img/006.png") 0 0 / 100% 100%;
                  margin-right: 16.5px;
                }
                .main_content_right_one_content_content_ul_li_name {
                  width: 35%;
                  font-size: 16px;
                  font-family: SourceHanSansCN;
                  font-weight: 400;
                  color: #FFFFFF;
                  line-height: 1;
                  text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
                  overflow:hidden;
                  text-overflow:ellipsis;
                  white-space:nowrap;
                  margin-right: 10px;
                }
                .main_content_right_one_content_content_ul_li_shebei {
                  width: 40%;
                  font-size: 16px;
                  font-family: SourceHanSansCN;
                  font-weight: 400;
                  color: #FFFFFF;
                  line-height: 1;
                  text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
                  overflow:hidden;
                  text-overflow:ellipsis;
                  white-space:nowrap;
                  margin-right: 10px;
                }
                .main_content_right_one_content_content_ul_li_status {
                  width: 44px;
                  height: 18px;
                  background: #FF0000;
                  border-radius: 1px;
                  font-size: 11px;
                  font-family: SourceHanSansCN;
                  font-weight: 500;
                  color: #FFFFFF;
                  line-height: 18px;
                  text-align: center;
                }
                .main_content_right_one_content_content_ul_li_status2 {
                  width: 44px;
                  height: 18px;
                  background: #00D80A;
                  border-radius: 1px;
                  font-size: 11px;
                  font-family: SourceHanSansCN;
                  font-weight: 500;
                  color: #FFFFFF;
                  line-height: 18px;
                  text-align: center;
                }
              }
            }
          }
          .main_content_right_one_content_echarts {
            width: 100%;
            height: 100%;
          }
        }
        .main_content_right_one_content2 {
          width: 100%;
          height: 300px;
        }
      }
    }
  }
  .main_bottom {
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 43%;
    height: 65px;
    background: url("../assets/img/012.png") 0 0 / 100% 100%;
    .main_bottom_box {
      width: 90%;
      position: absolute;
      top: -90px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      box-sizing: border-box;
      padding: 0 101px 0 188px;
      .main_bottom_one {
        display: flex;
        align-items: center;
        .main_bottom_one_img1 {
          width: 98px;
          height: 90px;
          background: url("../assets/img/009.png") 0 0 / 100% 100%;
        }
        .main_bottom_one_img2 {
          width: 98px;
          height: 90px;
          background: url("../assets/img/010.png") 0 0 / 100% 100%;
        }
        .main_bottom_one_right {
          display: flex;
          flex-direction: column;
          align-items: center;
          margin-left: 30px;
          .main_bottom_one_right_title {
            font-size: 20px;
            font-family: SourceHanSansCN;
            font-weight: bold;
            color: #00CCFF;
            line-height: 1;
            text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
          }
          .main_bottom_one_right_num {
            display: flex;
            align-items: flex-end;
            margin-top: 10px;
            .main_bottom_one_right_num_num {
              font-size: 41px;
              font-family: FZLTCHJW;
              font-weight: normal;
              color: #FFCE23;
              line-height: 1;
              text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
            }
            .main_bottom_one_right_num_text {
              font-size: 15px;
              font-family: SourceHanSansCN;
              font-weight: 400;
              color: #FFFFFF;
              line-height: 1;
              text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
            }
          }
        }
      }
    }
  }
}
</style>
