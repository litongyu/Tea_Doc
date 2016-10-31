###1.产品类型的新增或修改：
* url: http://localhost:8080/api/productType/newOrUpdate 
* Method:POST
* 参数：在body里
* 新增：
   <pre>
    [
        {
        "name":"红茶1",
        "descript":"红茶的描述信息",
        "url":"图片地址url1"
        }
    ]
</pre>
* 修改
	<pre>
	[
        {
        “id”:1,
        "name":"红茶1",
        "descript":"红茶的描述信息",
        "url":"图片地址url1"
        }
    ]
	</pre>
* 返回
	<pre>{
 	 "code": 200,
  	 "data": "all succeed"
	}
	</pre>
####2.茶产品类型的查询
* url: http://localhost:8080/api/productType/getAllProductType?state=1
* Method:POST
* 参数：在url上
state =1 获得所有可以使用的茶产品
state＝0获得所有不能使用的茶产品
* 返回：
 <pre>
{
	  "code": 200,
	  "data": [
    {
      "id": 1,
      "name": "红茶",
      "descript": "红茶的描述信息",
      "url": "图片地址url",
      "state": 1,
      "alive": 1
    },
    {
      "id": 2,
      "name": "绿茶",
      "descript": "绿茶的描述信息",
      "url": "图片地址url",
      "state": 1,
      "alive": 1
    }
  	]
	}
</pre>
