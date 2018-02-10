# YuFei Design Front-end API


## 1. 如何使用

> tips: api.js不依赖jQuery,但由于其中使用到了IE9不兼容的新特性Promise，为了兼容IE9，须先引入promise.js

````
<script src="api/promise.js"></script>
<script src="api/api.js"></script>
<script>
 
  // 实例化
  var api = new API(options);
  console.log('api: %o', api);
  
</script>
 
</body>
````

## 2. API配置项(options)
  ### rootdir
  配置网站根目录地址，默认值：''
  > 例：
    rootdir: 'test.yfd.com.cn/yinger/' 或 rootdir: 'test.yfd.com.cn/yinger'，<br>
    很显然最后一条斜杠是可有可无的
  
  ### database
  配置网站所使用的数据库，默认值：'access'
  > 例：
    database: 'access' or database: 'sql'
    
  ### autoCompletePath
  配置需要自动拼接路径的字段，当读取该字段时，自动为该字段拼接rootdir，默认值：['img_url', 'big_img', 'video_src']
  > 当只有一个字段时，可直接写字段名，当有多个字段时为一个数组，例：<br>
  只需要拼接img_url字段： autoCompletePath: 'img_url' <br>
  需要多个字段： autoCompletePath: ['img_url', 'big_img', 'video_src']
  

## 3. API实例属性
  ### rootdir
  ````$xslt
  console.log(api.rootdir) --> test.yfd.com.cn/yinger
  ````
  ### database
  ````$xslt
  console.log(api.database) --> access
  ````
  
## 4. API实例方法
  ### ajax(options);
  向服务器发起一个请求，必要参数options
  ````options配置说明
  // 默认options
   
  optons = {
      method: 'GET',          // 配置请求方法， String
      url: '',                // 配置请求地址, String
      timeout: 0,             // 配置请求超取消请求时间，单位ms，0表示不取消请求 Number
      data: {},               // 配置向服务器发送的数据, Object
      dataType: 'json',       // 配置获取的数据类型，'json'或'text', String
      async: true,            // 配置是否发起异步请求, Boolean
      user: null,             // 配置用户名, String
      password: null,         // 配置用户密码, String
      sendBefore: null,       // 配置请求发出前的回调函数, Function
      success: null,          // 配置请求成功后的回调函数, Function
      error: null,            // 配置请求出错时的回调函数, Function
      completed: null,        // 配置请求完成后的回调函数, Function
      autoCompletePath: '',   // 配置自动添加路径的字段, String
      completeRootdir: ''     // 配置自动添加路径前缀, String
  }
 ````
 
 ### getUrl(fnName)
  获取方法对应的请求地址，参数fnName可以是以下值：
  - 'getRow'
  - 'getRows'
  - 'getProvinces'
  - 'getSeo'
  - 'getAlbum'
  - 'getAddr'
  - 'postFeedback'
  - 'postEmail'
  - 'search'
  
 
  
  ### getRow(options)
  获取一行（一条记录），必要参数options
  ````$xslt
  var options = {
      data: {
          id: 214,
          title_en: 1,
          sub_title: 1,
          big_img: 1,
          video_src: 1
      },
      autoCompletePath: ['img_url', 'big_img']
  };
   
  api.getRow(options).then(function(response){
      var data = response.data;
      // to do something...
  }).catch(err){
      console.log(err);
  }
````
  
  ### getRows(options)
  获取多行（多条记录），必要参数options
  
  ### getCategory(options)
  获取某分类下的子分类，必要参数options
  
  ### getProvinces(options)
  获取省份和城市，可选参数options
  
  ### getSeo(options)
  获取省份和城市，可选参数options
  
  ### getAlbum(options)
  获取某条记录的相册，必要参数options
  
  ### getAddr(options)
  获取所有店铺地址，可选参数options
  
  ### postFeedback(options)
  提交留言反馈，必要参数options
  
  ### postEmail(options)
  邮箱订阅，必要参数options
  
  ### search(options)
  关键字查询，必要参数options
  
  
## 5. 最后我再说两句，最后两句....
  1. API实例方法中的ajax方法和getUrl方法是其他方法的底层实现，在项目中几乎用不到，但是为了各人的骚操作，我把它们暴露出来了。<br>
  2. API实例方法中除ajax和getUrl以外的方法均返回一个Promise实例，其参数options有这种操作：<br>
  当options中不存在data属性时，我认为options就是data，而当options中存在data属性时，我认为你还想配置其他属性（嗯，虽然配置了也不一定起作用），
  因为在实例化API时，假如没有禁止自动拼接路径，则默认所有方法都会自动对img_url、big_img和video_src这三个字段拼接路径，因此，其方法中除了data属性外
  就不需要配置其他属性了
  ````$xslt
  var options = {
      data: {
        id: 214,
        title_en: 1,
        sub_title: 1
      }
  };
   
  var data = {
      id: 214,
      title_en: 1,
      sub_title: 1
  };
   
  api.getRow(options).then(function(response){
      // 这里得到的结果和下面那货得到的结果是一样的
  });
   
  api.getRow(data).then(function(response){
      // 这里得到的结果和上面那货得到的结果是一样的
  });
  
  ````
    
