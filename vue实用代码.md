## vue实用代码 ##

# 批量导出功能
```
/**
     * 批量导出功能
     */
    handleExportAll (url) {
      let searchJson = {
        companyId: this.active,
        reserve1: this.isCurrentCompany ? 1 : 0,
        measureCode: ''
      }
      this.searchSets.forEach(ele => {
        searchJson[ele['key']] = ele.value
      })
      this.$http.post(url, searchJson, {loading: true, responseType: 'blob'}).then(res => {
        const data = res.data
        if (!data) {
          return
        }
        let blob = new Blob([data])
        let url = window.URL.createObjectURL(blob)
        let link = document.createElement('a')
        link.style.display = 'none'
        link.href = url.replace(/"/g, '')
        let fileName = res.headers['content-disposition']
        if (fileName && fileName.length >= 2) {
          fileName = fileName.split('=')[1]
        }
        fileName = decodeURIComponent(fileName)
        link.setAttribute('download', fileName)
        document.body.appendChild(link)
        link.click()
      })
    }
```
## webpack+vue脚手架 ##
> [ ] `npm install vue -g`  //如果全局安装过可忽略
> [ ] `npm install vue-cli -g`//如果全局安装过可忽略
> [X] `vue init webpack yourprojectname(项目名)`

## webpack配置less-loader ##
weboack-cli 脚手架中
```
    {
        test: /\.(less|css)$/,    
        loader: "style-loader!css-loader!less-loader",
      },
```
 npm安装完loader即可使用

# 不认识dispatch
检查store是否挂在到模板上
```
    import store from './store'
    //没有vue.use（）
    new Vue({
      el: '#app',
      store,/////挂在//
      router,
      components: { App },
      template: '<App/>'
    })
```
# 不认识jsonp
检查
```
import VueResource from 'vue-resource'
Vue.use(VueResource)
```
## vuex的异步调用用法 ##
## 可以好好利用下flex grow ##
```
#重复利用剩余空间
# 比如一行中排列，左边是一张40px 40px 的图片，右边是文字说明
    
    .singer-item{
      display: flex; //flex布局
      height: 40px;
      align-items:  center;
      padding: 10px 5px;
    }
    .singer-item img{//左边图片宽度
      width: 40px;
      height: 40px;
      border-radius:  50%;
    }
    
    .singer-info{
      display: flex;
      align-items: center;
      padding-left: 10px;
      height: 40px;
      flex-grow: 1;//沾满右边空间
      border-bottom: #eeeeee 1px solid;
    }
```
## text-align的用法 ##
| text-align | 属性规定元素中的文本的水平对齐方式     |
| --------   | -----:  |
| left       |把文本排列到左边。默认值：由浏览器决定。|
|right|把文本排列到右边|
|center|把文本排列到中间|
|justify|实现两端对齐文本效果|
|inherit|规定应该从父元素继承 text-align 属性的值|
`可用于调整div中img的垂直居中`

## 不换行的方式 ##
```
  white-space: nowrap; /*如果是中文 设置文字超出范围不断行*/
  overflow: hidden;;/*设置超出控件范围隐藏*/
  text-overflow: ellipsis; /*设置多余文本隐藏显示*/
```

## 过度动画 ##
 在进入/离开的过渡中，会有 6 个 class 切换。

>[] **v-enter**：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。

>[] **v-enter-active**：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。
>[] v-enter-to: 2.1.8版及以上 定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。
>[] **v-leave**: 定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。
>[] **v-leave-active**：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。
>[] v-leave-to: 2.1.8版及以上 定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。
```
    <div id="example-1">
      <button @click="show = !show">
        Toggle render
      </button>
      <transition name="slide-fade">
        <p v-if="show">hello</p>
      </transition>
    </div>
```
```
    /* 可以设置不同的进入和离开动画 */
    /* 设置持续时间和动画函数 */
    .slide-fade-enter-active {
      transition: all .3s ease;
    }
    .slide-fade-leave-active {
      transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }
    .slide-fade-enter, .slide-fade-leave-to
    /* .slide-fade-leave-active for below version 2.1.8 */ {
      transform: translateX(10px);
      opacity: 0;
    }
```
- transform: translateX(-50%)
 >[ ] 把元素沿着横向（x轴）移动自身宽度的50%，一般是从左侧为开始点也就是0点。而数值是-50%，所以是从左侧0点向左移动自身宽度的50%

- transform: translateX(10px)
   >[ ] 沿x轴平移10px
   >[ ] **正数值表示元素沿X轴的正方向移动，负数值表示元素沿X轴的负方向移动**
## router ##
- 动态路由(query)
router中配置：
``` 
        {
          path: 'rank',
          name: 'rank',
          component: rankPage,
        }
```
调用方式：
```
this.$router.push({path:'rank',query:{id:1}})//rank？id=1
```
调用结果
```
http://localhost:8081/rank?id=1
```
参数获取方式
```
this.$route.query.id
```
注意事项：
    **path只能跟query共存，不能跟params共事**
- - 动态路由(params)
配置方式
```
        {
          path: 'rank/:id',   //动态
          name: 'rank',
          component: rankPage,
        }
```
调用方式
```
this.$router.push({path:'rank',params:{id:1}})//rank/1

```
调用结果     
```
http://localhost:8081/rank/1
```
参数获取方式
```
this.$route.params.id
```


## 创建远程仓库 ##
>[] 先在git中创建new repository 
>[] 项目根目录，`git bash`
```
    git remote
    git remote add origin  git@github.com:yayalif/miaomiao.git
    git remote
    git add.
    git commit -m 'first commit'
    git push -u origin master //master  分支
    
    
    //创建并切换开发分支
    git checkout -b dev
    //push 开发分支
    git push origin dev
    
    //一般多人协作也不在dev分支直接开发，而是（根据迭代）在创建一个分支
    git push -b 0725
    git push origin 0725
```
## 合并分支 ##
>[] 在当前分支：
    ```
            git pull
            git status
            git add .
            git commit -m 'commit'
            git log //查看日志
            //推送远程
            git push origin dev
    ```
>[]  切换分支
```
    git checkout dev
    git merge '当前分支 如0725' --no-ff
    
```

    
## assets 和 public的区别##
都是可以放置静态资源，
assest 一般放置比较小的图片、logo，可以转成base64的
public一般放置大的资源
## router的引入方式 ##
```
{
    path: '/',
    name: 'home',
    component：Home
}
{
//按需加载，适用于大项目
    path:'about',
    name:'about',
    component:()=>import('./views/about')
    
}
```
## 提高性能的方式 ##
>[] 按需引入，比如上述的router import
>[] 缓存 比如`keep-alive`对页面进行缓存，否则每次切换页面会重新进行加载

## vue 解决跨域问题 ##
vue-cli脚手架自带的配置`vue.config.js`


## 函数防抖 ##
定义： 快速输入的之后，之前的不触发，后续的才触发，  应用场景：用户输入的时候，用watch监听，并发送异步请求；
解决办法：
>[] 延时定时器中触发动作，setTimeout（）
```
    {
        clearTimeout(),
        setTimeout()
    }
```
>[] 采用axios中自带的abort
```
methods:{
    cancelRequest(){
          if(typeof this.source ==='function'){
              this.source('终止请求')
          }
      },
}
watch:{
        message(newValue) {
      var that = this;
      this.cancelRequest()
      // console.log(newValue)
      this.$axios
        .get("/api/searchList?cityId=10&kw=" + newValue, {
          cancelToken: new this.$axios.CancelToken(function(c) {
            that.source = c;
          })
        })
        .then(res => {
          if (res.data.data.movies) {
            this.moviesList = res.data.data.movies.list;
            console.log(this.moviesList);
          }
        })
        .catch(err => {
          if (this.$axios.isCancel(err)) {
            console.log("Rquest canceled", err.message); //请求如果被取消，这里是返回取消的message
          } else {
            //handle error
            console.log(err);
          }
        });
    }

}
```

##  移动端 的几个事件##
> [ ] touch的开始事件是@touchstart，但是滑屏的时候也会触发，
> [ ]移动过程是@touchmove,
结束事件是@touchend
> [ ] 移动端点击事件不用click，有延迟

>[ ] tap：zepto vue-touch better-scoll
>[ ] 滑屏： iscroll swiper  better-scroll
>[] better-scroll  触发条件
  - 可视页面小于可滑动页面
  - 数据加载完之后
  
  ```

      <div class=wraper ref=‘wrapper’>
        <ul> 
            <li>222</li>
            <li>222</li>
            <li>222</li>
            <li>222</li>
        </ul>
        //注意滚动的时wrapper的第一个子元素，第二个和后面的元素不会发生滚动
        <ul>
            <li>我不会滚动</li>
            <li>我不会滚动</li>
            <li>我不会滚动</li>
        </ul>
      </div>
      
      //注：
     .wrapper{
     //不能采用flex布局，否则，wrapper会自动适应为和ul的高度一样，不会触发滚动事件，
      //设置固定高度
      height：500px；
      overflow：hidden；
     }
      

  ```









