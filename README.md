# YuFei Design Front-end API


## 1. 如何使用

> tips: 但由于代码中使用到了ES6中的新特性Promise，对于不兼容Promise的浏览器(如IE9)，须先引入promise.js

1. ES6语法或前端构建工具环境下：
````
// html
 
<script src="js/main.js"></script>

 
</body>
````
````main.js
// main.js
     
import Promise from '../api/promise';
import API from '../api/api';
    
let api = new API(options);
    
````

2. ES5语法：
````
// html
 
<script src="api/promise.js"></script>
<script src="api/api.js"></script>
<script src="js/main.js"></script>

 
</body>
````
````main.js
// main.js
 
var api = new API(options);

````

## 2. API配置项(options)
  ### rootdir
  配置网站根目录地址，默认值：''
  > 例：
    rootdir: 'test.yfd.com.cn/yinger/' 或 rootdir: 'test.yfd.com.cn/yinger'，<br>
    很显然最后一条斜杠是可有可无的
  
  ### database
  配置网站所使用的数据库，可选'access'或'sql'，默认值：'access'
  > 例：
    database: 'access' <br>
    当值为'access'或'sql'之外的任何值时，将自动设置为'access'
    
  ### fixPath
  配置需要自动拼接路径的字段，当读取该字段时，自动为该字段拼接rootdir，如不需要自动拼接请设置为false，默认值：['img_url', 'big_img', 'video_src']
  > 当只有一个字段时，可直接写字段名，当有多个字段时为一个数组，例：<br>
  不需要拼接：fixPath: false <br>
  只需要拼接img_url字段： fixPath: 'img_url' <br>
  需要多个字段： fixPath: ['img_url', 'big_img', 'video_src']
  
  
  ### decode
  配置需要自动解码的字段，当读取该字段时，自动解码(unescape(str))该字段，如不需要自动解码请设置为false，默认值：['zhaiyao', 'content']

## 3. API实例属性
  ### rootdir
  返回实例去掉最后一条斜杠(如果有)的rootdir；
  ### database
  返回实例的数据库类型，'access'或'sql'；
  
  > 例：

   ````database
   var api = new API({
       rootdir: 'test.yfd.com.cn/yinger/'
   });
    
   console.log(api.rootdir)  --> test.yfd.com.cn/yinger
   console.log(api.database) --> access
   ````
  
## 4. API实例方法

  > a. ajax方法是所有方法的底层封装实现 <br>
    b. 除getUrl和ajax方法外，所有方法均返回一个Promise实例，
    options配置项与ajax方法的配置项相同并设置了适当的默认配置，
    一般情况下，除了data属性外，其他属性不需要特别设置，当只需要配置data属性时，可用data当做options

  ### getRow(options)
  获取一行（一条记录），必要参数options
  ````data
  // options中的data属性全部可用的配置如下：
  // 如果需要返回的数据中包含以下字段(id字段除外)，请把该字段设置为1
   
  var data = {
      id: 214,              // 记录ID  
      title_en: 0,          // 英文标题
      sub_title: 0,         // 副标题
      big_img: 0,           // 大图地址
      video_src: 0,         // 视频地址
      sell_price: 0,        // 销售价格
      market_price: 0,      // 市场价格
      stock_quantity: 0,    // 库存数量
      goods_no: 0,          // 商品货号
      puramt: 0,            // 销售成本
      tel_phone: 0          // 电话
  }
      
  ````
  
  ### getRows(options)
  获取多行（多条记录）列表，必要参数options
  ````angular2html
  var data = {
       categoryId: 214,      // 类别ID
       pageSize: 6,          // 每页大小
       pageIndex: 1,         // 第几页
       title_en: 0,          // 英文标题
       sub_title: 0,         // 副标题
       big_img: 0,           // 大图地址
       video_src: 0,         // 视频地址
       filter: 0,            // 带筛选字段可选值：'置顶' | '推荐' | '热门'
       sell_price: 0,        // 销售价格
       market_price: 0,      // 市场价格
       stock_quantity: 0,    // 库存数量
       goods_no: 0,          // 商品货号
       puramt: 0,            // 销售成本
       tel_phone: 0          // 电话
   }
  ````
  
  ### getSublevel(options)
  获取某分类下的子级列表，必要参数options
  ````data
  // options中的data属性全部可用的配置如下：
  // 如果需要返回的数据中包含以下字段(id字段除外)，请把该字段设置为1
   
  var data = {
      categoryId: 214,    // 类别ID
  }
        
  ````
  
  ### getProvinces([options])
  获取全部省份和城市列表，可选参数options
  
  ### getSeo([options])
  获取省份和城市，可选参数options
  
  ### getAlbum(options)
  获取某条记录的相册列表，必要参数options
  ````data
  var data = {
      id: 214,    // 记录ID
  }
        
  ````
  
  ### getStores([options])
  获取所有店铺信息，可选参数options
  
  ### postMsg(options)
  提交留言反馈，必要参数options
  ````data
  var data = {
      txtName: 'yfd',            // 称呼
      txtEmail: 'yfd@yfd.com'    // 邮箱
      tel: 123456                // 号码
      content: 'yfd'             // 内容
  }
        
  ````
  
  ### postEmail(options)
  邮箱订阅，必要参数options
  ````data
  var data = {
      txtName: 'yfd',            // 称呼
      txtEmail: 'yfd@yfd.com'    // 邮箱
      tel: 123456                // 号码
      content: 'yfd'             // 内容
  }
        
  ````
  ### search(options)
  关键字查询，必要参数options
  ````data
  var data = {
      keyword: 'yfd'    // 关键字
  }
        
  ````

  ### ※ getUrl(fnName)
  返回上述方法对应的请求地址，必要参数fnName是对应的方法名(函数名)；
  ````
    console.log(api.getUrl('getRow'));
    // test.yfd.com.cn/yinger/tools/yufei.ashx?action=get_model_parms
  ````
  
  ### ※ ajax(options);
  向服务器发起一个请求，必要参数options，使用方法与$.ajax(options)类似
  ````options配置说明
  // 默认options
   
  optons = {
      method: 'GET',          // [String] 配置请求方法 
      url: '',                // [String] 配置请求地址
      timeout: 0,             // [Number] 配置请求超取消请求时间，单位ms，0表示不取消请求 
      data: {},               // [Object] 配置向服务器发送的数据
      dataType: 'json',       // [String] 配置获取的数据类型，'json'或'text' 
      async: true,            // [Boolean] 配置是否发起异步请求
      user: null,             // [String] 配置用户名 
      password: null,         // [String] 配置用户密码
      sendBefore: null,       // [Function] 配置请求发出前的回调函数
      success: null,          // [Function] 配置请求成功后的回调函数
      error: null,            // [Function] 配置请求出错时的回调函数
      completed: null,        // [Function] 配置请求完成后的回调函数
      autoCompletePath: '',   // [String | Array | Boolean] 配置自动添加路径的字段
      completeRootdir: ''     // [String] 配置自动添加路径前缀
  }
  ````
  
## 5. 演示
````demo
// main.js
 
import Promise from '../api/promise';
import API from '../api/api';
 
// 实例化
let api = new API({
    rootdir: 'test.yfd.com.cn/yinger/'
}); 
 
 
// 1. 获取单条记录，
// 使用默认配置，请求id为214的记录，需要英文标题
var data: {
        id: 214, 
        title_en: 1
    };
api.getRow(data).then(function(response){
    console.log('response: %o', response);
});
 
// 个性化配置，请求id为214的记录，需要英文标题
var options = {
        data: {
            id: 214, 
            title_en: 1
        },
        autoCompletePath: false
    };
api.getRow(options).then(function(response){
    console.log('response: %o', response);
});

````
  
