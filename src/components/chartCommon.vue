<template>
  <section
    ref="chartContainer"
    :class="className"
    :style="{ width: width, height: height }"
  ></section>
</template>

<script setup lang="ts">
import { init, ECharts, EChartsOption } from "echarts";
import { ref, watch, withDefaults, onMounted, onBeforeUnmount } from "vue";

interface IProps {
  className?: string;
  width?: string;
  height?: string;
  chartOptions: EChartsOption;
}

const props = withDefaults(defineProps<IProps>(), {
  className: "commonChart",
  width: "100%",
  height: "100%",
  chartOptions: () => ({}),
});

const chartContainer = ref<HTMLElement>();
let chartInstance: ECharts | null = null;
const initEcharts = (): void => {
  chartInstance = init(chartContainer.value as HTMLElement, void 0, {
    width: "auto",
    height: "auto",
  });
  chartInstance.setOption(props.chartOptions, true);
};

onMounted(() => {
  initEcharts();
  window.addEventListener("resize", () => {
    chartInstance?.resize();
  });
});

watch(
  () => props.chartOptions,
  (newOptions) => {
    if (newOptions) {
      chartInstance?.setOption(newOptions, true);
    }
  },
  {
    deep: true,
  }
);

onBeforeUnmount(() => {
  if (chartInstance) {
    chartInstance.dispose();
    chartInstance = null;
  }
});
</script>

<style lang="less" scoped>
.commonChart {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}
</style>
