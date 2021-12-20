<script setup>
import Flex from './components/Flex.vue'
</script>

<template>
  <Flex type="flex">
    <Flex class="flex-box" 
      tag="section" type="flex" direction="row" wrap="wrap-reverse"
      justify="around" align="center">
      <Flex class="flex-item" type="flex" justify="center" align="center">1</Flex>
      <Flex class="flex-item" type="flex" justify="center" align="center">2</Flex>
      <Flex class="flex-item" type="flex" justify="center" align="center">3</Flex>
      <Flex class="flex-item" type="flex" justify="center" align="center">4</Flex>
      <Flex class="flex-item" type="flex" justify="center" align="center">5</Flex>
      <Flex class="flex-item" type="flex" justify="center" align="center">6</Flex>
      <Flex class="flex-item" type="flex" justify="center" align="center">7</Flex>
      <Flex class="flex-item" type="flex" justify="center" align="center">8</Flex>
      <Flex class="flex-item" type="flex" justify="center" align="center">9</Flex>
    </Flex>
    <Flex>
      
    </Flex>
  </Flex>
</template>

<style>
#app {
  min-height: 100vh;
}
.flex-box {
  width: 500px;
  height: 500px;
  background-color: rgba(0, 0, 0, .1);
}
.flex-item {
  width: 120px;
  height: 120px;
  /* padding: 30px 50px; */
  background-color: #999;
  font-size: 30px;
  line-height: 1;
  color: #fff;
  border-radius: 5px;
  margin: 4px;
}
</style>
