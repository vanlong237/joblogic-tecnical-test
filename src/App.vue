<template>
<main class="main-wrapper">
  <LeftSideBar @onSelect="handleSelected" />
  <MainDetails
    :details="employees[selectedIndex]"
    @onChangePopularity="handleChangePopularity"
  />
</main>
</template>
<script setup>
import { provide, reactive, ref } from 'vue';
import employeeData from './assets/EmployeeData.json';
import LeftSideBar from './components/LeftSideBar.vue';
import MainDetails from './components/MainDetails.vue';
import { PROVIDE_KEY } from './constants';

const employees = reactive(employeeData.employees);
provide(PROVIDE_KEY.EMPLOYEE_DATA, employees);

const selectedIndex = ref(0);
provide(PROVIDE_KEY.SELECTED_INDEX, selectedIndex);

const histories = ref([0]);
provide(PROVIDE_KEY.HISTORIES, histories);

const handleSelected = (index) => {
  selectedIndex.value = index;
  histories.value = Array.from(new Set([...histories.value, index]).values());
}

const handleChangePopularity = (newValue) => {
  employees[selectedIndex.value].popularity = newValue;
}

</script>

<style>
.main-wrapper {
  width: 100vw;
  min-height: 100vh;
}
</style>
