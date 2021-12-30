<script setup>
import { reactive } from 'vue';
import Flex from './components/Flex.vue';
import Operation from './components/Operation.vue';

const porps = reactive({
  direction: '',
  wrap: '',
  justify: '',
  align: '',
  children: 2,
});

function updatePorps(data) {
  Object.assign(porps, data);
}
</script>

<template>
  <Flex tag="div" type="flex">
    <Flex class="box" 
      type="flex" :direction="porps.direction" :wrap="porps.wrap"
      :justify="porps.justify" :align="porps.align">
      <Flex v-for="i in porps.children" :key="i"
        class="flex-item" type="flex" justify="center" align="center">{{ i }}</Flex>
    </Flex>
    <Operation :options="porps" @update:options="updatePorps" />
  </Flex>
</template>

<style>
#app {
  min-height: 100vh;
  padding: 10px;
}
.box {
  width: 200px;
  height: 200px;
  padding: 10px;
  border-radius: 10px;
  background-color: #000;
  margin-right: 20px;
}

.flex-item {
  width: 40px;
  height: 40px;
  background-color: #fff;
  font-size: 16px;
  line-height: 1;
  color: #666;
  border-radius: 5px;
}
</style>
