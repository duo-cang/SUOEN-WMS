# 索恩WMS海外仓系统简介

索恩 WMS 是专为第三方跨境电商海外仓场景设计的专业仓储管理系统，聚焦于解决海外仓运营中的订单处理、库存管控、物流协同等核心问题，通过数字化手段提升仓储作业效率与跨境供应链响应速度。 该系统覆盖海外仓全业务流程，从商品入库、库位管理、订单分拣、打包发货到库存盘点、退换货处理等环节均实现标准化管理。其核心优势在于支持多仓协同运营，可同时对接亚马逊、eBay、temu、tiktok、shopfiy、shopee等主流电商平台，以及各类 ERP 系统、物流服务商接口，实现订单自动同步、库存实时更新、物流信息追踪等一体化功能。 在功能层面，索恩 WMS 具备智能波次拣货、动态库位分配、多维度库存预警等特色功能，能有效降低人工操作误差，提高仓储空间利用率。同时，系统支持多语言、适配不同国家的税务规则与物流标准，满足全球化布局的跨境企业需求。 通过开放的 API 接口，索恩 WMS 可与企业现有业务系统无缝集成，打破数据孤岛，实现从前端销售到后端仓储的全链路可视化管理。无论是中小跨境卖家还是大型跨境电商企业，都能通过索恩 WMS 优化海外仓运营成本，提升客户履约体验。


#### 官方 API 文档及调试地址：https://api.suoen.com/api/docs/wms 

索恩 WMS API 的接口功能按业务模块分类，涵盖授权、产品管理、入库、出库、库存、基础数据及财务等核心场景，具体如下：
一、授权（Auth）接口
用于身份验证与令牌管理，确保接口访问安全：
获取 Token（POST /api/user/authorization/Token）：通过appId和appSecret获取访问令牌accessToken及刷新令牌refreshToken，作为后续接口调用的身份凭证。
刷新 Token（POST /api/user/authorization/RefreshToken）：当accessToken过期时，通过accessToken和refreshToken重新获取有效令牌，避免重复授权。
二、产品（Product）接口
用于管理商品基础信息，支持产品全生命周期数据维护：
创建产品（POST /api/user/wms/Product/Add）：添加新产品信息，包括 SKU、名称、规格（长度 / 宽度 / 高度 / 重量）、申报信息（中英文名称、海关编码、原产地）、特殊属性（是否带电池 / 液体等），支持跨境仓储所需的合规信息录入。
查询产品列表（GET /api/user/wms/Product/List）：按 SKU、名称、单位等条件查询产品列表，返回产品库存数量、状态、规格等详情，便于商品信息核对与管理。
三、入库（Inbound）接口
覆盖入库全流程操作，支持入库单的创建、取消与查询：
创建入库单（POST /api/user/wms/Inbound/Add）：提交入库请求，需指定仓库代码、入库类型（如箱装 / 托盘）、预计到达时间、运输单号及入库产品信息（箱号、SKU、数量），用于仓库提前规划收货。
取消入库单（POST /api/user/wms/Inbound/Cancel）：通过InboundId取消未完成的入库单，终止入库流程。
查询入库单列表（GET /api/user/wms/Inbound/List）：按入库单号、仓库代码、参考号等条件查询入库单状态（如草稿、在途、已收货、已上架）、产品数量、异常信息等，跟踪入库进度。
四、出库（Outbound）接口
支持出库单的创建、取消、查询及物流跟踪，覆盖订单履约全流程：
创建出库单（POST /api/user/wms/Outbound/Add）：提交出库请求，需指定仓库代码、物流服务代码、收件信息（地址、电话、国家）、出库产品（SKU、数量、箱号），生成出库单并关联物流面单。
取消出库单（POST /api/user/wms/Outbound/Cancel）：通过OutboundId和取消原因，取消未发货的出库单。
查询出库单列表（GET /api/user/wms/Outbound/List）：按出库单号、运单号、状态（如待拣货、已打包、已发货）等条件查询出库单详情，包括产品数量、物流信息、费用等。
跟踪出库物流（GET /api/user/wms/Outbound/Tracking）：通过OutboundId或TrackingNo查询物流跟踪信息，返回物流状态（如在途、派送中、已签收）及详细节点记录。
五、库存（Stock）接口
提供多维度库存查询，支持精细化库存管理：
批次库存查询（GET /api/user/wms/BatchStock/List）：按 SKU、仓库代码、批次类型（合格品 / 残次品）等条件，查询各批次库存的数量、货位、入库时间等，适合追溯特定批次库存流转。
总库存查询（GET /api/user/wms/TotalStock/List）：按 SKU、仓库代码查询总库存数据，包括合格品 / 残次品数量、可用库存、出库占用库存等汇总信息，用于全局库存监控。
六、基础（Base）接口
提供仓储与物流服务的基础数据查询，支撑业务配置：
查询仓库列表（GET /api/user/wms/Base/WarehouseList）：按仓库代码、状态（启用 / 禁用）查询可用仓库信息，返回仓库名称、代码等，用于入库 / 出库时指定仓库。
查询物流服务列表（GET /api/user/wms/Base/ShippingServiceList）：按仓库代码、物流服务代码查询支持的物流服务，返回服务名称、代码，用于出库时选择物流渠道。
七、财务（Finance）接口
用于费用账单查询，支持财务对账：
查询账单列表（GET /api/user/finance/BillList）：按账单编号、时间范围、业务类型（入库 / 出库）等条件查询费用账单，返回金额、费用类型、支付状态等，便于核对仓储及物流费用。

#### 接入准备
    
    秘钥申请： 登录客户端账号，获取appId和accessToken，如果没有需要注册 https://www.suoen.com
    授权机制： 使用appId和AppSecret兑换accessToken accessToken失效后，通过refreshToken重新获取
    请求规范： 数据格式：请求参数以 JSON 格式置于请求体中 
    请求头参数： --header 'Authorization: Bearer YOUR_SECRET_TOKEN'
