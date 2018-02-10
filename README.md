# YuFei Design Front-end API


## 1. 如何使用

> tips: api.js中使用到了IE9不兼容的Promise，为了兼容IE9，须先引入promise.js

````
<script src="api/promise.js"></script>
<script src="api/api.js"></script>
<script>
 
  var api = new API(options);
  console.log('api: %o', api);
  
</script>
 
</body>
````

## 2. API配置项(options)
  ### rootdir
  配置网站根目录地址，默认值：''
  
  ### database
  配置网站所使用的数据库，默认值：'access'

  ### autoCompletePath
  配置需要自动拼接路径的字段，当读取该字段时，自动为后台返回的数据拼接路径，默认值：['img_url', 'big_img', 'video_src']
  > 当只有一个字段时，可直接写字段名，当有多个字段时为一个数组，如：
  只需要拼接img_url字段： autoCompletePath: 'img_url'
  需要多个字段： autoCompletePath: ['img_url', 'big_img', 'video_src']

