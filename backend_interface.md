# 后台服务器接口文档
## 说明
服务器提供基于HTTP协议的访问请求，报文内容编码均为UFT-8，报文格式为json字符串。分别提供了人脸注册、人脸验证两种种方法。所有输入参数都不允许缺省。所有的请求返回状态体现在http返回码中，不在返回数据中额外提供字段。  
  
  
## 人脸注册
方法名：addFace
简述：用于将一张新的人脸照片注册到后台数据库
URL：http://{ip地址}:{端口号}/faceService/addFaces
提交方式：POST
输入参数：
参数名称 | 类型 | 说明  
-|-|---
uid | String | 用户的id账号
uid_type | String | 用户id的类型，有身份证号、工号等
name | String | 用户名字
channel | String | 上传渠道，有微信小程序、安卓、ios等
img | String | 图片采用Base64编码后的字符串  
返回参数：
参数名称 | 类型 | 说明  
-|-|---
code | Integer | 若code为0表示操作成功，否则操作失败，含义详见错误码定义
message | String | 系统返回的信息
  

## 人脸验证
方法名：checkPerson
简述：将上传的人脸与已注册的人脸进行比对，返回比对结果
URL：http://{ip地址}:{端口号}/faceService/checkPerson
提交方式：POST
输入参数：
参数名称 | 类型 | 说明  
-|-|---
uid | String | 用户的id账号
uid_type | String | 用户id的类型，有身份证号、工号等
name | String | 用户名字
channel | String | 上传渠道，有微信小程序、安卓、ios等
img | String | 图片采用Base64编码后的字符串
返回参数
-|-|---
code | Integer | 若code为0表示操作成功，否则操作失败，含义详见错误码定义
message | String | 系统返回的信息
sim | float | 相似度，区间为0-1，越接近1，相似度越高
uid_type | String | 比对结果，’1’表示通过，’0’表示验证失败
imgFlowNo | String | 对比记录的流水号
  
  
## 错误码定义
**该错误码参考了HTTP状态码设计规范，但与HTTP协议本身返回的状态码并没有关联。**

错误码 | 含义
-|----
400 | 请求输入参数中，有缺失参数
405 | 找不到对应的处理方法
410 | 上传的图片中找不到人脸
401 | 用户在提交人脸验证请求时，还未注册过人脸
409 | 用户在提交人脸注册请求时，已经注册过人脸了