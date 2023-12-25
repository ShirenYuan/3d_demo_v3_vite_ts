<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <div class="main">
      <TheWelcome class="main_3d" />
      <!-- top -->
      <div class="main_top">
        <div class="main_top_left">
          <div class="main_top_left_left">
            <div class="main_top_left_left_icon"></div>
            <div class="main_top_left_left_tianqi"></div>
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
          <div class="main_top_right_date">9:00</div>
          <div class="main_top_right_year">2023.12.20</div>
          <div class="main_top_right_week">星期一</div>
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
                <div class="main_content_left_one_content_one_echarts"></div>
                <div class="main_content_left_one_content_one_text">使用中</div>
              </div>
              <div class="main_content_left_one_content_one">
                <div class="main_content_left_one_content_one_echarts"></div>
                <div class="main_content_left_one_content_one_text">使用统计</div>
              </div>
              <div class="main_content_left_one_content_one">
                <div class="main_content_left_one_content_one_echarts"></div>
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
                  <div class="main_content_left_one_content_right_one_name">实验仪器名称1</div>
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
                  <div class="main_content_left_one_content_right_one_name">实验仪器名称2</div>
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
                  <div class="main_content_left_one_content_right_one_name">实验仪器名称3</div>
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
                  <div class="main_content_right_one_content_content_ul_li">
                    <div class="main_content_right_one_content_content_ul_li_icon"></div>
                    <div class="main_content_right_one_content_content_ul_li_name">xx实验室</div>
                    <div class="main_content_right_one_content_content_ul_li_shebei">实验设备名称xx</div>
                    <div class="main_content_right_one_content_content_ul_li_status">使用中</div>
                  </div>
                  <div class="main_content_right_one_content_content_ul_li">
                    <div class="main_content_right_one_content_content_ul_li_icon"></div>
                    <div class="main_content_right_one_content_content_ul_li_name">xx实验室</div>
                    <div class="main_content_right_one_content_content_ul_li_shebei">实验设备名称xx</div>
                    <div class="main_content_right_one_content_content_ul_li_status2">未使用</div>
                  </div>
                  <div class="main_content_right_one_content_content_ul_li">
                    <div class="main_content_right_one_content_content_ul_li_icon"></div>
                    <div class="main_content_right_one_content_content_ul_li_name">xx实验室</div>
                    <div class="main_content_right_one_content_content_ul_li_shebei">实验设备名称xx</div>
                    <div class="main_content_right_one_content_content_ul_li_status">使用中</div>
                  </div>
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
            <div class="main_content_right_one_content">
              <div class="main_content_right_one_content_echarts"></div>
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
    height: 7%;
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
    .main_top_left {
      display: flex;
      align-items: center;
      .main_top_left_left {
        display: flex;
        .main_top_left_left_icon {
          width: 14.25px;
          height: 23.1px;
          background: url("../assets/img/001.png") 0 0 / 100% 100%;
          margin-right: 14.5px;
        }
        .main_top_left_left_tianqi {

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
        height: 400px;
        .main_content_left_one_title {
          display: flex;
          align-items: flex-end;
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
          justify-content: center;
        }
        .main_content_left_one_content_one {
          display: flex;
          flex-direction: column;
          align-items: center;
          margin-right: 25px;
          .main_content_left_one_content_one_echarts {
            width: 135.3px;
            height: 135.3px;
            background: red;
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
        .main_content_right_one_title {
          display: flex;
          align-items: flex-end;
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
          height: 100%;

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
                  font-size: 16px;
                  font-family: SourceHanSansCN;
                  font-weight: 400;
                  color: #FFFFFF;
                  line-height: 1;
                  text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
                  margin-right: 51.5px;
                }
                .main_content_right_one_content_content_ul_li_shebei {
                  font-size: 16px;
                  font-family: SourceHanSansCN;
                  font-weight: 400;
                  color: #FFFFFF;
                  line-height: 1;
                  text-shadow: 0px 5px 5px rgba(1,1,1,0.2);
                  margin-right: 89px;
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

          }
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
