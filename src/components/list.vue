<template>
  <div class="uploader-list">
    <slot :file-list="fileList">
      <ul>
        <vuedraggable :options="options" @update="datadragEnd" >
          <li v-for="file in fileList" :key="file.id">
            <uploader-file :file="file" :list="true"></uploader-file>
          </li>
        </vuedraggable>
      </ul>
    </slot>
  </div>
</template>

<script>
  import {uploaderMixin} from '../common/mixins'
  import UploaderFile from './file.vue'
  import vuedraggable from 'vuedraggable'

  const COMPONENT_NAME = 'uploader-list'

  export default {
    name: COMPONENT_NAME,
    mixins: [uploaderMixin],
    computed: {
      fileList () {
        return this.uploader.fileList
      }
    },
    components: {
      UploaderFile,
      vuedraggable
    },
    data () {
      return {
        options: {
          // or { name: "...", pull: [true, false, clone], put: [true, false, array] } name相同的组可以互相拖动
          // group: 'name',
          // 内部排序列表
          sort: true,
          delay: 0, // 以毫秒为单位定义排序何时开始。
          // px,在取消延迟拖动事件之前，点应该移动多少像素?
          touchStartThreshold: 0,
          // ms, 动画速度运动项目排序时，' 0 ' -没有动画。
          animation: 200,
          // 在列表项中拖动句柄选择器。
          // handle: '.my-handle',
          // 不导致拖拽的选择器(字符串或函数)
          // filter: '.ignore-elements',
          // 调用“event.preventDefault()”时触发“filter”
          // preventOnFilter: true,
          // 指定元素中的哪些项应该是可拖动的。
          // draggable: '.item',
          // 设置拖动元素的class的占位符的类名。
          // ghostClass: 'sortable-ghost',
          // 设置被选中的元素的class
          // chosenClass: 'sortable-chosen',
          // 拖动元素的class。
          // dragClass: 'sortable-drag',
          // dataIdAttr: 'data-id',
          // 忽略HTML5的DnD行为，并强制退出。（h5里有个属性也是拖动，这里是为了去掉H5拖动对这个的影响）
          forceFallback: false,
          // 使用forceFallback时克隆的DOM元素的类名。
          // fallbackClass: 'sortable-fallback',
          // 将克隆的DOM元素添加到文档的主体中。（默认放在被拖动元素的同级）
          fallbackOnBody: false,
          // 用像素指定鼠标在被视为拖拽之前应该移动的距离。
          fallbackTolerance: 0,
          // or HTMLElement
          scroll: true,
          // scrollFn: function(offsetX, offsetY, originalEvent, touchEvt, hoverTargetEl) { ... }, // if you have custom scrollbar scrollFn may be used for autoscrolling
          // px, how near the mouse must be to an edge to start scrolling.
          scrollSensitivity: 30,
          // px
          scrollSpeed: 10
        }
      }
    },
    methods: {
      datadragEnd (evt) {
        console.log(evt)
      }
    }
  }
</script>

<style>
  .uploader-list {
    position: relative;
  }

  .uploader-list > ul {
    list-style: none;
    margin: 0;
    padding: 0
  }
</style>
