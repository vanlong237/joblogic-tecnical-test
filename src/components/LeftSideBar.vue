<template>
  <button v-if="!open" class="btn btn--open" @click="() => open = true">
    <span></span>
    <span></span>
    <span></span>
  </button>
  <nav :class="{
    navigation: true,
    'navigation--show': open
  }">
    <button class="btn btn--close" @click="() => open = false">
      &times;
    </button>
    <header class="navigation__header">
      <img class="navigation__header__logo" alt="logo" src="@/assets/_logo/the-godfather.svg" />
    </header>
    <ul class="employees-list">
      <li
        v-for="(item, index) in employees"
        :key="index"
        :class="{
          'employee-item': true,
          'employee-item--active': selectedIndex === index,
          'employee-item--selected': histories.includes(index)
        }"
        v-bind:style="{
          fontSize: `${8 * item.popularity}px`
        }"
        @click="() => { $emit('onSelect', index); open = false; }"
      >
        {{ item.name }}
      </li>
    </ul>
  </nav>
</template>
<script setup>
import { inject, ref } from 'vue';
import { PROVIDE_KEY } from '../constants';

const employees = inject(PROVIDE_KEY.EMPLOYEE_DATA, []);
const selectedIndex = inject(PROVIDE_KEY.SELECTED_INDEX, 0);
const histories = inject(PROVIDE_KEY.HISTORIES, []);

const open = ref(false)

</script>
<style>
.navigation {
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  bottom: 0;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.3);
  width: 300px;
  transition: all ease-in-out 0.25s;
}
.navigation__header {
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.employees-list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  list-style-type: none;
  padding: 0;
  margin: 0;
  margin-top: 20px;
}
.employee-item {
  color: #ffffff;
  text-align: center;
  padding: 0.5rem;
  display: block;
}
.employee-item--active,
.employee-item:hover {
  background: rgba(255, 255, 255, 0.3);
  cursor: pointer;
}
.employee-item--selected,
.employee-item--active {
  color: #3dd1f8;
}
.btn {
  background-color: transparent; /* Blue background */
  border: none; 
  color: white;
  padding: 1rem;
  cursor: pointer;
  outline: none;
}
.btn--open span {
  width: 20px;
  height: 4px;
  background-color: #ffff;
  display: block;
  margin: 4px;
}
.btn--open {
  position: fixed;
  top: 20px;
  left: 20px;
}
.btn--close {
  position: absolute;
  top: 20px;
  right: 20px;
  font-size: 2rem;
  line-height: 0.5;
}
@media only screen and (min-width: 769px) {
  .btn {
    display: none;
  }
}
@media only screen and (max-width: 768px) {
  .navigation {
    margin-left: -100%;
    background-color: rgba(0, 0, 0, 0.8);
    width: 100%;
  }
  .navigation--show {
    margin-left: 0;
  }
}
</style>