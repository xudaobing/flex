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

// justify-content属性 在主轴上的对齐方式
const JUSTIFY_CONTENT = {
  start: 'justify-start',
  center: 'justify-center',
  end: 'justify-end',
  between: 'justify-space-between',
  around: 'justify-space-around',
}

// align-items属性 在交叉轴上如何对齐
const ALIGN_ITEMS = {
  start: 'align-start',
  center: 'align-center',
  end: 'align-end',
  baseline: 'align-baseline',
  stretch: 'align-stretch',
};

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
    console.log(context.slots)
    const { slots } = context;
    const elClass = {};
    const isFlex = props.type === 'flex';
    const isInlineFlex = props.type === 'inline-flex';
    
    
    if (isFlex) elClass.flex = true;
    if (isInlineFlex) elClass['inline-flex'] = true;

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

      // 项目在主轴上的对齐方式
      if (props.justify && (k = JUSTIFY_CONTENT[props.justify])) {
        elClass[k] = true;
      }

      // 项目在交叉轴上如何对齐
      if (props.align && (k = ALIGN_ITEMS[props.align])) {
        elClass[k] = true;
      }
    }

    const children = typeof slots.default === 'function' ? slots.default() : slots.default;

    return () => h(props.tag || 'div', {
      class: elClass,
    }, children);
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

  //  justify-content
  &.justify-start {
    justify-content: flex-start;
  }
  &.justify-center {
    justify-content: center;
  }
  &.justify-end {
    justify-content: flex-end;
  }
  &.justify-space-between {
    justify-content: space-between;
  }
  &.justify-space-around {
    justify-content: space-around;
  }

  //  align-items
  &.align-start {
    align-items: flex-start;
  }
  &.align-center {
    align-items: center;
  }
  &.align-end {
    align-items: flex-end;
  }
  &.align-baseline {
    align-items: baseline;
  }
  &.align-stretch {
    align-items: stretch;
  }
}
</style>
