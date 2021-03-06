# vgSrc
## 简介
一个简单的 Angular 图片加载插件，插件根据图片资源的不同加载状态，显示不同图片。

##  使用
1.  推荐使用 bower 加载：
  ```bash
  bower install vgSrc --save
  ```
    并引入：
  ```html
  <script src="/bower_components/vgSrc/dist/vgSrc.min.js"></script>
  ```

1.  也可下载源码，在页面引入：
  ```html
  <script src="/libs/vgSrc/dist/vgSrc.min.js"></script>}
  ```

##  example
1.  简单实例
  ```html
  <img vg-src="ctrl.currentImg" alt="">
  ```

1.  添加样式
  ```html
  <img vg-src="ctrl.currentImg" loading-cls="loading" error-cls="error" empty-cls="empty" loaded-cls="load" alt="">
  ```

1.  监听事件
  ```html
  <img vg-src="ctrl.currentImg" loading-cls="loading" error-cls="error" empty-cls="empty" loaded-cls="load" alt="">
  ```

更多实例，请查阅 **[sample/index.html](https://github.com/VanMess/vgSrc/blob/master/sample/index.html)** 文件

##  API
####    vgSrcConfigProvider
配置接口：
  ```javascript
  vgSrcConfigProvider.$set(config)
  ```

example:
  ```javascript
  ng.module('vgSrc.sample', ['vgSrc']).config([
    'vgSrcConfigProvider',
    function(vgSrcConfigProvider) {
        vgSrcConfigProvider.$set({
            debug: false,
            error: 'http://ico.ooopic.com/iconset01/status-icons/gif/99589.gif',
            onBegin: function($e) {
                // console.log('start load:' + $e.src);
            },
            onError: function($e) {
                // console.log('failure load:' + $e.src);
            },
            onLoad: function($e) {
                //  console.log('complete load:' + $e.src);
            }
        });
    }
  ]);
  ```

####    vgSrc (directive)
vgSrc 指令用法与 ngSrc 指令类型。指令支持 angular 表达式，如.
  ```html
  <img vg-src="ctrl.currentImg" alt="">
  <img vg-src="'/img/someImage.png'" alt="">
  ```

##  配置项
####    替换图片
vgSrc 支持 loading、error、empty 状态下的图片替换：

1.  vgSrc 指令求值结果为空时(null、undefined、空字符串)，将显示 empty 值指定的图片
1.  开始加载时，将显示 loading 值指定的图片
1.  加载出错时，将显示 error 值指定的图片
1.  加载成功后，正常显示图片

####    事件
vgSrc 支持 onBegin、onError、onLoad 事件，可通过 vgSrcConfigProvider 、 vgSrc 两种方式注册不同类型的事件处理器：

1.  通过 vgSrcConfigProvider 方式注册的监听器将做为默认的事件监听器，事件参数为：`$e{src:''}`，用法如：
  ```javascript
  onBegin:function($e){
    console.log($e.src);
  }
  ```

1.  通过 vgSrc 方式注册的监听器将覆盖默认的事件监听器，事件参数为：`$e{src:''}`，用法如：
  ```html
  <img vg-src="ctrl.currentImg" on-begin="ctrl.log(src)" alt="">
  ```

####    样式class
vgSrc 支持 loadingCls、loadedCls、errorCls、emptyCls 样式，可通过 vgSrcConfigProvider 、 vgSrc 两种方式注册 class 值：

1.  通过 vgSrcConfigProvider 方式注册的 class 将做为默认的 class ，用法如：
  ```javascript
  errorCls:'errorClass'
  ```

1.  通过 vgSrc 方式注册的 class 将做为此image特定的 class，用法如：
  ```html
  <img vg-src="ctrl.currentImg" error-cls="errorClass" alt="">
  ```
** 注意，class 属性不支持angular表达式 —— 你只能传递简单的字符串 **

####    配置项汇总
  ```javascript
  {
    //  启动调试模式
    debug: false,

    //  图片加载中的替换显示图片
    loading: '/loading.jpg',

    //  图片加载中的样式 class
    loadingCls: '',

    //  图片加载完成的样式 class
    loadedCls: '',

    //  图片加载失败的替换显示图片
    error: '/error.jpg',

    //  图片加载失败的样式 class
    errorCls: '',

    //  图片值为空时的替换显示图片
    empty: '',

    //  图片值为空时的样式 class
    emptyCls: '',

    //  资源开始加载事件
    'onBegin': ng.noop,

    //  资源加载出错事件
    'onError': ng.noop,

    //  资源加载完毕事件
    'onLoad': ng.noop
  }
  ```

##  兼容性
目前兼容主流浏览器及ie8
