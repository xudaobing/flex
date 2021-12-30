<script>
import Flex from './Flex.vue';
export default {
  name: 'Operation',
  props: {
    options: Object,
  },
  emits: ['update:options'],
  computed: {
    direction: {
      get() {
        return this.options?.direction;
      },
      set(direction) {
        this.updateOptions({
          direction,
        }) 
      }
    },
    justify: {
      get() {
        return this.options?.justify;
      },
      set(justify) {
        this.updateOptions({
          justify,
        }) 
      }
    },
    align: {
      get() {
        return this.options?.align;
      },
      set(align) {
        this.updateOptions({
          align,
        }) 
      }
    },
  },
  components: {
    Flex,
  },
  methods: {
    updateOptions(data) {
      const options = {
        ...this.options,
        ...data,
      };
      this.$emit('update:options', options);
    }
  },
}
</script>

<template>
<Flex tag="div">
  <Flex type="flex" justify="center" align="center">
    <div>主轴方向</div>
    <div>
      <select v-model="direction">
        <option disabled value="">请选择</option>
        <option value="row">水平</option>
        <option value="col">垂直</option>
      </select>
    </div>
  </Flex>
  <Flex type="flex" justify="center" align="center">
    <div>在主轴上的对齐方式</div>
    <div>
      <select v-model="justify">
        <option disabled value="">请选择</option>
        <option value="start">左对齐</option>
        <option value="center">居中</option>
        <option value="end">右对齐</option>
        <option value="between">两端对齐</option>
        <option value="around">间隔相等</option>
      </select>
    </div>
  </Flex>
  <Flex type="flex" justify="center" align="center">
    <div>在交叉轴上的对齐方式</div>
    <div>
      <select v-model="align">
        <option disabled value="">请选择</option>
        <option value="stretch">auto</option>
        <option value="start">起点对齐</option>
        <option value="center">居中</option>
        <option value="end">终点对齐</option>
        <option value="baseline">基线对齐</option>
      </select>
    </div>
  </Flex>
</Flex>
</template>