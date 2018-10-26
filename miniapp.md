## 代码构成
## JSON配置
    app.json 是当前小程序的全局配置，包括了小程序的所有页面路径、界面表现、网络超时时间、底部 tab 等
        {
            "pages":[               //*定义小程序所有的路径
                "pages/index/index",
            ],         
            "window":{          // 定义小程序所有页面的顶部背景颜色，文字颜色定义等
                "navigationBarBackgroundColor": ''          //导航栏背景颜色，如 #000000
                "navigationBarTextStyle": ''            //导航栏标题颜色，仅支持 black / white
                "navigationBarTitleText": ''            //导航栏标题文字内容
                "navigationStyle"               //导航栏样式，仅支持以下值：default 默认样式,custom 自定义导航栏，只保留右上角胶囊按钮
                "backgroundColor": ''           //窗口的背景色
                "backgroundTextStyle": ''         //下拉 loading 的样式，仅支持 dark / light    
                "backgroundColorTop": ''            //顶部窗口的背景色，仅 iOS 支持
                "backgroundColorBottom": ''            //底部窗口的背景色，仅 iOS 支持
                "enablePullDownRefresh": ''         //是否全局开启下拉刷新
                "onReachBottomDistance": ''     //页面上拉触底事件触发时距页面底部距离，单位为px,默认50
            },
            "tabBar":{
                "color": ''    //*tabbar的文字颜色
                "selectedColor": ''         //*tabbar的文字被选中颜色
                "backgroundColor": ''       //*tab 的背景色
                "borderStyle": ''           //tabbar上边框的颜色， 仅支持 black / white
                "list":[                    //*
                    {
                        "pagePath": "pages/index/index",  //*
                        "text": "首页",                     //*
                        "iconPath": "",
                        "selectedIconPath": ""
                    }
                ]
                "position": ''              //tabBar的位置，仅支持 bottom / top
            },
            "networkTimeout": {             //所有值默认时间都是6000
                "request": '',              //wx.request 的超时时间，单位：毫秒。
                "connectSocket": '',        //wx.connectSocket 的超时时间，单位：毫秒
                "uploadFile": '',           //wx.uploadFile 的超时时间，单位：毫秒。
                "downloadFile": '',         //wx.downloadFile 的超时时间，单位：毫秒。
            },
            "debug": '',                    //是否开启 debug 模式，默认关闭
            "functionalPages": '',          //是否启用插件功能页，默认关闭
            "subpackages": '',              //分包结构配置Object Array
            "workers": ''                   //Worker 代码放置的目录
            "requiredBackgroundModes": ''   //需要在后台使用的能力，如「音乐播放」String Array
            "plugins":''                    //使用到的插件object
            "preloadRule": ''               //分包预下载规则object
            "resizable": ''                 //iPad 小程序是否支持屏幕旋转，默认关闭
            "navigateToMiniProgramAppIdList": ''        //需要跳转的小程序列表，详见 wx.navigateToMiniProgram String Array
        }
    注：客户端 6.7.2 版本开始，navigationStyle: custom 对 <web-view> 组件无效



    project.config.json
        小程序开发者工具在每个项目的根目录都会生成一个 project.config.json，你在工具上做的任何配置都会写入到这个文件，当你重新安装工具或者换电脑工作时，你只要载入同一个项目的代码包，开发者工具就自动会帮你恢复到当时你开发项目时的个性化配置，其中会包括编辑器的颜色、代码上传时自动压缩等等一系列选项
        {
            "miniprogramRoot": ''           //指定小程序源码的目录(需为相对路径)Path String
            "qcloudRoot": ''           //指定腾讯云项目的目录(需为相对路径)Path String
            "pluginRoot": ''           //指定插件项目的目录(需为相对路径)Path String
            "compileType": ''           //编译类型String
            "setting": ''           //项目设置object
            "libVersion": ''           //基础库版本String
            "appid": ''           //项目的 appid，只在新建项目时读取String
            "projectname": ''           //项目名字，只在新建项目时读取String
            "packOptions": ''           //打包配置选项object
            "debugOptions": ''           //调试配置选项object
            "scripts": ''           //自定义预处理object
        }
        compileType 有效值
            miniprogram         当前为普通小程序项目
            plugin              当前为小程序插件项目

        setting 中可以指定以下设置
            es6                 是否启用 es6 转 es5 Boolean
            postcss             上传代码时样式是否自动补全 Boolean
            minified            上传代码时是否自动压缩  Boolean
            urlCheck            是否检查安全域名和 TLS 版本 Boolean
            uglifyFileName      是否进行代码保护  Boolean

        scripts 中指定自定义预处理的命令
            beforeCompile       编译前预处理命令
            beforePreview       预览前预处理命令
            beforeUpload        上传前预处理命令
        
        packOptions 用以配置项目在打包过程中的选项。打包是预览、上传时对项目进行的必须步骤
            目前可以指定 packOptions.ignore 字段，用以配置打包时对符合指定规则的文件或文件夹进行忽略，以跳过打包的过程，这些文件或文件夹将不会出现在预览或上传的结果内。
            packOptions.ignore 为一对象数组，对象元素类型如下

            value               路径或取值string
            type                类型string

            type 可以取的值为 folder、file、suffix、prefix、regexp2、glob2，分别对应文件夹、文件、后缀、前缀、正则表达式、Glob 规则。所有规则值都会自动忽略大小写。
            注 1: value 字段的值若表示文件或文件夹路径，以小程序目录 (miniprogramRoot) 为根目录。
            注 2: regexp、glob 仅 1.02.1809260 及以上版本工具支持。 
            注: 更改可能需要重新打开项目才能生效。
            demo
            {
                "packOptions": {
                    "ignore": [{
                    "type": "file",
                    "value": "test/test.js"
                    }, {
                    "type": "folder",
                    "value": "test"
                    }, {
                    "type": "suffix",
                    "value": ".webp"
                    }, {
                    "type": "prefix",
                    "value": "test-"
                    }, {
                    "type": "glob",
                    "value": "test/**/*.js"
                    }, {
                    "type": "regexp",
                    "value": "\\.jsx$"
                    }]
                }
            }

        debugOptions 用以配置在对项目代码进行调试时的选项。
            目前可以指定 debugOptions.hidedInDevtools 字段，用以配置调试时于调试器 Sources 面板隐藏源代码的文件。
            hidedInDevtools 的配置规则和 packOptions.ignore 是一致的。
            当某个 js 文件符合此规则时，调试器 Sources 面板中此文件源代码正文内容将被隐藏，显示为：
                // xxx.js has been hided by project.config.json

        项目配置示例：         
            {
                "miniprogramRoot": "./src",
                "qcloudRoot": "./svr",
                "setting": {
                    "postcss": true,
                    "es6": true,
                    "minified": true,
                    "urlCheck": false
                },
                "packOptions": {
                    "ignore": []
                },
                "debugOptions": {}
            }


    
    page.json
        {
            "navigationBarBackgroundColor": '',         //导航栏背景颜色，如 #000000
            "navigationBarTextStyle": '',               //导航栏标题颜色，仅支持 black / white
            "navigationBarTitleText": '',               //导航栏标题文字内容
            "backgroundColor": '',                      //窗口的背景色
            "backgroundTextStyle": '',                  //下拉 loading 的样式，仅支持 dark / light
            "enablePullDownRefresh": '',                //是否全局开启下拉刷新。
            "onReachBottomDistance": '',                //页面上拉触底事件触发时距页面底部距离，单位为px。
            "disableScroll": '',                        //设置为 true 则页面整体不能上下滚动；只在页面配置中有效，无法在 app.json 中设置该项
        }

## js配置
    app.js
        App() 函数用来注册一个小程序。接受一个 Object 参数，其指定小程序的生命周期回调等
        App() 必须在 app.js 中调用，必须调用且只能调用一次。不然会出现无法预期的后果

        App({
            globalData：{}                        //全局数据
            onLaunch:function(Object){}               //小程序初始化完成时（全局只触发一次）
            onShow:function(){}               //小程序启动，或从后台进入前台显示时
            onHide:function(){}               //小程序从前台进入后台时
            onError:function(){}               //小程序发生脚本错误，或者 api 调用失败时触发，会带上错误信息
            onPageNotFound:function(){}        //小程序要打开的页面不存在时触发，会带上页面信息回调该函数
            其他                            //开发者可以添加任意的函数或数据到 Object 参数中，用 this 可以访问
        })

        onLaunch(Object)参数说明
            path            //打开小程序的路径String
            query            //打开小程序的query object
            scene            //打开小程序的场景值number
            shareTicket            //获取更多转发信息
            referrerInfo            //当场景为由从另一个小程序或公众号或App打开时，返回此字段Object
            referrerInfo.appId            //来源小程序或公众号或App的 appId，详见下方说明String
            referrerInfo.extraData            //打开小程序的路径String来源小程序传过来的数据，scene=1037或1038时支持object

        以下场景支持返回 referrerInfo.appId：
            场景值	            场景	                appId信息含义
            1020	公众号 profile 页相关小程序列表	    来源公众号 appId
            1035	公众号自定义菜单	                来源公众号 appId
            1036	App 分享消息卡片	                来源应用 appId
            1037	小程序打开小程序	                来源小程序 appId
            1038	从另一个小程序返回	                来源小程序 appId
            1043	公众号模板消息	                    来源公众号 appId

        onShow(Object)参数与onLaunch一致
        onHide()
        onError(String error)   小程序发生脚本错误，或者 api 调用失败时触发。
        onPageNotFound(Object)
            字段	类型	说明
            path	String	不存在页面的路径
            query	Object	打开不存在页面的 query
            isEntryPage	Boolean	是否本次启动的首个页面（例如从分享等入口进来，首个页面是开发者配置的分享页面）
        
            开发者可以在 onPageNotFound 回调中进行重定向处理，但必须在回调中同步处理，异步处理（例如 setTimeout 异步执行）无效。
            如果开发者没有添加 onPageNotFound 监听，当跳转页面不存在时，将推入微信客户端原生的页面不存在提示页面
            demo
                App({
                    onPageNotFound(res) {
                        wx.redirectTo({
                        url: 'pages/...'
                        }) // 如果是 tabbar 页面，请使用 wx.switchTab
                    }
                })



    getApp(Object)
        全局的 getApp() 函数可以用来获取到小程序 App 实例。
        Object 参数说明：
            字段	类型	说明
            allowDefault    Boolean       在 App 未定义时返回默认实现。当App被调用时，默认实现中定义的属性会被覆盖合并到App中。一般用于独立分包。

        demo
        var appInstance = getApp()
        不要在定义于 App() 内的函数中调用 getApp() ，使用 this 就可以拿到 app 实例。
        通过 getApp() 获取实例之后，不要私自调用生命周期函数。



    page.js
        Page(Object) 函数用来注册一个页面。接受一个 Object 类型参数，其指定页面的初始数据、生命周期回调、事件处理函数等。
        Object 参数说明：
        Page({
            data:{},
            //页面加载时触发。一个页面只会调用一次，可以在 onLoad 的参数中获取打开当前页面路径中的参数。
            onLoad(Object query){
                //query         打开当前页面路径中的参数
            }
            onShow(){},
            //页面初次渲染完成时触发。一个页面只会调用一次，代表页面已经准备妥当，可以和视图层进行交互。
            //注意：对界面内容进行设置的 API 如wx.setNavigationBarTitle，请在onReady之后进行
            onReady(){

            },
            onHide(){},
            onUnload(){},
            onPullDownRefresh(){
                //监听用户下拉刷新事件。
               // 需要在app.json的window选项中或页面配置中开启enablePullDownRefresh。
                //可以通过wx.startPullDownRefresh触发下拉刷新，调用后触发下拉刷新动画，效果与用户手动下拉刷新一致。
                //当处理完数据刷新后，wx.stopPullDownRefresh可以停止当前页面的下拉刷新。
            },
            onReachBottom(){
                //监听用户上拉触底事件
                //可以在app.json的window选项中或页面配置中设置触发距离onReachBottomDistance。
                //在触发距离内滑动期间，本事件只会被触发一次
            },
            onPageScroll(Object){
                //监听用户滑动页面事件。
                //Object 参数说明：
                //    scrollTop   页面在垂直方向已滚动的距离（单位px）number
            },
            onShareAppMessage(Object){
                //监听用户点击页面内转发按钮（<button> 组件 open-type="share"）或右上角菜单“转发”按钮的行为，并自定义转发内容。
                //只有定义了此事件处理函数，右上角菜单才会显示“转发”按钮
                //Object 参数说明：
                //  from        转发事件来源。button：页面内转发按钮；menu：右上角转发菜单
                //  target      如果 from 值是 button，则 target 是触发这次转发事件的 button，否则为 undefined
                //  webViewUrl  页面中包含<web-view>组件时，返回当前<web-view>的url

                //onShareAppMessage需要 return 一个 Object，用于自定义转发内容，返回内容如下：
                return {
                    title: '',          //转发标题,默认当前小程序名称
                    path: '',           //转发路径,默认当前页面 path ，必须是以 / 开头的完整路径
                    imageUrl: ''        //自定义图片路径，可以是本地文件路径、代码包文件路径或者网络图片路径，使用默认截图
                }
            }，
            onTabItemTap(Object){
                //点击 tab 时触发
                //Object 参数说明
                //  index   被点击tabItem的序号，从0开始
                //  pagePath    被点击tabItem的页面路径
                //  text	    被点击tabItem的按钮文字
            }
        })

        Page.route
            到当前页面的路径，类型为String。
            demo
            Page({
                onShow: function() {
                    console.log(this.route)
                }
            })

        Page.prototype.setData(Object data, Function callback)
            Object 以 key: value 的形式表示，将 this.data 中的 key 对应的值改变成 value。
            其中 key 可以以数据路径的形式给出，支持改变数组中的某一项或对象的某个属性，如 array[2].message，a.b.c.d，并且不需要在 this.data 中预先定义。

        页面栈
            特别注意    
                Tab 切换    页面全部出栈，只留下新的 Tab 页面
                重加载      页面全部出栈，只留下新的页面
            getCurrentPages() 函数用于获取当前页面栈的实例，以数组形式按栈的顺序给出，第一个元素为首页，最后一个元素为当前页面。

            不要在 App.onLaunch 的时候调用 getCurrentPages()，此时 page 还没有生成。

            navigateTo, redirectTo 只能打开非 tabBar 页面。
            switchTab 只能打开 tabBar 页面。
            reLaunch 可以打开任意页面。
            页面底部的 tabBar 由页面决定，即只要是定义为 tabBar 的页面，底部都有 tabBar。
            调用页面路由带的参数可以在目标页面的onLoad中获取。

            demo重加载
                重启动	调用 API wx.reLaunch 或使用组件 <navigator open-type="reLaunch"/>

## npm支持
    使用 npm 包
        1.在小程序中执行命令安装 npm 包：
            npm install --production
        2.点击开发者工具中的菜单栏：工具 --> 构建 npm
        3.勾选“使用 npm 模块”选项：(在右上角详情，和忽略https的位置一样)
        4.构建完成后即可使用 npm 包。
    
    js 中引入 npm 包：
        const package = require('packageName')

    使用 npm 包中的自定义组件：
        {
            "usingComponents": {
                "package": "packageName",
                "package-other": "packageName/other"
            }
        }

## 视图层 View
    框架的视图层由 WXML 与 WXSS 编写，由组件来进行展示。

    将逻辑层的数据反应成视图，同时将视图层的事件发送给逻辑层。

    WXML(WeiXin Markup language) 用于描述页面的结构。

    WXS(WeiXin Script) 是小程序的一套脚本语言，结合 WXML，可以构建出页面的结构。

    WXSS(WeiXin Style Sheet) 用于描述页面的样式。

    组件(Component)是视图的基本组成单元。

## 数据绑定
    <text>{{msg}}</text>
    <view id="item-{{id}}"> </view>
    <view hidden="{{flag ? true : false}}"> Hidden </view>
    <view>{{object.key}} {{array[0]}}</view>
    <view wx:for="{{[zero, 1, 2, 3, 4]}}"> {{item}} </view>     //最终组合成数组[0, 1, 2, 3, 4]。
    <template is="objectCombine" data="{{for: a, bar: b}}"></template>  //最终组合成的对象是 {for: 1, bar: 2}
    <template is="objectCombine" data="{{...obj1, ...obj2, e: 5}}"></template>  //也可以用扩展运算符 ... 来将一个对象展开
    <template is="objectCombine" data="{{foo, bar}}"></template>        //如果对象的 key 和 value 相同，也可以间接地表达
    <view wx:for="{{[1,2,3]}} ">{{item}}</view>         等价于下面
    <view wx:for="{{[1,2,3] + ' '}}">{{item}}</view>
    Page({
        data:{
            msg:'hello world',
            object: {
                key: 'Hello '
            },
            array: ['MINA'],
            zero: 0,
            a: 1,
            b: 2,
            foo: 'my-foo',
            bar: 'my-bar',
        }
    })
## 列表渲染
    <view wx:for="{{array}}"> {{item}} </view>
    Page({
        data: {
            array: [1, 2, 3, 4, 5]
        }
    })

    wx:key
        wx:key="unique"      //unique是唯一标识
        wx:key="*this"      //this指自己

    使用 wx:for-item 可以指定数组当前元素的变量名，
    使用 wx:for-index 可以指定数组当前下标的变量名：
    <view wx:for="{{array}}" wx:for-index="idx" wx:for-item="itemName">
        {{idx}}: {{itemName.message}}
    </view>

    <block wx:for="{{[1, 2, 3]}}">              渲染多层结构可以用block包裹
        <view> {{index}}: </view>
        <view> {{item}} </view>
    </block>

    当 wx:for 的值为字符串时，会将字符串解析成字符串数组
        <view wx:for="array">
            {{item}}
        </view>
        等同于
        <view wx:for="{{['a','r','r','a','y']}}">
            {{item}}
        </view
## 条件渲染
    <view wx:if="{{view == 'WEBVIEW'}}"> WEBVIEW </view>
    <view wx:elif="{{view == 'APP'}}"> APP </view>
    <view wx:else="{{view == 'MINA'}}"> MINA </view>
    Page({
        data: {
            view: 'MINA'
        }
    })

    wx:if vs hidden
        wx:if 是惰性的，当初始条件为false时，什么也不做
        hidden 就简单的多，组件始终会被渲染，只是简单的控制显示与隐藏
        如果需要频繁切换的情景下，用 hidden 更好，如果在运行时条件不大可能改变则 wx:if 较好
## 模板
    <template name="staffName">
    <view>
        FirstName: {{firstName}}, LastName: {{lastName}}
    </view>
    </template>

    <template is="staffName" data="{{...staffA}}"></template>
    <template is="staffName" data="{{...staffB}}"></template>
    <template is="staffName" data="{{...staffC}}"></template>
    Page({
        data: {
            staffA: {firstName: 'Hulk', lastName: 'Hu'},
            staffB: {firstName: 'Shang', lastName: 'You'},
            staffC: {firstName: 'Gideon', lastName: 'Lin'}
        }
    })

    <template name="odd">
        <view> odd </view>
    </template>

    <template name="even">
        <view> even </view>
    </template>

    <block wx:for="{{[1, 2, 3, 4, 5]}}">   is 属性可以使用 Mustache 语法，来动态决定具体需要渲染哪个模板：
        <template is="{{item % 2 == 0 ? 'even' : 'odd'}}"/>
    </block>

    模板的作用域
        模板拥有自己的作用域，只能使用 data 传入的数据以及模板定义文件中定义的 <wxs /> 模块。
## 事件
    冒泡事件
        touchstart
        touchmove
        touchcancel         手指触摸动作被打断，如来电提醒，弹窗
        touchend            手指触摸动作结束
        tap                 手指触摸后马上离开
        longpress           手指触摸后，超过350ms再离开，如果指定了事件回调函数并触发了这个事件，tap事件将不被触发
        transitionend       会在 WXSS transition 或 wx.createAnimation 动画结束后触发
        animationstart      会在一个 WXSS animation 动画开始时触发
        animationiteration  会在一个 WXSS animation 一次迭代结束时触发
        animationend        会在一个 WXSS animation 动画完成时触发
        touchforcechange     在支持 3D Touch 的 iPhone 设备，重按时会触发

        注：除上表之外的其他组件自定义事件如无特殊声明都是非冒泡事件，如<form/>的submit事件，<input/>的input事件，<scroll-view/>的scroll事件
    
    事件绑定写法
        bindtap="tap"     bindtouchstart="touchstart"          不阻止冒泡
        bind:tap
        catchtap    catchtouchstart         阻止冒泡
        catch:touchstart

    事件的捕获阶段
        捕获阶段位于冒泡阶段之前，且在捕获阶段中，事件到达节点的顺序与冒泡阶段恰好相反。需要在捕获阶段监听事件时，可以采用capture-bind、capture-catch关键字，后者将中断捕获阶段和取消冒泡阶段。

        在下面的代码中，点击 inner view 会先后调用handleTap2、handleTap4、handleTap3、handleTap1。
        <view id="outer" bind:touchstart="handleTap1" capture-bind:touchstart="handleTap2">
        outer view
        <view id="inner" bind:touchstart="handleTap3" capture-bind:touchstart="handleTap4">
            inner view
        </view>
        </view>

        如果将上面代码中的第一个capture-bind改为capture-catch，将只触发handleTap2。
        <view id="outer" bind:touchstart="handleTap1" capture-catch:touchstart="handleTap2">
        outer view
        <view id="inner" bind:touchstart="handleTap3" capture-bind:touchstart="handleTap4">
            inner view
        </view>
        </view>

    BaseEvent 基础事件对象属性列表：
        target              触发事件的组件的一些属性值集合
        currentTarget       当前组件的一些属性值集合

    TouchEvent 触摸事件对象属性列表（继承 BaseEvent）
        touches         触摸事件，当前停留在屏幕中的触摸点信息的数组
        changedTouches  触摸事件，当前变化的触摸点信息的数组

    CustomEvent 自定义事件对象属性列表（继承 BaseEvent）
        detail      object        额外的信息
        自定义事件所携带的数据，如表单组件的提交事件会携带用户的输入，媒体的错误事件会携带错误信息，详见组件定义中各个事件的定义。

点击事件的detail 带有的 x, y 同 pageX, pageY 代表距离文档左上角的距离。

    touches
        touches 是一个数组，每个元素为一个 Touch 对象（canvas 触摸事件中携带的 touches 是 CanvasTouch 数组）。 表示当前停留在屏幕上的触摸点。

    Touch 对象
        属性	        类型	说明
        identifier	    Number	触摸点的标识符
        pageX, pageY	Number	距离文档左上角的距离，文档的左上角为原点 ，横向为X轴，纵向为Y轴
        clientX, clientY	Number	距离页面可显示区域（屏幕除去导航条）左上角距离，横向为X轴，纵向为Y轴

    CanvasTouch 对象
        属性	        类型	说明
        identifier	    Number	触摸点的标识符
        x, y	Number	距离 Canvas 左上角的距离，Canvas 的左上角为原点 ，横向为X轴，纵向为Y轴
    
    changedTouches
        changedTouches 数据格式同 touches。 表示有变化的触摸点，如从无变有（touchstart），位置变化（touchmove），从有变无（touchend、touchcancel）。
        
        特殊事件： <canvas/> 中的触摸事件不可冒泡，所以没有 currentTarget
    
    target&currentTarget下面的主要属性
        dataset         事件源组件上由data-开头的自定义属性组成的集合

    dataset
         以data-开头，多个单词由连字符-链接，不能有大写(大写会自动转成小写)如data-element-type，最终在 event.currentTarget.dataset 中会将连字符转成驼峰elementType。

## 引用
    WXML 提供两种文件引用方式import和include。
    import 有作用域的概念，即只会 import 目标文件中定义的 template，而不会 import 目标文件 import 的 template。
        <!-- item.wxml -->
        <template name="item">
            <text>{{text}}</text>
        </template>

        在 index.wxml 中引用了 item.wxml，就可以使用item模板：
        <import src="item.wxml"/>
        <template is="item" data="{{text: 'forbar'}}"/>

    include 可以将目标文件除了 <template/> <wxs/> 外的整个代码引入，相当于是拷贝到 include 位置
        <!-- index.wxml -->
        <include src="header.wxml"/>
            <view> body </view>
        <include src="footer.wxml"/>

        <!-- header.wxml -->
        <view> header </view>

        <!-- footer.wxml -->
        <view> footer </view>