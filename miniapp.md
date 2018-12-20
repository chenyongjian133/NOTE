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


​    
​    page.json
​        {
​            "navigationBarBackgroundColor": '',         //导航栏背景颜色，如 #000000
​            "navigationBarTextStyle": '',               //导航栏标题颜色，仅支持 black / white
​            "navigationBarTitleText": '',               //导航栏标题文字内容
​            "backgroundColor": '',                      //窗口的背景色
​            "backgroundTextStyle": '',                  //下拉 loading 的样式，仅支持 dark / light
​            "enablePullDownRefresh": '',                //是否全局开启下拉刷新。
​            "onReachBottomDistance": '',                //页面上拉触底事件触发时距页面底部距离，单位为px。
​            "disableScroll": '',                        //设置为 true 则页面整体不能上下滚动；只在页面配置中有效，无法在 app.json 中设置该项
​        }

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

## WXSS
    微信规定：屏幕宽为750rpx
    rpx换算px
        屏幕宽度/750
            例如i6，i7屏幕宽度为375px
            即 1rpx = 0.5px
            只要拿i6做视觉稿
            以375宽度设计的，乘以2就可以兼容所有设备
    
    px换算rpx
        750/屏幕宽度
    
    样式导入
        @import 'xxx.wxss';
    
    style
        <view style="color:{{color}};">test</view>
    
    class
        <view class="abc {{myclass}}">text</view>

## WXS
    是小程序脚本语言
    注意
        wxs不依赖基础库版本，可以在任意小程序上运行
        wxs和js不一样，有自己的语法
        wxs和js代码是隔离的，只能调用js文件中的data，wxs中不能调用js文件中的函数，也不能调用微信的api
        wxs函数不能作为组件的事件回调
        在ios上运行速度比js快2-20倍，在安卓上差不多
    
    例：
        <!--wxml-->
        <wxs module="m1">
        var msg = "hello world";
        module.exports.message = msg;
        </wxs>
    
        <view>{{m1.message}}</view>
    
        页面效果
            hello world
    
    例：    
        Page({
            data:{
                array:[1,2,3,4,5,6,6,67,,8]
            }
        })
    
        <!--wxml-->
        <wxs module="m1">
        var getMax = function(array){
            var max = undefined;
            for(var i=0;i<array.length;i++){
                max = max === undefined?
                    array[i]:
                    (max >= array[i] ? max : array[i])
            }
            return max;
        }
        module.exports.getMax = getMax;
        </wxs>
    
        <view>{{m1.getMax(array)}}</view>
        页面输出
            67

## wxs语法
    wxs代码可以写在wxml文件内以<wxs>标签方式展示。或以.wxs为后缀的文件内
    
    模块
        每一个 .wxs 文件和 <wxs> 标签都是一个单独的模块。
        每个模块都有自己独立的作用域。即在一个模块里面定义的变量与函数，默认为私有的，对其他模块不可见。
        一个模块要想对外暴露其内部的私有变量与函数，只能通过 module.exports 实现。
    
    module 对象
        每个 wxs 模块均有一个内置的 module 对象。
    
        pages/tools.wxs
    
        var foo = 'hello'
        var bar = function(d){
            return d
        }
        module.exports={
            FOO:foo,
            bar:bar
        }
        module.exports.msg = 'world'
    
        引用该wxs文件
        index.wxml
    
        <wxs src="./../tools.wxs" module='tools' />
        <view>{{tools.msg}}</view>
        <view>{{tools.bar(tools.FOO)}}</view>
    
        页面输出
            world
            helloworld
    
    require函数
        在.wxs模块中引用其他 wxs 文件模块，可以使用 require 函数。
        注意
            只能引用 .wxs 文件模块，且必须使用相对路径。
            wxs 模块均为单例，wxs 模块在第一次被引用时，会自动初始化为单例对象。多个页面，多个地方，多次引用，使用的都是同一个 wxs 模块对象。
            如果一个 wxs 模块在定义之后，一直没有被引用，则该模块不会被解析与运行。
    
        pages/logic.wxs
        var tools = require('./tools.wxs')
        console.log(tools.FOO)
        console.log(tools.bar('logic.wxs'))
    
        index.wxml引用logic.wxs
        <wxs src='./../logic.wxs' module='logic' />
    
    作用域
        <wxs> 模块只能在定义模块的 WXML 文件中被访问到。使用 <include> 或 <import> 时，<wxs> 模块不会被引入到对应的 WXML 文件中。
        <template> 标签中，只能使用定义该 <template> 的 WXML 文件中定义的 <wxs> 模块
    
    wxs的变量命名
        和js一致
    
    wxs的注释：和js一致
    
    运算符
        基本运算符
            +，-，*，/，%       加减乘除模
        一元运算符
            ++，--      自增自减
            +，-        正负运算
            ~           否运算
            ！          取反
            delete      删除对象属性    true === delete a.fake
            void        undefined === void a
            typeof      'number' === typeof a
        位运算
            <<              左移
            >>              无符号右移
            >>>             带符号右移
            &,|,^           与或异或
        比较运算
            < ,>,<=,>=,==,===
        赋值运算
            =，+=，-=，*=，/=，%=
            <<=,>>=,>>>=,&=,|=,^=
        逻辑运算
            &&,||
        三目运算
            条件?true:false
        逗号运算
            var a=10,b=20
            console.log(20===(a,b))         //true
    
    语句
        if，for，while，switch，do while等语法和js一致，支持break，continue
    
    数据类型
        number  数值(包含整数和小数)
        string  字符串
        boolean 布尔
        object  对象
        function    函数
        array   数组
        date    日期
        regexp  正则
    
        number：
            属性constructor：返回字符串“Number”
            方法：
                toString
                toLocaleString
                valueOf
                toFixed
                toExponential
                toPrecision
    
        number：
            属性constructor：返回字符串“String”
                length：       返回长度
            方法：
                toString
                valueOf
                charAt
                charCodeAt
                concat
                indexOf
                lastIndexOf
                localeCompare
                match
                replace
                search
                slice
                split
                substring
                toLowerCase
                toLocaleLowerCase
                toUpperCase
                toLocaleUpperCase
                trim
    
        number：
            属性constructor：返回字符串“Boolean”
            方法：
                toString
                valueOf
    
        object：
            属性constructor：返回字符串“Object”
            方法：
                toString        返回字符串 "[object Object]"
        
        function：
            属性constructor：返回字符串“Function”
                length：     返回形参个数
            方法：
                toString
            
        array
            属性constructor：返回字符串“Array”
                length：     
            方法：
                toString
                concat
                join
                pop
                push
                reverse
                shift
                slice
                sort
                splice
                unshift
                indexOf
                lastIndexOf
                every
                some
                forEach
                map
                filter
                reduce
                reduceRight
    
        date
            属性constructor：返回字符串“Date”
            var date = getDate()    返回当前时间对象
            date = getDate(1500000000000);
            // Fri Jul 14 2017 10:40:00 GMT+0800 (中国标准时间)
            date = getDate('2017-7-14');
            // Fri Jul 14 2017 00:00:00 GMT+0800 (中国标准时间)
            date = getDate(2017, 6, 14, 10, 40, 0, 0);
            // Fri Jul 14 2017 10:40:00 GMT+0800 (中国标准时间)
            方法
                toString
                toDateString
                toTimeString
                toLocaleString
                toLocaleDateString
                toLocaleTimeString
                valueOf
                getTime
                getFullYear
                getUTCFullYear
                getMonth
                getUTCMonth
                getDate
                getUTCDate
                getDay
                getUTCDay
                getHours
                getUTCHours
                getMinutes
                getUTCMinutes
                getSeconds
                getUTCSeconds
                getMilliseconds
                getUTCMilliseconds
                getTimezoneOffset
                setTime
                setMilliseconds
                setUTCMilliseconds
                setSeconds
                setUTCSeconds
                setMinutes
                setUTCMinutes
                setHours
                setUTCHours
                setDate
                setUTCDate
                setMonth
                setUTCMonth
                setFullYear
                setUTCFullYear
                toUTCString
                toISOString
                toJSON
        
        regexp  
            属性constructor：返回字符串“RegExp”
                source
                global
                ignoreCase
                mutiline
                lastIndex
            getRegExp(pattern[, flags]) 生成 regexp 对象需要使用 getRegExp函数。
                var a = getRegExp("x", "img");
                console.log("x" === a.source);
                console.log(true === a.global);
                console.log(true === a.ignoreCase);
                console.log(true === a.multiline);
            方法
                exec
                test
                toString
    
    基础类库(内置对象)
        Math
            属性
                E
                LN10
                LN2
                LOG2E
                LOG10E
                PI
                SQRT1_2
                SQRT2
            方法
                abs
                acos
                asin
                atan
                atan2
                ceil
                cos
                exp
                floor
                log
                max
                min
                pow
                random
                round
                sin
                sqrt
                tan
        
        JSON
            stringify(object): 将 object 对象转换为 JSON 字符串，并返回该字符串。
            parse(string): 将 JSON 字符串转化成对象，并返回该对象。
    
        Number
            属性
            MAX_VALUE
            MIN_VALUE
            NEGATIVE_INFINITY
            POSITIVE_INFINITY
        
        Date
            属性
            parse
            UTC
            now
    
        Global
            属性
            NaN
            Infinity
            undefined
            方法
                parseInt
                parseFloat
                isNaN
                isFinite
                decodeURI
                decodeURIComponent
                encodeURI
                encodeURIComponent

## wxml节点信息
    const query = wx.createSelectorQuery()
    query.select("#id").boundingClientReact(function(res){
        res.top             //id节点的上边界坐标(相对显示区域)
    })
    query.selectViewport().scrollOffset(function(res){
        res.scrollTop       //  显示区域的垂直滚动位置
    })
    query.exec()
    
    在自定义组件中，推荐使用 this.createSelectorQuery 来代替 wx.createSelectorQuery ，这样会将选择器选取范围定在这个自定义组件内

## WXML节点布局相交状态
<ul>
    <li>参照节点：监听的参照节点，取它的布局区域作为参照区域。如果有多个参照节点，则会取它们布局区域的 交集 作为参照区域。页面显示区域也可作为参照区域之一。</li>
    <li>目标节点：监听的目标，默认只能是一个节点（使用 selectAll 选项时，可以同时监听多个节点）。</li>
    <li>相交区域：目标节点的布局区域与参照区域的相交区域。</li>
    <li>相交比例：相交区域占参照区域的比例</li>
    <li>阈值：相交比例如果达到阈值，则会触发监听器的回调函数。阈值可以有多个。</li>
</ul>

## 响应显示区域变化
    在ipad上旋转屏幕，需要在app.json中配置“resizable”:true
    
    Media Query
        .my-class{
            width:40px
        }
        @media (min-width:480px){
             /* 仅在 480px 或更宽的屏幕上生效的样式规则 */
            .my-class{
                width:200px
            }
        }
    
    监视屏幕尺寸变化
        wx.onWindowResize(function(res){
            res.size.windowWidth        //新的显示区域宽度
            res.size.windowHeight       // 新的显示区域高度
        })

## 自定义组件
    组件定义
        包含json，wxml，js，wxss的一个文件夹
        在json中设置component字段为true
            {
                "component": true
            }
        在js中用Component函数注册组件
    
            Component({
                //父组件传入的属性
                properties:{
                    myProperty:{
                        type: String,   //*必填，目前接受的类型包括：String, Number, Boolean, Object, Array, null（表示任意类型）
                        value: '',
                        observer: function(newV,oldV,changedPath){
                            //传入的属性被改变时，自动触发，这里可以调用methods里面的方法
                        }
                    },
                    myProperty2: String // 简化的定义方式
                },
                //自身属性
                data:{
    
                },
                lifetimes:{
                    //生命周期函数,也可以直接定义在和lifetimes同级，但是会被lifetimes有同名的覆盖
                    created(){
    
                    },
                    moved(){}
                },
                attached(){
    
                },
                ready:function(){
    
                },
                moved:function(){}          //会被lifetimes里面的moved覆盖
                pageLifetimes:{
                    show:function(){},      // 组件所在页面的生命周期函数
                    hide(){}
                }
                //自身方法
                methods:{
                    myMethod:function(){
                        this.setData({})
                    }
                    //内部方法建议以下划线开头
                    _myInnerMethod:function(){
                        this.setData({
                            'A[0].B': 'myPrivateData'
                        })
                    }
                }
            })
    
            在 properties 定义段中，属性名采用驼峰写法（propertyName）；在 wxml 中，指定属性值时则对应使用连字符写法（component-tag-name property-name="attr value"），应用于数据绑定时采用驼峰写法（attr="{{propertyName}}"）
    
    组件使用
        在app.json中声明 usingComponents 字段，这个组件会成为全局组件，在小程序内的页面或自定义组件中可以直接使用而无需再声明
    
        页面中使用：json文件声明usingComponents字段
            {
                "usingComponents": {
                    "component-tag-name": "path/to/the/custom/component"
                }
            }
    
    组件模板
        在组件模板中可以提供<slot>节点，用于继承父组件引用时提供的子节点
        demo
            //组件模板
            <view class='wrapper'>
                <view>组件内部节点</view>
                <slot></slot>
            </view>
            //使用组件
            <view>
                <component-tag-name>
                    <view>这个view会插到组件内部slot的位置</view>
                </component-tag-name>
            </view>
    
    抽象节点
        自定义组件模板中的一些节点，其对应使用的自定义组件不是由自定义组件模板决定的，而是由组件使用者决定，这时可以把这个不确定的节点定义为抽象节点
        例：
            //组件模板selectable-group
            <view wx:for='{{labels}}'>
                <label>
                    <selectable disabled='{{false}}'></selectable>
                    {{item}}
                </label>
            </view>
            其中selectable不是在json中声明使用的组件，而是一个抽象节点，需要在json中声明componentGenerics字段
            {
                 "componentGenerics": {
                    "selectable": true
                }
            }
    
            //使用包含抽象节点的组件:在使用 selectable-group 组件时，必须指定“selectable”具体是哪个组件：
            <view>
                <selectable-group generic:selectable='custom-radio' />
                <selectable-group generic:selectable="custom-checkbox" />
            </view>
            其中custom-radio是在此使用者json文件usingComponents中声明的组件
            {
                "usingComponents": {
                    "custom-radio": "path/to/custom/radio",
                    "custom-checkbox": "path/to/custom/checkbox"
                }
            }
    
    抽象节点的默认组件
        抽象节点可以指定一个默认组件，当具体组件未被指定时，将创建默认组件的实例。默认组件可以在 componentGenerics 字段中指定：
        {
            "componentGenerics": {
                "selectable": {
                "default": "path/to/default/component"
                }
            }
        }
        节点的 generic 引用 generic:xxx="yyy" 中，值 yyy 只能是静态值，不能包含数据绑定。因而抽象节点特性并不适用于动态决定节点名的场景
    
    Component构造器
        定义段	    类型	    是否必填	描述
        properties	Object Map	否	      组件的对外属性，是属性名到属性设置的映射表，包含三个字段，type 属性类型、 value 属性初始值、 observer 属性值被更改时的响应函数
        data	    Object	    否	       组件的内部数据，和 properties 一同用于组件的模板渲染
        methods	    Object	    否      	组件的方法
        behaviors	String Array	否	    类似于mixins和traits的组件间代码复用机制
        created	    Function	否	        组件生命周期函数，在组件实例进入页面节点树时执行，注意此时不能调用 setData
        attached	Function	否	        组件生命周期函数，在组件实例进入页面节点树时执行
        ready	    Function	否	        组件生命周期函数，在组件布局完成后执行，此时可以获取节点信息（使用 SelectorQuery ）
        moved	    Function	否	        组件生命周期函数，在组件实例被移动到节点树另一个位置时执行
        detached	Function	否	        组件生命周期函数，在组件实例被从页面节点树移除时执行
        relations	Object	    否      	组件间关系定义
        externalClasses	String Array	否	组件接受的外部样式类
        options	Object Map	    否	    一些选项
        lifetimes	Object	    否	    组件生命周期声明对象，组件的生命周期：created、attached、ready、moved、detached将收归到lifetimes字段内进行声明，原有声明方式仍旧有效，如同时存在两种声明方式，则lifetimes字段内声明方式优先级最高
        pageLifetimes	Object	否	    组件所在页面的生命周期声明对象(父组件)，目前仅支持页面的show和hide两个生命周期
        definitionFilter	Function	否	定义段过滤器，用于自定义组件扩展
    
    组件实例可以在组件的方法、生命周期函数和属性 observer 中通过 this 访问。组件包含一些通用属性和方法
        属性名	类型	描述
        is	String	组件的文件路径
        id	String	节点id
        dataset	String	节点dataset
        data	Object	组件数据，包括内部数据和属性值
        properties	Object	组件数据，包括内部数据和属性值（与 data 一致）
    
        方法名	参数	            描述
        setData	Object newData	    设置data并执行视图层渲染
        hasBehavior	Object behavior	检查组件是否具有 behavior （检查时会递归检查被直接或间接引入的所有behavior）
        triggerEvent	String name, Object detail, Object options	触发事件，参见 组件事件
        createSelectorQuery		创建一个 SelectorQuery 对象，选择器选取范围为这个组件实例内
        createIntersectionObserver		创建一个 IntersectionObserver 对象，选择器选取范围为这个组件实例内
        selectComponent	String selector	使用选择器选择组件实例节点，返回匹配到的第一个组件实例对象（会被 wx://component-export 影响）
        selectAllComponents	String selector	使用选择器选择组件实例节点，返回匹配到的全部组件实例对象组成的数组
        getRelationNodes	String relationKey	获取这个关系所对应的所有关联节点，参见 组件间关系
    
    使用 Component 构造器构造页面
        小程序普通页面也可以认为是组件，所以也可以使用Component构造器,但是必须在json中声明这两个字段
        {
            "usingComponents": {}，
        }
        组件的属性可以用于接收页面的参数，如访问页面 /pages/index/index?paramA=123&paramB=xyz ，如果声明有属性 paramA 或 paramB ，则它们会被赋值为 123 或 xyz 。
        Component({
            properties: {
                paramA: Number,
                paramB: String,
            },
            methods: {
                onLoad: function() {
                this.data.paramA // 页面参数 paramA 的值
                this.data.paramB // 页面参数 paramB 的值
                }
            }
        })
    
        在一个组件的定义和使用时，组件的属性名和 data 字段相互间都不能冲突（尽管它们位于不同的定义段中）。
        从基础库 2.0.9 开始，对象类型的属性和 data 字段中可以包含函数类型的子字段，即可以通过对象类型的属性字段来传递函数。低于这一版本的基础库不支持这一特性。
        bug : 对于 type 为 Object 或 Array 的属性，如果通过该组件自身的 this.setData 来改变属性值的一个子字段，则依旧会触发属性 observer ，且 observer 接收到的 newVal 是变化的那个子字段的值， oldVal 为空， changedPath 包含子字段的字段名相关信息。

## 组件间通信与事件
    WXML 数据绑定：用于父组件向子组件的指定属性设置数据，仅能设置 JSON 兼容数据（自基础库版本 2.0.9 开始，还可以在数据中包含函数
    
    事件：用于子组件向父组件传递数据，可以传递任意数据。
    
    父组件还可以通过 this.selectComponent 方法获取子组件实例对象，这样就可以直接访问组件的任意数据和方法。
    
    监听事件
        自定义组件可以触发任意的事件，引用组件的页面可以监听这些事件。
        <!-- 当自定义组件触发“myevent”事件时，调用“onMyEvent”方法 -->
        <component-tag-name bindmyevent="onMyEvent" />
        <!-- 或者可以写成 -->
        <component-tag-name bind:myevent="onMyEvent" />
        //父组件定义方法
        Page({
            onMyEvent: function(e){
                e.detail // 自定义组件触发事件时提供的detail对象
            }
        })
    
    触发事件
        自定义组件触发事件时，需要使用 triggerEvent 方法，指定事件名、detail对象和事件选项：
        <!-- 自定义button组件 -->
        <button bindtap="onTap">点击这个按钮将触发“myevent”事件</button> 
        Component({
            properties:{},
            methods:{
                onTap:function(){
                    var myEventDetail = {}      // detail对象，提供给事件监听函数
                    var myEventOption = {}      // 触发事件的选项
                    this.triggerEvent('myevent',myEventDetail,myEventOption)
                }
            }
        })
        
    触发事件的选项包括：
        选项名	类型	是否必填	默认值	描述
        bubbles	Boolean	否	false	事件是否冒泡
        composed	Boolean	否	false	事件是否可以穿越组件边界，为false时，事件将只能在引用组件的节点树上触发，不进入其他任何组件内部
        capturePhase	Boolean	否	false	事件是否拥有捕获阶段
    
        // 页面 page.wxml
        <another-component bindcustomevent="pageEventListener1">
            <my-component bindcustomevent="pageEventListener2"></my-component>
        </another-component>
        // 组件 another-component.wxml
        <view bindcustomevent="anotherEventListener">
            <slot />
        </view>
        // 组件 my-component.wxml
        <view bindcustomevent="myEventListener">
            <slot />
        </view>
        // 组件 my-component.js
        Component({
            methods: {
                onTap: function(){
                this.triggerEvent('customevent', {}) // 只会触发 pageEventListener2
                this.triggerEvent('customevent', {}, { bubbles: true }) // 会依次触发 pageEventListener2 、 pageEventListener1
                this.triggerEvent('customevent', {}, { bubbles: true, composed: true }) // 会依次触发 pageEventListener2 、 anotherEventListener 、 pageEventListener1
                }
            }
        })

## behaviors
    behaviors 是用于组件间代码共享的特性，类似于一些编程语言中的“mixins”或“traits”。
        behavior 可以包含一组属性、数据、生命周期函数和方法，组件引用它时，它的属性、数据和方法会被合并到组件中，生命周期函数也会在对应时机被调用。每个组件可以引用多个 behavior 。 behavior 也可以引用其他 behavior 。
        behavior 需要使用 Behavior() 构造器定义。
        例：
            //my-behavior.js
            modules.exports=Behavior({
                behaviors: [],
                properties: {
                    myBehaviorProperty: String
                },
                data:{
                    myBehaviorData:{}
                },
                attached:function(){
    
                },
                methods:{
                    myBehaviorMethod:function(){}
                }
            })
        组件引用时，在 behaviors 定义段中将它们逐个列出即可。
        
        例：
            // my-component.js
            var myBehavior = require('my-behavior')
                Component({
                behaviors: [myBehavior],
                properties: {
                    myProperty: {
                    type: String
                    }
                },
                data: {
                    myData: {}
                },
                attached: function(){},
                methods: {
                    myMethod: function(){}
                }
            })
        注意
            当组件触发 attached 生命周期时，会依次触发 my-behavior 中的 attached 生命周期函数和 my-component 中的 attached 生命周期函数。
    
    字段的覆盖和组合规则
        组件和它引用的 behavior 中可以包含同名的字段，对这些字段的处理方法如下：
    
        如果有同名的属性或方法，组件本身的属性或方法会覆盖 behavior 中的属性或方法，如果引用了多个 behavior ，在定义段中靠后 behavior 中的属性或方法会覆盖靠前的属性或方法；
        
        如果有同名的数据字段，如果数据是对象类型，会进行对象合并，如果是非对象类型则会进行相互覆盖；
        生命周期函数不会相互覆盖，而是在对应触发时机被逐个调用。如果同一个 behavior 被一个组件多次引用，它定义的生命周期函数只会被执行一次。

## 组件间关系
    有时需要实现这样的组件：
    <custom-ul>
        <custom-li> item 1 </custom-li>
        <custom-li> item 2 </custom-li>
    </custom-ul>
    custom-ul 和 custom-li 都是自定义组件，它们有相互间的关系，相互间的通信往往比较复杂。此时在组件定义时加入 relations 定义段，可以解决这样的问题。
    //custom-ul.js
    Component({
        relations:{
            './custom-li'"{
                type: 'child',              // 关联的目标节点应为子节点
                linked:function(target){}   // 每次有custom-li被插入时执行，target是该节点实例对象，触发在该节点attached生命周期之后
                linkChanged:function(target){}  // 每次有custom-li被移动后执行，target是该节点实例对象，触发在该节点moved生命周期之后
                unlinked:function(target){} // 每次有custom-li被移除时执行，target是该节点实例对象，触发在该节点detached生命周期之后
            }
        },
        methods:{
            _getAllLi:function(){
                // 使用getRelationNodes可以获得nodes数组，包含所有已关联的custom-li，且是有序的
                var nodes = this.getRelationNodes('custom-li')
            }
        },
        ready:funtion(){
            this._getAllLi()
        }
    })
    //custom-li.js
    Component({
        relations:{
            './custom-ul': {
                type: 'parent',         // 关联的目标节点应为父节点
                linked(target){}        // 每次被插入到custom-ul时执行，target是custom-ul节点实例对象，触发在attached生命周期之后
                linkChanged(target){}   // 每次被移动后执行，target是custom-ul节点实例对象，触发在moved生命周期之后
                unlinked(target){}      // 每次被移除时执行，target是custom-ul节点实例对象，触发在detached生命周期之后
            }
        }
    })
    注意：必须在两个组件定义中都加入relations定义，否则不会生效。
    
    关联一类组件
        有时，需要关联的是一类组件，如：
            <custom-form>
                <view>
                    input
                    <custom-input></custom-input>
                </view>
                <custom-submit> submit </custom-submit>
            </custom-form>
    
        custom-form 组件想要关联 custom-input 和 custom-submit 两个组件。此时，如果这两个组件都有同一个behavior：
            // path/to/custom-form-controls.js
            module.exports = Behavior({
                // ...
            })
    
            // path/to/custom-input.js
            var customFormControls = require('./custom-form-controls')
                Component({
                behaviors: [customFormControls],
                relations: {
                    './custom-form': {
                    type: 'ancestor', // 关联的目标节点应为祖先节点
                    }
                }
            })
    
            // path/to/custom-submit.js
            var customFormControls = require('./custom-form-controls')
            Component({
                behaviors: [customFormControls],
                relations: {
                    './custom-form': {
                    type: 'ancestor', // 关联的目标节点应为祖先节点
                    }
                }
            })
            则在 relations 关系定义中，可使用这个behavior来代替组件路径作为关联的目标节点
            // path/to/custom-form.js
            var customFormControls = require('./custom-form-controls')
                Component({
                relations: {
                    'customFormControls': {
                    type: 'descendant', // 关联的目标节点应为子孙节点
                    target: customFormControls
                    }
                }
            })
    
        relations 定义段
            选项	类型	是否必填	描述
            type	String	是	        目标组件的相对关系，可选的值为 parent 、 child 、 ancestor 、 descendant
            linked	Function	否	关系生命周期函数，当关系被建立在页面节点树中时触发，触发时机在组件attached生命周期之后
            linkChanged	Function	否	关系生命周期函数，当关系在页面节点树中发生改变时触发，触发时机在组件moved生命周期之后
            unlinked	Function	否	关系生命周期函数，当关系脱离页面节点树时触发，触发时机在组件detached生命周期之后
            target	String	否	如果这一项被设置，则它表示关联的目标节点所应具有的behavior，所有拥有这一behavior的组件节点都会被关联

## 基础能力
    1. 服务器域名配置
        每个微信小程序需要事先设置一个通讯域名，小程序只可以跟指定的域名与进行网络通信。包括普通 HTTPS 请求（request）、上传文件（uploadFile）、下载文件（downloadFile) 和 WebSocket 通信（connectSocket）
    
        域名只支持 https (request、uploadFile、downloadFile) 和 wss (connectSocket) 协议；
        域名不能使用 IP 地址或 localhost；
        域名必须经过 ICP 备案；
        出于安全考虑，api.weixin.qq.com 不能被配置为服务器域名，相关API也不能在小程序内调用。 开发者应将 appsecret 保存到后台服务器中，通过服务器使用 appsecret 获取 accesstoken，并调用相关 API；
        对于每个接口，分别可以配置最多 20 个域名。
    
    2. 存储
        每个微信小程序都可以有自己的本地缓存，可以通过 wx.setStorage/wx.setStorageSync、wx.getStorage/wx.getStorageSync、wx.clearStorage/wx.clearStorageSync，wx.removeStorage/wx.removeStorageSync 对本地缓存进行读写和清理。
    
        同一个微信用户，同一个小程序 storage 上限为 10MB。storage 以用户维度隔离，同一台设备上，A 用户无法读取到 B 用户的数据。
    
        注意： 如果用户储存空间不足，我们会清空最近最久未使用的小程序的本地缓存。我们不建议将关键信息全部存在 storage，以防储存空间不足或用户换设备的情况。
    
    3. 文件系统
        文件主要分为两大类：
            代码包文件：代码包文件指的是在项目目录中添加的文件。
            本地文件：通过调用接口本地产生，或通过网络下载下来，存储到本地的文件。
        
        其中本地文件又分为三种：
            本地临时文件：临时产生，随时会被回收的文件。不限制存储大小。
            本地缓存文件：小程序通过接口把本地临时文件缓存后产生的文件，不能自定义目录和文件名。除非用户主动删除小程序，否则不会被删除。跟本地用户文件共计，普通小程序最多可存储 10MB，游戏类目的小程序最多可存储 50MB。
            本地用户文件：小程序通过接口把本地临时文件缓存后产生的文件，允许自定义目录和文件名。除非用户主动删除小程序，否则不会被删除。跟本地用户文件共计，普通小程序最多可存储 10MB，游戏类目的小程序最多可存储 50MB。
        
        本地临时文件
            本地临时文件只能通过调用特定接口产生，不能直接写入内容。本地临时文件产生后，仅在当前生命周期内有效，重启之后即不可用。因此，不可把本地临时文件路径存储起来下次使用。如果需要下次在使用，可通过 FileSystemManager.saveFile() 或 FileSystemManager.copyFile() 接口把本地临时文件转换成本地缓存文件或本地用户文件。
            wx.chooseImage({
                success: function (res) {
                    var tempFilePaths = res.tempFilePaths // tempFilePaths 的每一项是一个本地临时文件路径
                }
            })
        
        本地缓存文件
            本地缓存文件只能通过调用特定接口产生，不能直接写入内容。本地缓存文件产生后，重启之后仍可用。本地缓存文件只能通过 FileSystemManager.saveFile() 接口将本地临时文件保存获得。
            fs.saveFile({
                tempFilePath: '', // 传入一个本地临时文件路径
                success(res) {
                    console.log(res.savedFilePath) // res.savedFilePath 为一个本地缓存文件路径
                }
            })
        
        本地用户文件
            本地用户文件是从 1.7.0 版本开始新增的概念。我们提供了一个用户文件目录给开发者，开发者对这个目录有完全自由的读写权限。通过 wx.env.USER_DATA_PATH 可以获取到这个目录的路径。
            // 在本地用户文件目录下创建一个文件 hello.txt，写入内容 "hello, world"
            const fs = wx.getFileSystemManager()
            fs.writeFileSync(`${wx.env.USER_DATA_PATH}/hello.txt`, 'hello, world', 'utf8')

## Canvas 画布
    所有在 <canvas/> 中的画图必须用 JavaScript 完成：
    demo：
        //wxml
        <canvas canvas-id="myCanvas" style="border: 1px solid;"/>
        //JS
        Page({
            onLoad(){
                const ctx = wx.createCanvasContext('myCanvas')      //创建canvas绘图上下文对象CanvasContext
                ctx.setFillStyle('red')     //填充红色
                ctx.fillRect(10,10,150,75)  //画矩形fillRect(x, y, width, height)
                ctx.draw()                  //开画
            }
        })
    
    坐标系
        canvas 是在一个二维的网格当中。左上角的坐标为(0, 0)。
    
    渐变
        渐变能用于填充一个矩形，圆，线，文字等。填充色可以不固定位固定的一种颜色。
        两种颜色渐变的方式：
            createLinearGradient(x, y, x1, y1) 创建一个线性的渐变
            createCircularGradient(x, y, r) 创建一个从圆心开始的渐变
        一旦我们创建了一个渐变对象，我们必须添加两个颜色渐变点。
            addColorStop(position, color) 方法用于指定颜色渐变点的位置和颜色，位置必须位于0到1之间。
            可以用setFillStyle 和 setStrokeStyle 方法设置渐变，然后进行画图描述。
        demo：
            const ctx = wx.createCanvasContext('myCanvas')
            // Create linear gradient
            const grd = ctx.createLinearGradient(0, 0, 200, 0)
            grd.addColorStop(0, 'red')
            grd.addColorStop(1, 'white')
            // Fill with gradient用渐变色填充
            ctx.setFillStyle(grd)
            ctx.fillRect(10, 10, 150, 80)
            ctx.draw()
    
            const ctx = wx.createCanvasContext('myCanvas')
            // Create circular gradient
            const grd = ctx.createCircularGradient(75, 50, 50)
            grd.addColorStop(0, 'red')
            grd.addColorStop(1, 'white')
            // Fill with gradient
            ctx.setFillStyle(grd)
            ctx.fillRect(10, 10, 150, 80)
            ctx.draw()

## 分包加载
    所谓的主包，即放置默认启动页面/TabBar 页面，以及一些所有分包都需用到公共资源/JS 脚本；而分包则是根据开发者的配置进行划分。
    
    目前小程序分包大小有以下限制：
        整个小程序所有分包大小不超过 8M
        单个分包/主包大小不能超过 2M
    
    配置分包
        例：目录
            ├── app.js
            ├── app.json
            ├── app.wxss
            ├── packageA
            │   └── pages
            │       ├── cat
            │       └── dog
            ├── packageB
            │   └── pages
            │       ├── apple
            │       └── banana
            ├── pages
            │   ├── index
            │   └── logs
            └── utils
        
            在 app.json subpackages 字段声明项目分包结构：
            {
                "pages":[
                    "pages/index",
                    "pages/logs"
                ],
                "subpackages": [
                    {
                    "root": "packageA",
                    "pages": [
                        "pages/cat",
                        "pages/dog"
                    ]
                    }, {
                    "root": "packageB",
                    "name": "pack2",
                    "pages": [
                        "pages/apple",
                        "pages/banana"
                    ]
                    }
                ]
            }
    
        subpackages字段说明
            字段	类型	说明
            root	String	分包根目录
            name	String	分包别名，分包预下载时可以使用
            pages	StringArray	分包页面路径，相对与分包根目录
            independent	Boolean	分包是否是独立分包
    
    打包原则
        声明 subpackages 后，将按 subpackages 配置路径进行打包，subpackages 配置路径外的目录将被打包到 app（主包） 中
        app（主包）也可以有自己的 pages（即最外层的 pages 字段）
        subpackage 的根目录不能是另外一个 subpackage 内的子目录
        tabBar 页面必须在 app（主包）内
    
    引用原则
        packageA 无法 require packageB JS 文件，但可以 require app、自己 package 内的 JS 文件
        packageA 无法 import packageB 的 template，但可以 require app、自己 package 内的 template
        packageA 无法使用 packageB 的资源，但可以使用 app、自己 package 内的资源

## 独立分包
    独立分包是小程序中一种特殊类型的分包，可以独立于主包和其他分包运行。从独立分包中页面进入小程序时，不需要下载主包
    
    例
        目录
        ├── app.js
        ├── app.json
        ├── app.wxss
        ├── moduleA
        │   └── pages
        │       ├── rabbit
        │       └── squirrel
        ├── moduleB
        │   └── pages
        │       ├── pear
        │       └── pineapple
        ├── pages
        │   ├── index
        │   └── logs
        └── utils
        在app.json的subpackages字段中对应的分包配置项中定义independent字段声明对应分包为独立分包
        {
            "pages": [
                "pages/index",
                "pages/logs"
            ],
            "subpackages": [
                {
                "root": "moduleA",
                "pages": [
                    "pages/rabbit",
                    "pages/squirrel"
                ]
                }, {
                "root": "moduleA",
                "pages": [
                    "pages/pear",
                    "pages/pineapple"
                ],
                "independent": true
                }
            ]
        }
    
    限制
        独立分包属于分包的一种。普通分包的所有限制都对独立分包有效。独立分包中插件、自定义组件的处理方式同普通分包。
        独立分包中不能依赖主包和其他分包中的内容，包括js文件、template、wxss、自定义组件、插件等。主包中的app.wxss对独立分包无效，应避免在独立分包页面中使用 app.wxss 中的样式；
        App 只能在主包内定义，独立分包中不能定义 App，会造成无法预期的行为；
        独立分包中暂时不支持使用插件。
    
    关于 getApp()
        由于独立分包不依赖主包，所以独立分包使用app共享数据时候，可以不存在app
        为了在独立分包中满足这一需求，基础库 2.2.4 版本开始 getApp支持 allowDefault参数，在 App 未定义时返回一个默认实现。当主包加载，App 被注册时，默认实现中定义的属性会被覆盖合并到真正的 App 中
        例：
            独立分包中js获取app
            const app = getApp({allowDefault: true}) // {}
            app.data = 456
            app.global = {}
    
            app。js中
            App({
                data: 123,
                other: 'hello'
            })
            console.log(getApp()) // {global: {}, data: 456, other: 'hello'}
    
    关于 App 生命周期
        当从独立分包启动小程序时，主包中 App 的 onLaunch 和首次 onShow 会在从独立分包页面首次进入主包或其他普通分包页面时调用

## 分包预下载
    开发者可以通过配置，在进入小程序某个页面时，由框架自动预下载可能需要的分包，提升进入后续分包页面时的启动速度。对于独立分包，也可以预下载主包。
    分包预下载目前只支持通过配置方式使用，暂不支持通过调用API完成。
    
    配置方法
        预下载分包行为在进入某个页面时触发，通过在 app.json 增加 preloadRule 配置来控制。
        例
            {
                "pages": ["pages/index"],
                "subpackages": [
                    {
                    "root": "important",
                    "pages": ["index"],
                    },
                    {
                    "root": "sub1",
                    "pages": ["index"],
                    },
                    {
                    "name": "hello",
                    "root": "path/to",
                    "pages": ["index"]
                    },
                    {
                    "root": "sub3",
                    "pages": ["index"]
                    },
                    {
                    "root": "indep",
                    "pages": ["index"],
                    "independent": true
                    }
                ],
                "preloadRule": {
                    "pages/index": {
                    "network": "all",
                    "packages": ["important"]
                    },
                    "sub1/index": {
                    "packages": ["hello", "sub3"]
                    },
                    "sub3/index": {
                    "packages": ["path/to"]
                    },
                    "indep/index": {
                    "packages": ["__APP__"]
                    }
                }
            }
        preloadRule 中，key 是页面路径，value 是进入此页面的预下载配置，每个配置有以下几项：
        字段	类型	        必填	默认值	说明
        packages	StringArray	是	    无	进入页面后预下载分包的 root 或 name。__APP__ 表示主包。
        network	String	        否	    wifi	在指定网络下预下载，可选值为：all: 不限网络 wifi: 仅wifi下预下载
    
    限制
        同一个分包中的页面享有共同的预下载大小限额 2M，限额会在工具中打包时校验。
        如，页面 A 和 B 都在同一个分包中，A 中预下载总大小 0.5M 的分包，B中最多只能预下载总大小 1.5M 的分包。

## 蓝牙
    蓝牙适配器模块生效周期为调用 wx.openBluetoothAdapter 至调用 wx.closeBluetoothAdapter 或小程序被销毁为止。
    在小程序蓝牙适配器模块生效期间，开发者才能够正常调用蓝牙相关的小程序 API，并收到蓝牙模块相关的事件回调。
    
    注意
        由于系统限制，Android 上获取到的 deviceId 为设备 MAC 地址，iOS 上则为设备 uuid。因此 deviceId 不能硬编码到代码中。
        目前不支持在开发者工具上进行蓝牙功能的调试，需要使用真机才能正常调用小程序蓝牙接口。
    
    低功耗蓝牙（BLE）注意事项
        iOS 上对特征值的 read、write、notify操作，由于系统需要获取特征值实例，传入的 serviceId 与 characteristicId 必须由 wx.getBLEDeviceServices 与 wx.getBLEDeviceCharacteristics 中获取到后才能使用。建议双平台统一在建立连接后先执行 wx.getBLEDeviceServices 与 wx.getBLEDeviceCharacteristics 后再进行与蓝牙设备的数据交互。

## 微信连wifi
    ①wifi商户-需要在公众号的后台开通wifi功能，并且关联小程序
    ②wifi硬件商-提供硬件服务
    3。wifi服务商
        Wi-Fi可通过提供线下服务解决方案和Wi-Fi综合解决方案，提升线下商户经营效率，拓展新客源。
    
        Wi-Fi服务商首先要注册微信开放平台账号，并通过开发者资质认证审核。在管理中心创建公众号第三方平台，务必选择“微信连Wi-Fi”权限集。
    
        在获得公众号授权登录后，可通过软件服务管理接口实现基于Wi-Fi的服务流程。
    
    移动端实现流程
        ①获取门店Wi-Fi信息
            改造portal型设备的第一步，是获得门店Wi-Fi信息，包括：appId，shop_id，ssid，secretkey。有两种获取门店Wi-Fi信息的方法：
            - 通过页面操作获得
                在进微信公众平台微信连Wi-Fi插件中，打开【设备管理】->【添加设备】，添加“新增微信方式连网+连网后近场服务”->”Portal型设备”；添加成功后即可获得门店Wi-Fi参数信息
                已添加设备也可在【设备详情】->【查看设备改造信息】中，获得门店Wi-Fi参数信息。
            - 调用接口获得
                调用接口可以添加portal型设备的网络信息，并获得secretkey。secretkey为加密字符串参数，是portal设备改造流程中的重要参数
                为防止secretkey泄露，可通过此接口重置刷新，重置后之前生成的secretkey将会失效
                注意
                    同一个门店可以添加多个ssid，最大添加100个ssid；
                    一个门店只能拥有一种设备类型，只要调用此接口添加一个ssid后，该门店即为portal型改造设备。如果门店下已有非portal型设备时，无法调用此接口
            例
                协议：https
                http请求方式: POST
                请求URL：https://api.weixin.qq.com/bizwifi/apportal/register?access_token=ACCESS_TOKEN
                POST数据格式：JSON


​                
​                参数	是否必须	说明
​                access_token	是	调用接口凭证
​                POST数据	是	JSON数据
​    
                POST数据示例
                {
                    "shop_id": 429620,
                    "ssid": "WX123",
                    "reset": false
                }
    
                字段	是否必填	说明
                shop_id	是	门店ID
                ssid	是	无线网络设备的ssid，限30个字符以内。 ssid支持中文，但可能因设备兼容性问题导致显示乱码，或无法连接等问题，相关风险自行承担 ！
                reset	否	重置secretkey，false-不重置，true-重置，默认为false
    
                返回结构
                {
                    "errcode": 0,
                    "data": {
                        "secretkey": "1af08ec5cdb70a4d7365bcd64d3120f6"
                    }
                }
                字段	说明
                secretkey	改造portal页面所需参数，该参数用于触发呼起微信的JSAPI接口的sign参数值的计算
        
        ②改造移动端portal页面
            若连网设备是移动设备，在portal页中引用下述微信JSAPI，让原有Wi-Fi portal页具备呼起微信的能力：
            <script type="text/javascript" src="https://wifi.weixin.qq.com/resources/js/wechatticket/wechatutil.js" ></script>
            调用JSAPI触发呼起微信客户端：
            Wechat_GotoRedirect(
            appId,      
            extend,     
            timestamp, 
            sign,       
            shop_id,   
            authUrl,   
            mac,      
            ssid );
            例：
                Wechat_GotoRedirect(
                'wx23fb4aaf04b8491e',  
                'demoNew',            
                '1441768153341',          
                'a355c78bad9be9235d2105d28f8e010c',   
                '6747662',  
                'http://wifi.weixin.qq.com/assistant/wifigw/auth.xhtml?httpCode=200',       
                'aa:aa:aa:aa:aa:aa',     
                '2099');
                参数	是否必须	说明
                appId	是	商家微信公众平台账号
                extend	是	extend里面可以放开发者需要的相关参数集合 ，最终将透传给运营商认证URL。extend参数只支持英文和数字，且长度不得超过300个字符。
                timestamp	是	时间戳使用毫秒
                sign	是	请求参数签名，具体计算方法见下方说明
                shopId	是	AP设备所在门店的ID，即shop_id
                authUrl	是	认证服务端URL，微信客户端将把用户微信身份信息向此URL提交并获得认证放行*
                mac	安卓设备必需	用户手机mac地址，格式冒号分隔，字符长度17个，并且字母小写，例如：00:1f:7a:ad:5c:a8
                ssid	是	AP设备的无线网络名称
    
                sign = MD5(appId + extend + timestamp + shopId + authUrl + mac + ssid + secretkey);
        
        3.支持临时放行上网请求
            请确保AP/AC在portal页打开后能够临时放行用户的上网请求。只有临时放行成功，才可以调用上述JSAPI呼起微信，换取用户身份信息，保证后续认证请求顺利完成，从而成功连网。
    
            注意：IOS呼起微信时如果网络不通Wi-Fi会被切走，导致连网失败，因此请务必确保AC/AP支持临时放行上网请求。
    
            部分安卓设备的web浏览器无法自动呼起微信客户端的问题，请参考常见问题中的解决方案。
        
        ④接受微信身份认证放行
            微信客户端被呼起后，将自动向authUrl（JSAPI的传入参数）发起请求，提交认证所需的用户微信身份信息参数，包括extend、openId、tid。
            微信客户端向authUrl发送请求示例：
            http://www.foo.com/portal/auth.html?extend=xxx&openId=xxx&tid=xxx
            参数	说明
            extend	为上文中调用呼起微信JSAPI时传递的extend参数，这里原样回传给商家主页
            openId	用户的微信openId
            tid	为加密后的用户手机号码（仅作网监部门备案使用）
    
            authUrl所对应的后台认证服务器必须能识别这些参数信息，并向微信客户端返回AC认证结果，微信客户端将根据http返回码，提示用户连网成功与否。
                http返回码为200，则认为服务认证成功，微信客户端跳转到成功连接页，用户点击“完成”按钮后，将跳转到商家主页
    
                若认证服务器需要转移认证请求，请返回302和下一跳地址，微信客户端将向下一跳地址再发起一次请求，302跳转仅支持一次
    
            注意：微信客户端一次请求的等待时间为10s，请确保后台认证服务器在微信客户端向authUrl发送请求10s之内返回AC认证结果，即http返回码。超过10s未返回认证结果将视为认证失败。
        
        5.实现扫二维码连网
            在完成第一至四步的前提下，进行下述配置，可实现portal设备扫二维码连Wi-Fi。具体操作如下：
            1. 改造portal server跳转内容
                当一个未认证的手机用户试图联网时，AC会将用户的http请求转跳到Portal Server上的Portal页面，这里AC需要进一步识别，如果这个http请求是来自于微信客户端，则在转跳URL上带上authUrl和extend两个约定参数即可。
                例
                http://www.foo.com/portal/portal.html?authUrl=http%3A%2F%2Fwww.foo.com%2Fportal%2Fauth.html&extend=xxx
                参数	说明
                authUrl	即第二步portal页中填写的authUrl，是认证服务端URL，微信客户端将把用户微信身份信息向此URL提交并获得认证放行
                extend	为上文中调用呼起微信JSAPI时传递的extend参数，这里原样回传给商家主页
            
            2. 如何识别http请求是否来自微信客户端
                在http数据包的header结构中解析“User-Agent”即可，判断是否包含关键字“micromessenger”（这里请注意不要拦截其他微信http请求，所以关键词请匹配好），示例代码如下：
                例
                String userAgent = request.getHeader("User-Agent");
                if(userAgent.matches(".*micromessenger.*")){  response.sendRedirect("http://www.foo.com/portal/portal.html?authUrl=http%3A%2F%2Fwww.foo.com%2Fportal%2Fauth.html&extend=xxx ");            
                }
                微信客户端将解析Portal Server转跳地址中的authUrl和extend参数，继续完成连接流程。
            
            3. 防止IOS自动弹出portal页
                为了防止IOS切换ssid时自动弹出portal页，请将IOS的嗅探地址“http://captive.apple.com/hotspot-detect.html”放入白名单。
            
            4. 下载物料二维码
                完成portal server改造后，调用
                "获取物料二维码"接口，下载该门店二维码，张贴于店内，顾客即可扫码连Wi-Fi。

## 开通微信连Wi-Fi插件
    调用微信连Wi-Fi其他所有接口的前提是已开通“微信连Wi-Fi”功能插件，目前开通插件共有两种方法
    1）在微信公众平台通过页面操作添加“微信连Wi-Fi“功能插件；
    2）调用此接口开通插件。
        1. 用户进入第三方平台网站并授权登录
            用户需要先进入第三方平台网站，如www.ABC.com。第三方平台引导用户进行微信公众号授权登录操作。
        2. 第三方平台获取开插件wifi_token
            协议：https
            http请求方式: GET
            请求URL：https://api.weixin.qq.com/bizwifi/openplugin/token?access_token=ACCESS_TOKEN
            POST数据格式：JSON
            参数	是否必须	说明
            access_token	是	调用接口凭证
            POST数据	是	JSON数据
            
            POST数据示例
                {
                    "callback_url": "http://weixin.qq.com/"
                }
                
            字段	是否必填	说明
            callback_url	是	回调URL，开通插件成功后的跳转页面。注：该参数域名必须与跳转进开通插件页面的页面域名保持一致，建议均采用第三方平台域名。
    
            返回数据
            {
                "errcode": 0,
                "data": {
                    "is_open": true,
                    "wifi_token": ""
                }
            }
            字段	说明
            is_open	该公众号是否已开通微信连Wi-Fi插件，true-已开通，false-未开通
            wifi_token	开通插件的凭证，当is_open为false时才返回值
        3. 引导用户进入开通插件页面
            第三方平台可以在自己的网页中放置“开通微信连Wi-Fi插件”的入口，引导用户进入开通插件页面。建议第三方平台采用“在当前页面打开“的形式打开开通插件页面。
            网址为：https://wifi.weixin.qq.com/biz/mp/thirdProviderPlugin.xhtml?token=xxxx ，该网址中第三方平台需提供已获取的wifi_token。
        4. 用户填写信息，开通插件
            用户在开通插件页面填写相关信息，完成开通插件操作。
        5. 跳转callback_url
            用户开通插件成功后，网页将自动跳转到第三方平台调用“获取开通插件wifi_token”接口时提供的callback_url中，完成开通插件流程。之后第三方平台可以调用其他接口为用户提供微信连Wi-Fi服务
## 连Wi-Fi完成页跳转小程序
    设置需要跳转的小程序，连网完成点击“完成”按钮，即可进入设置的小程序。
    注：只能跳转与公众号关联的小程序。
    例
        协议：https
        请求方式: POST  
        请求URL： https://api.weixin.qq.com/bizwifi/finishpage/set?access_token=ACCESS_TOKEN  
        POST数据格式：JSON
        数	是否必填	说明
        access_token	是	调用接口凭证
        POST数据	是	JSON数据
    
        POST数据示例
        {
            "shop_id": 429620,
            "finishpage_url": "",  
            "wxa_user_name": "gh_966b66e00888",  
            "wxa_path": "pages/index/index",  
            "finishpage_type": 1  
        }
        字段	是否必填	说明
        shop_name	是	门店名称
        finishpage_url	否	连网完成页URL，finishpage_type为0时有效
        wxa_user_name	否	连网完成页跳转小程序原始id，finishpage_type为1时有效，要求小程序与公众号有绑定关系
        wxa_path	否	连网完成页跳转小程序路径，finishpage_type为1时有效，需要做urlencode
        finishpage_type	否	连网完成页跳转类型，0为H5，1为小程序
    
    设置顶部banner跳转小程序接口
        用户连Wi-Fi后长期逗留在场所内，可以在连接Wi-Fi后进入微信点击微信聊首页欢迎语，即可进入预先设置的小程序中获得资讯或服务。
        例
            协议：https
            请求方式: POST  
            请求URL：https://api.weixin.qq.com/bizwifi/homepage/set?access_token=ACCESS_TOKEN  
            POST数据格式：JSON
            access_token	是	调用接口凭证
            POST数据	是	JSON数据
    
            POST数据示例
            {
                "shop_id": 2200766,  
                "template_id": 2,  
                "struct": {  
                    "wxa_user_name": "gh_5cb1b4334f3a",  
                    "wxa_path": "index.html?query=abc"  
                }
            }
            字段	是否必填	说明
            shop_id	是	门店ID
            template_id	是	2-关联小程序（支持门店小程序）
            struct	是	连网完成页跳转小程序原始id，finishpage_type为1时有效，要求小程序与公众号有绑定关系
            wxa_user_name	是	账号原始ID
            wxa_path	是	小程序页面路径
    
    查询门店WiFi信息接口
        协议：https  
        http请求方式: POST  
        请求URL：https://api.weixin.qq.com/bizwifi/shop/get?access_token=ACCESS_TOKEN  
        POST数据格式：JSON
        参数	是否必填	说明
        access_token	是	调用接口凭证
        POST数据	是	JSON数据
    
        POST数据示例
            {  
                "errcode": 0,  
                "data": {  
                    "shop_name": "南山店",  
                    "ssid": " WX123",  
                    "ssid_list": [  
                    "WX123",  
                    "WX456"  
                    ],  
                    "ssid_password_list": [  
                    {  
                        "ssid": "WX123",  
                        "password": "123456789"  
                    },  
                    {  
                        "ssid": "WX456",  
                        "password": "21332465dge"  
                    }  
                    ],  
                    "password": "123456789",  
                    "protocol_type": 4,  
                    "ap_count": 2,  
                    "template_id": 1,  
                    "homepage_url": "http://www.weixin.qq.com/",  
                    "bar_type": 1,  
                    "sid":"",  
                    "poi_id":"285633617",  
                    "homepage_wxa_user_name":"",  
                    "homepage_wxa_path":"",  
                    "finishpage_url":"",  
                    "finishpage_wxa_user_name":"gh_966b66e00888",  
                    "finishpage_wxa_path":"pages/index/index",  
                    "finishpage_type":1,  
                }  
            }
            字段	是否必填	说明
            shop_name	是	门店名称
            ssid	是	无线网络设备的ssid，未添加设备为空，多个ssid时显示第一个
            ssid_list	是	无线网络设备的ssid列表，返回数组格式
            ssid_password_list	是	ssid和密码的列表，数组格式。当为密码型设备时，密码才有值
            password	是	设备密码，当设备类型为密码型时返回
            protocol_type	是	门店内设备的设备类型，0-未添加设备，4-密码型设备，31-portal型设备
            ap_count	是	门店内设备总数
            template_id	是	商家主页（bar条）模板类型 0 默认页 1 自定义h5 2 跳转小程序
            homepage_url	是	商家主页（bar条）链接
            bar_type	是	顶部常驻入口上显示的文本内容：0--欢迎光临+公众号名称；1--欢迎光临+门店名称；2--已连接+公众号名称+WiFi；3--已连接+门店名称+Wi-Fi
            finishpage_url	是	连网完成页链接,finishpage_type为0时有效
            sid	是	商户自己的id，与门店poi_id对应关系，建议在添加门店时候建立关联关系，具体请参考“微信门店接口”
            poi_id	是	门店ID（适用于微信卡券、微信门店业务），具体定义参考微信门店，与shop_id一一对应。
            homepage_wxa_user_name	是	商家主页（bar条）跳转的小程序原始id，template_id为2时有效
            finishpage_wxa_user_name	是	完成页跳转的小程序原始id，finishpage_type为1时有效
            inishpage_wxa_path	是	完成页跳转的小程序路径，需要做urlencode，finishpage_type为1时有效
            finishpage_type	是	完成页跳转类型 0为H5；1为小程序

## 获取Wi-Fi门店列表

## UnionID 机制说明
    如果开发者拥有多个移动应用、网站应用、和公众帐号（包括小程序），可通过 UnionID 来区分用户的唯一性，因为只要是同一个微信开放平台帐号下的移动应用、网站应用和公众帐号（包括小程序），用户的 UnionID 是唯一的
    换句话说，同一用户，对同一个微信开放平台下的不同应用，unionid是相同的。
    
    unionID获取途经
        调用接口 wx.getUserInfo，从解密数据中获取 UnionID。注意本接口需要用户授权，请开发者妥善处理用户拒绝授权后的情况。
    
        如果开发者帐号下存在同主体的公众号，并且该用户已经关注了该公众号。开发者可以直接通过 wx.login + code2Session 获取到该用户 UnionID，无须用户再次授权。
    
        如果开发者帐号下存在同主体的公众号或移动应用，并且该用户已经授权登录过该公众号或移动应用。开发者也可以直接通过 wx.login + code2Session 获取到该用户 UnionID ，无须用户再次授权。
    
    微信开放平台绑定小程序流程
        前提：微信开放平台帐号必须已完成开发者资质认证

## 授权
    分接口需要获得用户授权同意后才能调用。此类接口调用时：
        如果用户未接受或拒绝过此权限，会弹窗询问用户，用户点击同意后方可调用接口；
        如果用户已授权，可以直接调用接口；
        如果用户已拒绝授权，则不会出现弹窗，而是直接进入接口 fail 回调。请开发者兼容用户拒绝授权的场景。
    
    部分接口需要经过用户授权同意才能调用。我们把这些接口按使用范围分成多个 scope
    提前发起授权请求
        开发者可以使用 wx.authorize 在调用需授权 API 之前，提前向用户发起授权请求。
    scope 列表
    scope	                对应接口	                                         描述
    scope.userInfo	        wx.getUserInfo	                                    用户信息
    scope.userLocation	    wx.getLocation, wx.chooseLocation, wx.openLocation	地理位置
    scope.address	        wx.chooseAddress	                                通讯地址
    scope.invoiceTitle	    wx.chooseInvoiceTitle	                            发票抬头
    scope.werun	            wx.getWeRunData	                                    微信运动步数
    scope.record	        wx.startRecord	                                    录音功能
    scope.writePhotosAlbum	wx.saveImageToPhotosAlbum, wx.saveVideoToPhotosAlbum	保存到相册
    scope.camera	        <camera />组件                                       摄像头
    注意：wx.authorize({scope: "scope.userInfo"})，无法弹出授权窗口，请使用 <button open-type="getUserInfo"/>

## 开放数据校验与解密
    签名校验以及数据加解密涉及用户的会话密钥 session_key。 
    开发者应该事先通过 wx.login 登录流程获取会话密钥 session_key 并保存在服务器。
    为了数据不被篡改，开发者不应该把 session_key 传到小程序客户端等服务器外的环境。
    
    - 数据签名校验
        为了确保开放接口返回用户数据的安全性，微信会对明文数据进行签名。开发者可以根据业务需要对数据包进行签名校验，确保数据的完整性。
            调用wx.getUserInfo获取数据时，接口会同时返回 rawData、signature，其中 signature = sha1( rawData + session_key )
            开发者将 signature、rawData 发送到开发者服务器进行校验。服务器利用用户对应的 session_key 使用相同的算法计算出签名 signature2 ，比对 signature 与 signature2 即可校验数据的完整性。
    - 加密数据解密算法
        接口如果涉及敏感数据（如wx.getUserInfo当中的 openId 和 unionId），接口的明文内容将不包含这些敏感数据。
        开发者如需要获取敏感数据，需要对接口返回的加密数据(encryptedData) 进行对称解密。 解密算法如下：
    
        解密算法如下：
            对称解密使用的算法为 AES-128-CBC，数据采用PKCS#7填充。
            对称解密的目标密文为 Base64_Decode(encryptedData)。
            对称解密秘钥 aeskey = Base64_Decode(session_key), aeskey 是16字节。
            对称解密算法初始向量 为Base64_Decode(iv)，其中iv由数据接口返回。
    
        另外，为了应用能校验数据的有效性，会在敏感数据加上数据水印( watermark )
            watermark参数说明：
            参数	类型	说明
            appid	String	敏感数据归属 appId，开发者可校验此参数与自身 appId 是否一致
            timestamp	Int	敏感数据获取的时间戳, 开发者可以用于数据时效性校验
    
    - 会话密钥 session_key 有效性
        wx.login 调用时，用户的 session_key 可能会被更新而致使旧 session_key 失效（刷新机制存在最短周期，如果同一个用户短时间内多次调用 wx.login，并非每次调用都导致 session_key 刷新）。开发者应该在明确需要重新登录时才调用 wx.login，及时通过 code2Session 接口更新服务器存储的 session_key。
    
        微信不会把 session_key 的有效期告知开发者。我们会根据用户使用小程序的行为对 session_key 进行续期。用户越频繁使用小程序，session_key 有效期越长。
    
        开发者在 session_key 失效时，可以通过重新执行登录流程获取有效的 session_key。使用接口 wx.checkSession可以校验 session_key 是否有效，从而避免小程序反复执行登录流程。
    
        当开发者在实现自定义登录态时，可以考虑以 session_key 有效期作为自身登录态有效期，也可以实现自定义的时效性策略。
    
    - code2Session
        登录凭证校验。通过 wx.login() 接口获得临时登录凭证 code 后传到开发者服务器调用此接口完成登录流程
        请求地址
        GET https://api.weixin.qq.com/sns/jscode2session?appid=APPID&secret=SECRET&js_code=JSCODE&grant_type=authorization_code
        参数
        string appid    小程序 appId
        string secret   小程序 appSecret
        string js_code  登录时获取的 code
        string grant_type   授权类型，此处只需填写 authorization_code
        返回数据
        属性	类型	说明
        openid	string	用户唯一标识	
        session_key	string	会话密钥	
        unionid	string	用户在开放平台的唯一标识符，在满足 UnionID 下发条件的情况下会返回，详见 UnionID 机制说明。	
        errcode	number	错误码	
        errMsg	string	错误信息

## 获取手机号
    获取微信用户绑定的手机号，需先调用wx.login接口。
    因为需要用户主动触发才能发起获取手机号接口，所以该功能不由 API 来调用，需用 <button> 组件的点击来触发。
    
    使用方法
        需要将 <button> 组件 open-type 的值设置为 getPhoneNumber，当用户点击并同意之后，可以通过 bindgetphonenumber 事件回调获取到微信服务器返回的加密数据， 然后在第三方服务端结合 session_key 以及 app_id 进行解密获取手机号。
    注意
        在回调中调用 wx.login 登录，可能会刷新登录态。此时服务器使用 code 换取的 sessionKey 不是加密时使用的 sessionKey，导致解密失败。建议开发者提前进行 login；或者在回调中先使用 checkSession 进行登录态检查，避免 login 刷新登录态。
    例
        <button open-type="getPhoneNumber" bindgetphonenumber="getPhoneNumber"></button> 
        Page({ 
            getPhoneNumber (e) { 
                console.log(e.detail.errMsg) 
                console.log(e.detail.iv) 
                console.log(e.detail.encryptedData) 
            } 
        })
        返回数据
        参数	类型	说明
        encryptedData	String	包括敏感数据在内的完整用户信息的加密数据，详细见加密数据解密算法
        iv	String	加密算法的初始向量，详细见加密数据解密算法
    
        encryptedData 解密后为以下 JSON 结构，详见加密数据解密算法
        {
            "phoneNumber": "13580006666",  
            "purePhoneNumber": "13580006666", 
            "countryCode": "86",
            "watermark":
            {
                "appid":"APPID",
                "timestamp": TIMESTAMP
            }
        }

## 转发
    调用 wx.showShareMenu 并且设置 withShareTicket 为 true ，当用户将小程序转发到任一群聊之后，此转发卡片在群聊中被其他用户打开时，可以在 App.onLaunch 或 App.onShow 获取到一个 shareTicket。通过调用 wx.getShareInfo() 接口传入此 shareTicket 可以获取到转发信息。
    
    页面内发起转发
        通过给 button 组件设置属性 open-type="share"，可以在用户点击按钮后触发 Page.onShareAppMessage 事件，如果当前页面没有定义此事件，则点击后无效果。相关组件：button
        Tips
        不自定义转发图片的情况下，默认会取当前页面，从顶部开始，高度为 80% 屏幕宽度的图像作为转发图片。
        转发的调试支持请查看 普通转发的调试支持 和 带 shareTicket 的转发
        只有转发到群聊中打开才可以获取到 shareTickets 返回值，单聊没有 shareTickets
        shareTicket 仅在当前小程序生命周期内有效
        由于策略变动，小程序群相关能力进行调整，开发者可先使用 wx.getShareInfo 接口中的群ID进行功能开发。

## 打开 App
    此功能需要用户主动触发才能打开 APP，所以不由 API 来调用，需要用 open-type 的值设置为 launchApp 的 <button> 组件的点击来触发。
    
    当小程序从 APP 分享消息卡片的场景打开（场景值 1036，APP 分享小程序文档 iOS / Android） 或从 APP 打开的场景打开时（场景值 1069），小程序会获得打开 APP 的能力，此时用户点击按钮可以打开分享该卡片的 APP。即小程序不能打开任意 APP，只能 跳回 分享该小程序卡片的 APP。
    
    在一个小程序的生命周期内，只有在特定条件下，才具有打开 APP 的能力。 打开 APP 的能力 可以理解为由小程序框架在内部管理的一个状态，为 true 则可以打开 APP，为 false 则不可以打开 APP。
    
    在小程序的生命周期内，这个状态的初始值为 false，之后会随着小程序的每次打开（无论是启动还是切到前台）而改变：
        当小程序从 1036（App 分享消息卡片） 打开时，该状态置为 true。
        当小程序从 1069（App 打开小程序） 打开时，该状态置为 true。
        当小程序从以下场景打开时， 该状态不变，即保持上一次打开小程序时该状态的值：
        1038（从小程序返回，基础库 2.2.4 及以上版本支持）
        1089（微信聊天主界面下拉）
        1090（长按小程序右上角菜单唤出最近使用历史）
        当小程序从非以上陈列的场景打开时，该状态置为 false。
    
    - 使用方法
        小程序端
            需要将 <button> 组件 open-type 的值设置为 launchApp。如果需要在打开 APP 时向 APP 传递参数，可以设置 app-parameter 为要传递的参数。通过 binderror 可以监听打开 APP 的错误事件。
    
        app 端
            APP 需要接入 OpenSDK。 文档请参考 iOS / Android
    
            Android 第三方 app 需要处理 ShowMessageFromWX.req 的微信回调，iOS 则需要将 appId 添加到第三方 app 工程所属的 plist 文件 URL types 字段。 app-parameter 的获取方法，请参考 Android SDKSample 中 WXEntryActivity 中的 onResp 方法以及 iOS SDKSample 中 WXApiDelegate 中的 onResp 方法。

## 模板消息
    使用步骤
        ①获取模板 ID
            通过模板消息管理接口获取模板 ID（详见 模板消息管理）
            在微信公众平台手动配置获取模板 ID
        ②页面的 <form/> 组件，属性 report-submit 为 true 时，可以声明为需要发送模板消息，此时点击按钮提交表单可以获取 formId，用于发送模板消息。或者当用户完成 支付行为，可以获取 prepay_id 用于发送模板消息。
        3.调用接口下发模板消息（详见 sendTemplateMessage ）
## 客服消息
    <button> 组件 open-type 的值设置为 contact，当用户点击后就会进入客服会话，如果用户在会话中点击了小程序消息，则会返回到小程序，开发者可以通过 bindcontact 事件回调获取到用户所点消息的页面路径 path 和对应的参数 query
    <button open-type="contact" bindcontact="handleContact"></button> 
    Page({
        handleContact (e) {
            console.log(e.path)
            console.log(e.query)
        }
    })
    参数	类型	说明
    path	String	小程序消息指定的路径
    query	Object	小程序消息指定的查询参数
    
    - 后台接入消息服务
        接入微信小程序消息服务，开发者需要按照如下步骤完成：
            填写服务器配置
            验证服务器地址的有效性
            据接口文档实现业务逻辑
## 卡劵 

​	小程序卡券接口支持在小程序中领取/查看/使用公众号 AppId 创建的会员卡、票、券（含通用卡）。更多使用方法可参考 [小程序&卡券打通](https://mp.weixin.qq.com/cgi-bin/announce?action=getannouncement&key=1490190158&version=1&lang=zh_CN&platform=2)

​	目前只有认证小程序才能使用卡券接口，可参考 [指引](https://developers.weixin.qq.com/miniprogram/product/renzheng.html?t=18110616) 进行认证。

​	小程序内可以通过 [wx.addCard](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/card/wx.addCard.html) 接口给用户添加卡券。通过 [wx.openCard](https://developers.weixin.qq.com/miniprogram/dev/api/open-api/card/wx.openCard.html) 让用户选择已有卡券。

## 获取二维码

通过后台接口可以获取小程序任意页面的二维码，扫描该二维码可以直接进入小程序对应的页面，所有生成的二维码永久有效，可放心使用

