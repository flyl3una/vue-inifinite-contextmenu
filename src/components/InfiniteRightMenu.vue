<template>
	<transition name='fade'>
		<ul class="menu-ui" :style="{left:startX, top:startY}" v-if="show">
			<li v-for="(item, index) in list" @mouseover="showIndex=index" @mouseleave="showIndex=-1" :key="index">
				<a :class="item['divide'] ? 'divide':''" @click="emitClickEvent($event, item)">
					<i :class="item.headIcon" class="head-icon"></i>
					<span>{{ item.label}}</span>
					<i :class="item.tailIcon" class="tail-icon"></i>
				</a>
				<infinite-right-menu v-if="showChildren(item)" @refreshbizlines="emitClick"
														 :list="item.childrens" :startX="'100%'" :startY="'0'"
														 :show="showList(index)"></infinite-right-menu>
			</li>
		</ul>
	</transition>
</template>

<script>
  export default {
    name: 'InfiniteRightMenu',
    props: {
      startX: {// start x
        type: [String],
        required: false,
        default: '0'
      },
      startY: {// start y
        type: [String],
        required: false,
        default: '0'
      },
      list: {// data
        type: [Array],
        required: true,
        default: function () {
          return []
        }
      },
      show: {
        type: [Boolean],
        required: false,
        default: false
      }
    },
    data: () => ({
      showIndex: -1
    }),
    methods: {
      showChildren(item) {
        if (!item.childrens || !item.childrens.length) {
          return false
        } else {
          return true
        }
      },
      showList(index) {
        if (this.showIndex === index) {
          return true
        } else {
          return false
        }
      },
      emitClick (index) {
//        emit the event to parent
        this.$emit('refreshbizlines', index)
      },
      emitClickEvent (event, item) {
        event = event || window.event
        if (!this.showChildren(item)) {
          this.emitClick (item.clickIndex)
				}
        else {
          event.cancelBubble = true
          event.stopPropagation()
				}
			}
    },
    computed: {}
  }
</script>

<style scoped="">
	.menu-ui {
		position: absolute;
		background: white;
		width: 140px;
		display: list-item;
		box-shadow: 0 1px 16px 0 rgba(90, 109, 122, 0.41);
		list-style: none;
		padding: 10px 0;
		z-index: 1000;
		margin: 0;
	}

	.fade-enter-active {
		transition: all .4s ease;
	}
	.fade-leave-active {
		transition: all .1s cubic-bezier(1.0, 0.5, 0.8, 1.0);
	}
	.fade-enter, .fade-leave-to {
		transform: translateY(-10px);
		opacity: 0;
	}

	li {
		position: relative;
	}

	a {
		text-decoration: none;
		position: relative;
		display: block;
		cursor: pointer;
		align-items: center;
		padding: 0 10px;
		height: 32px;
		line-height: 32px;
		color: #616161;
	}

	.divide {
		border-bottom: 1px solid #e6e6e6;
	}

	li:hover {
		background-color: #4CAF50;
	}

	li:hover > a > span {
		color: white;
	}

	a > span {
		position: relative;
		float: left;
		padding-left: 20px;
		font-size: 14px;
		text-overflow: ellipsis;
		overflow: hidden;
		word-break: break-all;
	}

	i {
		font-size: 17px !important;
	}

	.head-icon {
		position: absolute;
		left: 10px;
	}

	.tail-icon {
		position: relative;
		float: right;
	}
</style>