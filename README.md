# 海外仓系统-索恩WMS-API

索恩 WMS API 为海外仓系统提供了标准化的数据交互接口，支持与电商平台、ERP 系统、物流服务商等外部系统进行对接，实现订单管理、库存控制、物流跟踪等核心业务的自动化处理。通过该 API，企业可高效整合海外仓资源，提升跨境电商运营效率。


#### 官方 API 文档及调试地址：https://api.suoen.com/api/docs/wms 核心功能接口分类

    订单管理接口
    库存管理接口
    物流对接接口
    基础数据接口

#### 接入准备

    秘钥申请 注册客户端账号，获取appId和accessToken

    授权机制 使用appId和AppSecret兑换accessToken accessToken失效后，通过refreshToken重新获取

    请求规范 数据格式：请求参数以 JSON 格式置于请求体中 请求头参数： --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
