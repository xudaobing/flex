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
        <option value="row">水平</option>
        <option value="col">垂直</option>
      </select>
    </div>
  </Flex>
  <Flex type="flex" justify="center" align="center">
    <div></div>
    <div></div>
  </Flex>
</Flex>
</template>