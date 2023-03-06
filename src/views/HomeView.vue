<script setup>
import { computed, ref, onMounted } from "vue";
import { useMainStore } from "@/stores/main";
import {
  mdiAccountMultiple,
  mdiCartOutline,
  mdiChartTimelineVariant,
  mdiMonitorCellphone,
  mdiReload,
  mdiGithub,
  mdiChartPie,
} from "@mdi/js";
import * as chartConfig from "@/components/Charts/chart.config.js";
import LineChart from "@/components/Charts/LineChart.vue";
import SectionMain from "@/components/SectionMain.vue";
import CardBoxWidget from "@/components/CardBoxWidget.vue";
import CardBox from "@/components/CardBox.vue";
import TableSampleClients from "@/components/TableSampleClients.vue";
import TableComplete from "@/components/TableComplete.vue";
import TablePending from "@/components/TablePending.vue";
import TableFailed from "@/components/TableFailed.vue";
import NotificationBar from "@/components/NotificationBar.vue";
import BaseButton from "@/components/BaseButton.vue";
import CardBoxTransaction from "@/components/CardBoxTransaction.vue";
import CardBoxClient from "@/components/CardBoxClient.vue";
import LayoutAuthenticated from "@/layouts/LayoutAuthenticated.vue";
import SectionTitleLineWithButton from "@/components/SectionTitleLineWithButton.vue";
import SectionBannerStarOnGitHub from "@/components/SectionBannerStarOnGitHub.vue";
import UserCard from "@/components/UserCard.vue";

const chartData = ref(null);

const fillChartData = () => {
  chartData.value = chartConfig.sampleChartData();
};

onMounted(() => {
  fillChartData();
});

const mainStore = useMainStore();

const clientBarItems = computed(() => mainStore.clients.slice(0, 4));

const transactionBarItems = computed(() => mainStore.history);
</script>

<template>
  <LayoutAuthenticated>
    <SectionMain class='before:content-[""] before:bg-black before:fixed before:top-0 before:left-0 before:right-0 before:bottom-0 before:bg-[url("http://s3.amazonaws.com/reeve-assets-production/iStock-1327760987-CNS.jpg")] before:bg-cover before:bg:-center before:opacity-90'>
      <div class="bg-opacity-50 rounded-md backdrop-blur bg-green-500 h-14 w-2/5">
      <SectionTitleLineWithButton
        :icon="mdiChartTimelineVariant"
        title="NewOLO Dashboard"
        main
        class = "relative text-green-100 font-semibold"
      >
      </SectionTitleLineWithButton>
      </div>

      <UserCard class="mb-6" />
      

      <div class="grid grid-cols-1 gap-6 lg:grid-cols-3 mb-6">
        <CardBox has-table>
          <TableComplete/>
        </CardBox>
        <CardBox has-table>
          <TablePending />
        </CardBox>
        <CardBox has-table>
          <TableFailed />
        </CardBox>
      </div>

      <SectionTitleLineWithButton :icon="mdiChartPie" title="Trends overview" class="relative text-white">
        <BaseButton
          :icon="mdiReload"
          color="whiteDark"
          @click="fillChartData"
          class="relative"
        />
      </SectionTitleLineWithButton>

      <CardBox class="mb-6">
        <div v-if="chartData">
          <line-chart :data="chartData" class="h-96" />
        </div>
      </CardBox>
      
    </SectionMain>
  </LayoutAuthenticated>
</template>
