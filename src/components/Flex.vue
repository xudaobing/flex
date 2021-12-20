<script>
import { h } from 'vue'

// flex-direction 属性，主轴方向
const FLEX_DIRECTION = {
  row: 'row',    // 主轴为水平方向，起点在左端
  'row-reverse': 'row-reverse', // 主轴为水平方向，起点在右端
  col: 'column', // 主轴为垂直方向，起点在上端
  'col-reverse': 'column-reverse', // 主轴为垂直方向，起点在低端
};

// flex-wrap 属性，是否换行
const FLEX_WRAP = [
  'nowrap', // 默认值，不换行
  'wrap',   // 换行
  'wrap-reverse', // 换行，排序从底部开始
];

// 在主轴上的对齐方式
const JUSTIFY_CONTENT = {
  start: 'flex-start',
  center: 'center',
  end: 'flex-end',
  between: 'space-between',
  around: 'space-around',
}


export default {
  props: {
    tag: String,       // 布局标签，  默认div
    type: String,      // 布局模式，  可选 "flex" || ""
    direction: String, // direction  flex布局下 主轴方向，可选
    wrap: String,      // 是否换行、或换行排序, 默认nowrap
    justify: String,   // justify    flex布局下 水平排列方式
    align: String,     // align      flex布局下 垂直排列方式
  },
  setup(props, context) {
    console.log(props, context)
    const { attrs, slots } = context;

    const isFlex = props.type === 'flex';
    const isInlineFlex = props.type === 'inline-flex';
    // const isColumn = props.direction === 'column' || props.direction === 'column-reverse';
    
    const elClass = {
      flex: isFlex,
      'inline-flex': isInlineFlex,
      // 'row-reverse': props.direction === 'reverse',
      // 'column': props.direction === 'column',
      // 'column-reverse': props.direction === 'column-reverse',
      // flex-wrap属性
      // wrap: props.wrap === 'wrap',
      // 'wrap-reverse': props.wrap === 'wrap-reverse',
    };
    let k;
    if (isFlex || isInlineFlex) {
      // 主轴方向
      if (props.direction && (k = FLEX_DIRECTION[props.direction])) {
        elClass[k] = true;
      }

      // 是否换行
      if ((k = props.wrap) && FLEX_WRAP.includes(k)) {
        elClass[k] = true;
      }
    }

    return () => h(props.tag || 'div', {
      class: elClass,
    }, slots.default())
  }
};
</script>

<style lang="scss" scoped>
.flex {
  display: flex;

  &.row-reverse {
    flex-direction: row-reverse;
  }

  &.column {
    flex-direction: column;
  }

  &.column-reverse {
    flex-direction: column-reverse;
  }

  // flex-wrap
  &.wrap {
    flex-wrap: wrap;
  }
  &.wrap-reverse {
    flex-wrap: wrap-reverse;
  }
}
</style>
