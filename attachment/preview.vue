<template>
  <div class="pswp" tabindex="-1" role="dialog" aria-hidden="true">

    <!-- Background of PhotoSwipe.
         It's a separate element as animating opacity is faster than rgba(). -->
    <div class="pswp__bg"></div>

    <!-- Slides wrapper with overflow:hidden. -->
    <div class="pswp__scroll-wrap">

      <!-- Container that holds slides.
          PhotoSwipe keeps only 3 of them in the DOM to save memory.
          Don't modify these 3 pswp__item elements, data is added later on. -->
      <div class="pswp__container">
        <div class="pswp__item"></div>
        <div class="pswp__item"></div>
        <div class="pswp__item"></div>
      </div>

      <!-- Default (PhotoSwipeUI_Default) interface on top of sliding area. Can be changed. -->
      <div class="pswp__ui pswp__ui--hidden">

        <div class="pswp__top-bar">

          <!--  Controls are self-explanatory. Order can be changed. -->

          <div class="pswp__counter"></div>

          <button class="pswp__button pswp__button--close" title="退出"></button>

          <button class="pswp__button pswp__button--share" title="Share"></button>

          <button class="pswp__button pswp__button--fs" title="Toggle fullscreen"></button>

          <button class="pswp__button pswp__button--zoom" title="放大/还原"></button>

          <!--20180414 xj add-->
          <button class="pswp__button pswp__button--rotate" title="旋转" @click="imgRotateFn"></button>

          <!-- Preloader demo http://codepen.io/dimsemenov/pen/yyBWoR -->
          <!-- element will get class pswp__preloader--active when preloader is running -->
          <div class="pswp__preloader">
            <div class="pswp__preloader__icn">
              <div class="pswp__preloader__cut">
                <div class="pswp__preloader__donut"></div>
              </div>
            </div>
          </div>
        </div>

        <div class="pswp__share-modal pswp__share-modal--hidden pswp__single-tap">
          <div class="pswp__share-tooltip"></div>
        </div>

        <!--xj edit Previous (arrow left)改为上一张-->
        <button class="pswp__button pswp__button--arrow--left" title="上一张" @click="initRotateFn">
        </button>

        <!--xj edit Next (arrow right)改为下一张-->
        <button class="pswp__button pswp__button--arrow--right" title="下一张" @click="initRotateFn">
        </button>

        <div class="pswp__caption">
          <div class="pswp__caption__center"></div>
        </div>

      </div>

    </div>

  </div>
</template>

<script>
  import PhotoSwipe from 'photoswipe/dist/photoswipe'
  import UI from 'photoswipe/dist/photoswipe-ui-default'
  export default {
      // xj add data 20180416
      data () {
          return{
            xjAngle: 0
          }
      },
    methods: {
      open (index, list, params = {
        captionEl: false,
        fullscreenEl: false,
        history: false,
        shareEl: false,
        tapToClose: true
      }) {
        let options = Object.assign({
          index: index,
          getThumbBoundsFn (index) {
            let thumbnail = document.querySelectorAll('.preview-img')[index]
            let pageYScroll = window.pageYOffset || document.documentElement.scrollTop
            let rect = thumbnail.getBoundingClientRect()
            return {x: rect.left, y: rect.top + pageYScroll, w: rect.width}
          }
        }, params)
        this.photoswipe = new PhotoSwipe(this.$el, UI, list, options)
        this.photoswipe.init()
      },
      close () {
        this.photoswipe.close()
      },
        // 20180414 xj add imgRotateFn
        imgRotateFn () {
          // let current;
          // document.getElementById('xjqbcd').style.WebkitTransform = 'rotate('+current+'deg)';
          this.xjAngle+=90;
          let imgNode = document.getElementsByClassName('pswp__img');
          for (let i = 0; i<imgNode.length; i++) {
              imgNode[i].style.WebkitTransform = 'rotate('+this.xjAngle+'deg)';
          }
        },
        initRotateFn () {
            this.xjAngle = 0;
            let imgNode = document.getElementsByClassName('pswp__img');
            for (let i = 0; i<imgNode.length; i++) {
                imgNode[i].style.WebkitTransform = 'rotate('+this.xjAngle+'deg)';
            }
        }
        // 20180414 xj add end
    }
  }
</script>

<style>
  @import '~photoswipe/dist/photoswipe.css';
  @import '~photoswipe/dist/default-skin/default-skin.css';
</style>
