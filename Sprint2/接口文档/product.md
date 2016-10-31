###茶产品的新增(图片暂未处理)
 * URL：http://localhost:8080/api/product/new?productType_id=1&teaSeller_id=1
 * Method:POST
 * 注意事项：    
  name如果用户选择默认，可以从productType的name中获得，不能为空;   
  level 1 2 3分别对应（一般，中等，上等);    
  locality：产地 省＋市＋街道，方便后面做地图的地位使用，可以用控件，让用户选；    
  stock:库存，是double型，但前台要保证它是数字且大于0    
  price:单价，double型，前台要保证是数字且大于0    
  startNum:起售数量，double型，前台要保证是数字且大于0    
  discount：折扣，double型，前台保证是数字，且在0<discount<=1    
  isFree:是否包邮，0不包邮，1包邮 填写0时，要写上邮费       
  postage:邮费，double型，前台保证是数字且大于0    
  deleverLimit:发货的时间间隔，int型，前台保证是数字且大于0    
  unit:计数单位，可以用下拉框供用户选择    
  以上的属性都必须传递到后台，用户不填的，要给予默认值
     
 * 参数：    
  body中：
 <pre> 
 { 
    "remark":"红茶好喝有营养",
    "name":"顶级红茶",
    "level":3,
    "locality":"浙江杭州",
    "stock":100,
    "price":56,
    "startNum":1.0,
    "discount":0.8,
    "isFree":0,
    "postage":5.0,
    "deliverLimit":10,
    "unit":"斤" 
	} </pre>
 url中：  
   productType_id：茶产品类型的id；     
   teaSeller_id茶农的id    
   
* 输出：
  <pre> 
  {
  "code": 200,
  "data": {
    "id": 1,
    "productType": {
      "id": 1,
      "name": "绿茶",
      "descript": "绿茶的描述信息",
      "url": "图片地址url",
      "state": 1,
      "alive": 1
    },
    "remark": "红茶好喝有营养",
    "name": "顶级红茶",
    "level": 3,
    "locality": "浙江杭州",
    "stock": 100,
    "price": 56,
    "startNum": 1,
    "discount": 0.8,
    "isFree": 0,
    "postate": 0,
    "deliverLimit": 10,  发货时间间隔：10或者5或者其它（代表天数）
    "createDate": null,
    "unit": "斤",
    "teaSeller": {
      "id": 1,
      "name": "ycc",
      "level": 1,
      "nickname": "ycc",
      "account": {
        "id": 1,
        "tel": "15821432414",
        "password": "123",
        "label": 0,
        "alive": 1
      },
      "address": "上海市闵行区",
      "tel": "15832341341413",
      "headUrl": "url",
      "money": 100,
      "licenseUrl": "licenseurl",
      "zip": "2341341",
      "idCard": "423432543254523",
      "alive": 1
    },
    "state": 0,
    "alive": 1
  }
}</pre>

### 茶产品的批量修改
* URL:http://localhost:8080/api/product/update
* Method:POST
* 注意事项：    
只能对stock,price,startNum,discount,isFree,postage,deliverLimit,unit）进行修改，其它不能进行修改。前台必须传的数据是id和修改的字段，未修改的，可以不传。但是仍然要保证数据格式的正确性。
* 参数：
 <pre>
[
{
    "id":1,（必须传）
    "stock":100,（可以不传）
    "price":10,（同上）
    "startNum":5,（同上）
    "discount":0.8（同上）
}
]
</pre>
* 返回值：
 <pre>
{
  "code": 200,
  "data": "all succeed"
}
</pre>
###茶产品的批量上架
* URL:http://localhost:8080/api/product/startSell
* Method:POST
* 注意事项：
只需要传入需要上架的商品id即可，可以进行上架的产品是存在且未上架的产品
* 参数：
 <pre>
[
    {
        "id":4
    }
]
</pre>
* 输出：
 <pre>
{
  "code": 200,
  "data": "all succeed"
}
</pre>
### 茶产品的多条件组合查询
* URL:http://localhost:8080/api/product/search 
* Method:POST
* 注意事项：这个可以输入的条件很多，所有的条件都可以不传或者数字传－1，字符传“”。 对于字符串都是进行模糊匹配   
  productType_id：茶产品类型的id，不需要该条件时可以不传或者传－1； 
  remark：描述信息，name：茶的名字，level：等级1，2，3；locality：产地；    
  isFree：是否包邮, teaSeller_name：茶农的名字，state：产品状态（0未上架  1上架），    
  stock：库存,查找库存大于stock的产品， lowPrice：低单价，查找大于lowPrice的产品，highPrice: 高单价，查找highPrice的产品，startNum：起售数量，查找大于startNum的产品，  discount：折扣，查找折扣力度大于disCount，输入0.8，则查找disCount<=0.8
  （pageIndex，pageSize,sortField,sortOrder）后面四个为分页参数，可以不写
* 参数：在注意事项中，提到的都可以写
* 输入：
 <pre>
{
  "content": [
    {
      "id": 4,
      "productType": {
        "id": 1,
        "name": "绿茶",
        "descript": "绿茶的描述信息",
        "url": "图片地址url",
        "state": 1,
        "alive": 1
      },
      "remark": "红茶好喝有营养",
      "name": "顶级红茶",
      "level": 3,
      "locality": "浙江杭州",
      "stock": 1000,
      "price": 100,
      "startNum": 5,
      "discount": 0.8,
      "isFree": 1,
      "postate": 0,
      "deliverLimit": 10,
      "createDate": "2016-10-31",
      "unit": "斤",
      "teaSeller": {
        "id": 1,
        "name": "ycc",
        "level": 1,
        "nickname": "ycc",
        "account": {
          "id": 1,
          "tel": "15821432414",
          "password": "123",
          "label": 0,
          "alive": 1
        },
        "address": "上海市闵行区",
        "tel": "15832341341413",
        "headUrl": "url",
        "money": 100,
        "licenseUrl": "licenseurl",
        "zip": "2341341",
        "idCard": "423432543254523",
        "alive": 1
      },
      "state": 1,
      "alive": 1
    }
  ],
  "totalElements": 1,
  "totalPages": 1,
  "last": true,
  "size": 10,
  "number": 0,
  "sort": [
    {
      "direction": "ASC",
      "property": "price",
      "ignoreCase": false,
      "nullHandling": "NATIVE",
      "ascending": true
    }
  ],
  "first": true,
  "numberOfElements": 1
}
</pre>