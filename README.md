mygallery
=========

1 界面
  按照要求为保持外观一致,直接使用Firefox查看示例页面结构,分析引用的CSS
  发现3个文件与此页面相关(framework.css,liulan.css,page.css),下载后并格式化.
  观察DOM结构,动态加载图片的结构如下红框所示.
  
  #imgs_container下的每一个ul即为一列图片展示.
  使用handlebars将每一个ul结构处理成模板文件.(代码参见myGallery.js)


2 基础lib库(js/lib)
  jQuery.1.9.1.js (主要是屏蔽浏览器差异,好用的DOM选择器)
  seajs.js (模块化处理)
  handlebars.js (语法与mustache一致,但性能要好)
  backbone.js(备用,前端的MVC处理)
  
3  插件(js/plugin)
  jquery.lazyload.min.js     (图片延时加载)
  mediaqueries.js  (对于不支持CSS3的浏览器使用该库实现media queries)
  

4 后台两个接口(php/myGallery.php):
  1 getPics   (首次返回30个结果,2个参数page,pagesize=30)    
   返回结果如下:
   {
  "errNo":0,
	"msg":"OK",
	"tag1" : "美女",
	"tag2" : "全部",
	"totalNum" : 98854,
	"start_index" : 0,
	"return_number" : 30,
	"data" : [{
			"id" : "9220203856802541257",
			"pn" : 1,
			"tags" : "美空",
			"image_url" : "xxx",
			"image_width" : 575,
			"image_height" : 848,
			"thumbnail_url" : "xxx",
			"thumbnail_width" : 230,
			"thumbnail_height" : 339,
			"thumb_large_width" : 310,
			"thumb_large_height" : 457,
			"thumb_large_url" : "xxx",
			"site_name" : "",
			"site_logo" : "",
			"site_url" : "http://www.yjz9.com",
			"from_url" : "http://www.yjz9.com/show_news.asp?id=7207",
			"obj_url" : "http://www.yjz9.com/upload/20122/120301bxg11.jpg",
			"download_num" : 0,
			"start_index" : 0,
			"return_number" : 30,
			"album_di" : "",
			"can_album_id" : "",
			"album_obj_num" : "0"
		}]}
    具体参见(js/json/data.js)


  
  2 searchPics  (根据输入的标签结果,返回查询后的数据,JSON格式)  
   返回结果如下:
   与上个接口相同,具体参见(js/json/data_search.js)
   
  
  
5 移动设备的支持
   使用mediaqueries实现响应式布局.
   
    Meta设置:
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   
   
   使用Media Queries为移动设备指定不同的CSS:
    /*Ipad*/
   <link rel="stylesheet" media="media screen and (max-device-width: 1024px)"  type="text/css"  href="ipad/ipad.css"> 


   /*其他分辨率设备,480px*/
   <link rel="stylesheet" media="media screen and (max-device-width: 480px)" type="text/css" href="mobile/mobilecss" />


   使用display:box布局
   #imgs_container{display:box   /*各核心浏览器私有写法*/}
   #imgs_container ul{box-flex:1  /*各核心浏览器私有写法*/}
