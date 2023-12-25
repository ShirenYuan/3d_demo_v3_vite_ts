<template>
  <div>
    <div id="he-plugin-simple"></div>
  </div>
</template>

<script lang="ts">
import { ref, onMounted } from 'vue';

export default {
  name: 'WeatherWidget',
  setup() {
    const widgetConfig = {
      "CONFIG": {
        "modules": "01234",
        "background": "5",
        "tmpColor": "98B9D9",
        "tmpSize": "16",
        "cityColor": "98B9D9",
        "citySize": "16",
        "aqiColor": "98B9D9",
        "aqiSize": "16",
        "weatherIconSize": "24",
        "alertIconSize": "18",
        "padding": "10px 10px 10px 10px",
        "shadow": "0",
        "language": "auto",
        "fixed": "false",
        "vertical": "top",
        "horizontal": "left",
        "key": "1028798cef9147acbbbe840d58bbea75"
      }
    };

    onMounted(() => {
      // 在组件挂载后执行的代码
      window.WIDGET = widgetConfig;
      const script = document.createElement('script');
      script.src = 'https://widget.qweather.net/simple/static/js/he-simple-common.js?v=2.0';
      document.head.appendChild(script);
    });

    return {};
  }
}
</script>
