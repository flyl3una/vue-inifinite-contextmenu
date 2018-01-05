<template>
	<div id="demo" @contextmenu="openContextMenu($event)" @click="show=false">
		<img src="/src/assets/logo.png">
		<h3>灰色面板中点击鼠标右键可显示无限级右键菜单</h3>
		<infinite-right-menu :list="lists" :startX="this.rightMenuX+'px'" :startY="this.rightMenuY+'px'"
												 :show="this.show" @refreshbizlines="clickEvent"></infinite-right-menu>
	</div>
</template>

<script>
  import InfiniteRightMenu from '@/components/InfiniteRightMenu'
  export default {
    name: 'Demo',
    data () {
      return {
        rightMenuX: 0,
        rightMenuY: 0,
        msg: 'Welcome to Your Vue.js App',
				rightMenuTarget: null,
        startX: 0,
        startY: 0,
        show: false,
        lists: [
          {
            clickIndex: 1,
            headIcon: 'iconfont icon-folder-share',
            label: '下么哈哈',
            tailIcon: 'iconfont icon-xiayibu',
            childrens: [
              {
                clickIndex: 2,
                headIcon: 'iconfont icon-xiaoxi2',
                label: 'abc',
                tailIcon: 'iconfont icon-xiayibu'
              },
              {
                clickIndex: 3,
                headIcon: 'iconfont icon-xiaoxi2',
                label: '放大撒',
                tailIcon: 'iconfont icon-xiayibu'
              }
            ]
          },
          {
            clickIndex: 4,
            headIcon: 'iconfont icon-weizhi',
            label: 'ddd',
            tailIcon: 'iconfont icon-xiayibu',
            divide: true,
            childrens: [
              {
                clickIndex: 5,
                headIcon: 'iconfont icon-folder-share',
                label: 'dba',
                tailIcon: 'iconfont icon-xiayibu'
              },
              {
                clickIndex: 6,
                headIcon: 'iconfont icon-folderopen',
                label: 'addsaa',
                tailIcon: 'iconfont icon-xiayibu',
                childrens: [
                  {
                    clickIndex: 7,
                    headIcon: 'iconfont icon-folder-share',
                    label: '下么哈哈',
                    tailIcon: 'iconfont icon-xiayibu',
                    childrens: [
                      {
                        clickIndex: 8,
                        headIcon: 'iconfont icon-xiaoxi2',
                        label: 'abc',
                        tailIcon: 'iconfont icon-xiayibu'
                      },
                      {
                        clickIndex: 9,
                        headIcon: 'iconfont icon-xiaoxi2',
                        label: '放大撒',
                        tailIcon: 'iconfont icon-xiayibu'
                      }
                    ]
                  },
                  {
                    clickIndex: 10,
                    headIcon: 'iconfont icon-weizhi',
                    label: 'ddd',
                    tailIcon: 'iconfont icon-xiayibu',
                    childrens: [
                      {
                        clickIndex: 11,
                        headIcon: 'iconfont icon-folder-open',
                        label: 'dba',
                        tailIcon: 'iconfont icon-xiayibu',
                        divide: true
                      },
                      {
                        clickIndex: 12,
                        headIcon: 'iconfont icon-xiaoxi2',
                        label: 'addsaa',
                        tailIcon: 'iconfont icon-xiayibu'
                      }
                    ]
                  },
                ]
              }
            ]
          },
          {
            clickIndex: 13,
            headIcon: 'iconfont icon-shouye2',
            label: '过分的事',
            tailIcon: 'iconfont icon-xiayibu',
            childrens: [
              {
                clickIndex: 14,
                headIcon: 'iconfont icon-xiaoxi2',
                label: 'abacaa',
                tailIcon: 'iconfont icon-xiayibu'
              },
              {
                clickIndex: 15,
                headIcon: 'iconfont icon-xiaoxi2',
                label: 'adaeaa',
                tailIcon: 'iconfont icon-xiayibu'
              }
            ]
          }
        ],
      }
    },
    methods: {
      clickEvent (index) {
//			switch index. Distribute function according to index and this.rightMenuTarget
        console.log('click ' + index)
				if (this.rightMenuTarget) {
          console.log(this.rightMenuTarget.innerText)
				} else {
          console.log("haven't target")
				}
        alert('click ' +  index)
      },

      openContextMenu(event) {
//        param: user right param
        var e = event||window.event;	//support firefox contextmenu
				this.rightMenuTarget = event.target
        this.show = false
        this.rightMenuX = e.clientX + document.documentElement.scrollLeft - document.documentElement.clientLeft
        this.rightMenuY = e.clientY + document.documentElement.scrollTop  - document.documentElement.clientTop
        event.preventDefault()
        event.stopPropagation()
        this.$nextTick(() => {
          this.show = true
        })
      }

    },
    components: {
      InfiniteRightMenu
    }
  }
</script>

<style scoped>
	#demo{
		width: 1000px;
		height: 1500px;
		background: #f5f5f5;
		border: 1px solid #e6e6e6;
		margin: auto;
		text-align: center;
		justify-content: center;
		cursor: pointer;
	}
</style>
