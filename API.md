# 1dong接口文档  

## 正式 http://118.31.78.209:8190

## 测试 http://47.111.66.51:9190

### 默认get请求,有json格式说明的post请求

[toc]



### 1功能 ：知识点导出

#### 请求方法：  /md/knowledge/exportExcel

#### 参数说明：

| 字段          | 类型    | 是否必填 | 描述及要求           |
| ------------- | ------- | -------- | -------------------- |
| startTime     | String  | 选填     | 开始时间             |
| endTime       | String  | 选填     | 结束时间             |
| type          | String  | 选填     | 知识点类型名称       |
| loadPerson    | String  | 选填     | 录入人员             |
| text          | String  | 选填     | 知识点               |
| recommendType | boolean | 选填     | 是否加入推荐类型筛选 |
| anaPerson     | boolean | 选填     | 是否加入解析人筛选   |

**Success**

```file
1懂20180822025220.xls
```

### 2功能 ：知识点导入

#### 2请求方法：/md/knowledge/importExcel

#### 2参数说明：

| 字段         | 类型   | 是否必填 | 描述及要求    |
| ---------- | ---- | ---- | -------- |
| tablesfile | File | 必填   | 导入的excel |

**Success**

```json
{
    "data": true,
    "message": "Success",
    "status": 0
}
```

### 3功能 ：导入模板下载

#### 请求方法：post  /md/upload/知识点录入模版.xlsx

**Success**

```json
知识点录入模版.xlsx
```



### 4功能 ：查询知识点类型

#### 请求方法：  /md/knowledge/selectType

#### 返回值说明：

| 字段   | 类型     | 描述        |
| ---- | ------ | --------- |
| kid  | String | 知识点类型自增id |
| type | String | 知识点类型     |

**Success**

```
[
    {
        "kid": "1",
        "type": "同义词"
    },
    {
        "kid": "2",
        "type": "人员职务"
    },
    {
        "kid": "3",
        "type": "工作职责"
    },
    {
        "kid": "4",
        "type": "未知"
    }
]
```



### 5功能 ：插入知识点文本

#### 请求方法：/md/knowledge/insert

#### 参数说明：json格式

| 字段      | 类型   | 是否必填 | 描述及要求             |
| --------- | ------ | -------- | ---------------------- |
| text      | String | 必填     | 文本                   |
| orgBsList | list   | 选填     | 适用范围插件选择后的值 |

```json
{"text":"测试1懂接口1","orgBsList": [
        {
            "businessId": "708153328107225372",
            "organizationId": "706153338148840508",
            "areaTypeId": 2,
            "areaTypeName": "具体范围",
            "organizationName": "4448",
            "businessName": "的富兰克林",
            "activeFlag": {
                "isBOActive": false,
                "isScopeActive": false
            }
        }
    ]}
```

#### 返回值说明：

| 字段      | 类型      | 描述    |
| ------- | ------- | ----- |
| data    | boolean | 数据    |
| message | String  | 返回值信息 |
| status  | int     | 返回值状态 |

**Success**

```
{
    "data": true,
    "message": "Success",
    "status": 0
}
```

### 6功能 ：查询知识点列表

#### 请求方法：  /md/knowledge/selectKnowInfo

#### 参数说明：

| 字段           | 类型    | 是否必填 | 描述及要求                                               |
| -------------- | ------- | -------- | -------------------------------------------------------- |
| startTime      | String  | 选填     | 开始时间                                                 |
| endTime        | String  | 选填     | 结束时间                                                 |
| type           | String  | 选填     | 知识点类型名称                                           |
| loadPerson     | String  | 选填     | 录入人员                                                 |
| num            | int     | 必填     | 一页显示的数量                                           |
| pageNumber     | int     | 必填     | 页数                                                     |
| text           | String  | 选填     | 知识点                                                   |
| recommendType  | boolean | 必填     | 是否包含推荐类型                                         |
| anaPerson      | boolean | 必填     | 是否包含解析人员                                         |
| is_file        | boolean | 必填     | 是否归档 归档填true未归档填false                         |
| is_deleted     | boolean | 必填     | 是否删除（归档未归档填false，回收站填true）不填默认false |
| areaTypeId     | int     | 选填     | 1：通用范围，2：组织范围，3：业务范围，4：组织业务范围   |
| organizationId | int     | 选填     | 组织id                                                   |
| businessId     | int     | 选填     | 业务id                                                   |

#### 返回值说明：

| 字段       | 类型    | 描述               |
| ---------- | ------- | ------------------ |
| data       | object  | 数据               |
| message    | String  | 返回值信息         |
| status     | int     | 返回值状态         |
| totalRow   | int     | 全部条数           |
| pageNumber | int     | 当前页数           |
| lastPage   | boolean | 是否是最后一页     |
| totalPage  | int     | 全部页数           |
| pageSize   | int     | 一页条数           |
| list       |         |                    |
| ldate      | String  | 录入时间           |
| loadPerson | String  | 录入人员           |
| from       | String  | 来源               |
| kiId       | String  | 录入信息id         |
| text       | String  | 知识点文本         |
| type       | String  | 知识点类型名称     |
| from_msg   | String  | 知识点来源详情信息 |
| from_time  | String  | 知识点来源详情时间 |
| recommend  | String  | 推荐类型           |
| ana_name   | String  | 解析人             |
| keyword    | String  | 推荐和疑似         |
| citation   | int     | 引用量             |

**Success**

```json
{
    "data": {
        "totalRow": 187,
        "pageNumber": 2,
        "lastPage": false,
        "firstPage": false,
        "totalPage": 19,
        "pageSize": 10,
        "list": [
            {
                "gmt_create": "2020-05-07 16:21:35",
                "ana_name": "詹子恒",
                "citation": 0,
                "loadPerson": "詹子恒",
                "recommend": "",
                "kiId": "1258204111954771984",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|测试业务|",
                "from_msg": "2020-05-07 16:21:34",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:计算机=电脑",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 507140511197407662,
                        "businessName": "下城专属业务|下城行政服务|测试业务|"
                    }
                ]
            },
            {
                "gmt_create": "2020-05-07 16:16:20",
                "ana_name": "詹子恒",
                "citation": 0,
                "loadPerson": "詹子恒",
                "recommend": "",
                "kiId": "1258204111954771983",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|",
                "from_msg": "2020-05-07 16:16:19",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:heihei=234",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 113174452377721791,
                        "businessName": "下城专属业务|下城行政服务|"
                    }
                ]
            },
            {
                "gmt_create": "2020-05-07 16:16:03",
                "ana_name": "詹子恒",
                "citation": 0,
                "loadPerson": "詹子恒",
                "recommend": "",
                "kiId": "1258204111954771982",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|测试业务|",
                "from_msg": "2020-05-07 16:16:02",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:123=12313",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 507140511197407662,
                        "businessName": "下城专属业务|下城行政服务|测试业务|"
                    }
                ]
            },
            {
                "gmt_create": "2020-05-07 16:06:41",
                "ana_name": "詹子恒",
                "citation": 0,
                "loadPerson": "詹子恒",
                "recommend": "",
                "kiId": "1258204111954771981",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|测试业务|",
                "from_msg": "2020-05-07 16:06:40",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:123=12313",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 507140511197407662,
                        "businessName": "下城专属业务|下城行政服务|测试业务|"
                    }
                ]
            },
            {
                "gmt_create": "2020-05-07 15:48:48",
                "ana_name": "詹子恒",
                "citation": 0,
                "loadPerson": "詹子恒",
                "recommend": "",
                "kiId": "1258204111954771980",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|测试业务|",
                "from_msg": "2020-05-07 15:48:47",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:123=123",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 507140511197407662,
                        "businessName": "下城专属业务|下城行政服务|测试业务|"
                    }
                ]
            },
            {
                "gmt_create": "2020-05-07 14:03:32",
                "ana_name": "吴晗践",
                "citation": 0,
                "loadPerson": "吴晗践",
                "recommend": "",
                "kiId": "1258204111954771979",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|交通运管业务|",
                "from_msg": "2020-05-07 14:03:32",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:123r4=123456",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 113174607156277624,
                        "businessName": "下城专属业务|下城行政服务|交通运管业务|"
                    }
                ]
            },
            {
                "gmt_create": "2020-05-07 13:55:03",
                "ana_name": "詹子恒",
                "citation": 0,
                "loadPerson": "詹子恒",
                "recommend": "",
                "kiId": "1258204111954771978",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|医疗卫生业务|",
                "from_msg": "2020-05-07 13:55:03",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:123456=123",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 113174607109283124,
                        "businessName": "下城专属业务|下城行政服务|医疗卫生业务|"
                    }
                ]
            },
            {
                "gmt_create": "2020-05-07 11:36:43",
                "ana_name": "詹子恒",
                "citation": 0,
                "loadPerson": "詹子恒",
                "recommend": "",
                "kiId": "1258204111954771977",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|医疗卫生业务|",
                "from_msg": "2020-05-07 11:36:43",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:frgt=123",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 113174607109283124,
                        "businessName": "下城专属业务|下城行政服务|医疗卫生业务|"
                    }
                ]
            },
            {
                "gmt_create": "2020-05-07 11:32:55",
                "ana_name": "詹子恒",
                "citation": 0,
                "loadPerson": "詹子恒",
                "recommend": "",
                "kiId": "1258204111954771976",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|医疗卫生业务|",
                "from_msg": "2020-05-07 11:32:54",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:123456=123456",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 113174607109283124,
                        "businessName": "下城专属业务|下城行政服务|医疗卫生业务|"
                    }
                ]
            },
            {
                "gmt_create": "2020-05-07 11:29:49",
                "ana_name": "詹子恒",
                "citation": 0,
                "loadPerson": "詹子恒",
                "recommend": "",
                "kiId": "1258204111954771975",
                "type": "同义词",
                "from_time": null,
                "orgBsText": "业务范围-下城专属业务|下城行政服务|医疗卫生业务|",
                "from_msg": "2020-05-07 11:29:48",
                "ldate": "2020-05-07",
                "from": "手动录入",
                "text": "同义词:服务语义库:123=123456",
                "keyword": "",
                "orgBsList": [
                    {
                        "organizationId": null,
                        "areaTypeName": "业务范围",
                        "organizationName": "",
                        "areaTypeId": 3,
                        "businessId": 113174607109283124,
                        "businessName": "下城专属业务|下城行政服务|医疗卫生业务|"
                    }
                ]
            }
        ]
    },
    "message": "Success",
    "status": 0
}
```

### 7功能 ：查询知识点录入人员

#### 请求方法：  /md/knowledge/selectLoadPerson

#### 返回值说明：

| 字段         | 类型     | 描述   |
| ---------- | ------ | ---- |
| loadPerson | String | 录入人员 |

**Success**

```
{
    "data": [
       
        {
            "loadPerson": "陈清清"
        },
        {
            "loadPerson": "陈福威"
        },
        {
            "loadPerson": "陈鹏程"
        },
        {
            "loadPerson": "高天宇"
        },
        {
            "loadPerson": "高楠"
        }
    ],
    "message": "Success",
    "status": 0
}
```

### 8功能 ：修改知识点录入信息

#### 请求方法：/md/knowledge/update

#### 参数说明：json格式

| 字段         | 类型     | 是否必填 | 描述及要求   |
| ---------- | ------ | ---- | ------- |
| kiId       | String | 必填   | 录入信息id  |
| kid        | String | 选填   | 知识点类型id |
| type       | String | 选填   | 知识点类型名称 |
| loadPerson | String | 必填   | 录入人员    |
| text       | String | 必填   | 知识点文本   |

```json
{
    "kiId": "1032453800973041665",
    "kid": "1",
    "type": "[同义词]",
    "text": "测试1懂接口1",
    "loadPerson": "陈清清66666666666666666666666666666663"
}
```

#### 返回值说明：

| 字段      | 类型      | 描述    |
| ------- | ------- | ----- |
| data    | boolean | 数据    |
| message | String  | 返回值信息 |
| status  | int     | 返回值状态 |

**Success**

```
{
    "data": true,
    "message": "Success",
    "status": 0
}
```

### 9功能 ：插入/修改解析后的知识点

#### 请求方法：  /md/knowledge/update

#### 参数说明：

| 字段     | 类型     | 是否必填 | 描述及要求   |
| ------ | ------ | ---- | ------- |
| kiId   | String | 必填   | 录入信息id  |
| kid    | String | 选填   | 知识点类型id |
| detail | String | 选填   | 知识点     |

```
table: [{"kid":"1","detail":"人名属于信息中心"},{"kid":"2","detail":"A=B"}]
kiId: 2
```



#### 返回值说明：

| 字段      | 类型      | 描述    |
| ------- | ------- | ----- |
| data    | boolean | 数据    |
| message | String  | 返回值信息 |
| status  | int     | 返回值状态 |

**Success**

```json
{data: "解析成功!", message: "Success", status: 0}
```

### 10功能 ：删除知识点（在回收站里点击移出垃圾箱至未归档还是调用该接口）

#### 请求方法：  /md/knowledge/delete

#### 参数说明：

| 字段   | 类型     | 是否必填 | 描述及要求  |
| ---- | ------ | ---- | ------ |
| kiId | String | 必填   | 录入信息id |

#### 返回值说明：

| 字段    | 类型    | 描述                                     |
| ------- | ------- | ---------------------------------------- |
| data    | boolean | 数据(1表示删除成功，0表示移出回收站成功) |
| message | String  | 返回值信息                               |
| status  | int     | 返回值状态                               |

**Success**

```json
{
    "data": true,
    "message": "Success",
    "status": 0
}
```

###  11功能 ：登入

#### 请求方法：  /md/login

#### 参数说明：

| 字段    | 类型   | 是否必填 | 描述及要求          |
| ------- | ------ | -------- | ------------------- |
| appName | String | 必填     | 账号                |
| token   | String | 必填     | 单点登入获得的token |

#### 返回值说明：

| 字段     | 类型   | 描述       |
| -------- | ------ | ---------- |
| data     | object | 数据       |
| message  | String | 返回值信息 |
| status   | int    | 返回值状态 |
| appName  | String | 账号       |
| userId   | String | 用户id     |
| userName | String | 用户名     |
| role     | list   | 权限       |
| roleName | list   | 权限名称   |

**Success**

```json
{
    "data": {
        "role": {
            "dong_fcbq_bqkgl": false,
            "dong_fcbq_bq_fcgl": false,
            "dong_zslx_lxsxdy": false,
            "dong_zslx_hsz": false,
            "dong_fcbq_cdgl_ck": false,
            "dong_fcbq_bqkgl_xz": false,
            "dong_syfw_xg": true,
            "dong_zsdgl_gd": false,
            "dong_zslx_lxgndy_gd": false,
            "dong_zslx_lxgndy_sc": false,
            "dong_zsdgl_xg": false,
            "dong_fcbq_cdgl_xg": false,
            "dong_sz": false,
            "dong_zslx_lxsxdy_ck": false,
            "dong_fcbq_bqkgl_xg": false,
            "dong_zsdgl_ck": false,
            "dong_fcbq_cdgl": false,
            "dong_fcbq_bq_fcgl_xg": false,
            "dong_zslx_lxsxdy_xg": false,
            "dong_fcbq": false,
            "dong_zslx_lxgndy_xz": false,
            "dong_fcbq_cdgl_xz": false,
            "dong_zslx": false,
            "dong_zsdgl_hsz": false,
            "dong_zsdgl_xz": false,
            "dong_fcbq_bq_fcgl_xz": false,
            "dong_sz_qxgl": false,
            "dong_fcbq_bqkgl_ck": false,
            "dong_sz_czjl": false,
            "dong_syfw": true,
            "dong_syfw_sc": true,
            "dong_zsdgl_hb": false,
            "dong_zsdgl_sc": false,
            "dong_zsdgl_jx": false,
            "dong_fcbq_cdgl_sc": false,
            "dong_fcbq_bqkgl_sc": false,
            "dong_zslx_lxgndy_ck": false,
            "dong_zslx_lxgndy": false,
            "dong_fcbq_bq_fcgl_sc": false,
            "dong_zsdgl": false,
            "dong_zslx_lxgndy_xg": false,
            "dong_syfw_xz": true
        },
        "appName": "fangshengqun",
        "roleName": {
            "dong_fcbq_bqkgl": "分词标签-标签库管理",
            "dong_fcbq_bq_fcgl": "分词标签-标签/分词管理",
            "dong_zslx_lxsxdy": "知识类型-类型实现定义",
            "dong_zslx_hsz": "知识类型-回收站",
            "dong_fcbq_cdgl_ck": "词典管理-查看",
            "dong_fcbq_bqkgl_xz": "标签库管理-新增",
            "dong_syfw_xg": "适用范围-修改",
            "dong_zsdgl_gd": "知识点管理-归档",
            "dong_zslx_lxgndy_gd": "类型概念定义-归档",
            "dong_zslx_lxgndy_sc": "类型概念定义-删除",
            "dong_zsdgl_xg": "知识点管理-修改",
            "dong_fcbq_cdgl_xg": "词典管理-修改",
            "dong_sz": "null-设置",
            "dong_zslx_lxsxdy_ck": "类型实现定义-查看",
            "dong_fcbq_bqkgl_xg": "标签库管理-修改",
            "dong_zsdgl_ck": "知识点管理-查看",
            "dong_fcbq_cdgl": "分词标签-词典管理",
            "dong_fcbq_bq_fcgl_xg": "标签/分词管理-修改",
            "dong_zslx_lxsxdy_xg": "类型实现定义-修改",
            "dong_fcbq": "null-分词标签",
            "dong_zslx_lxgndy_xz": "类型概念定义-新增",
            "dong_fcbq_cdgl_xz": "词典管理-新增",
            "dong_zslx": "null-知识类型",
            "dong_zsdgl_hsz": "知识点管理-回收站",
            "dong_zsdgl_xz": "知识点管理-新增",
            "dong_fcbq_bq_fcgl_xz": "标签/分词管理-新增",
            "dong_sz_qxgl": "设置-权限管理",
            "dong_fcbq_bqkgl_ck": "标签库管理-查看",
            "dong_sz_czjl": "设置-操作记录",
            "dong_syfw": "null-适用范围",
            "dong_syfw_sc": "适用范围-删除",
            "dong_zsdgl_hb": "知识点管理-合并",
            "dong_zsdgl_sc": "知识点管理-删除",
            "dong_zsdgl_jx": "知识点管理-解析",
            "dong_fcbq_cdgl_sc": "词典管理-删除",
            "dong_fcbq_bqkgl_sc": "标签库管理-删除",
            "dong_zslx_lxgndy_ck": "类型概念定义-查看",
            "dong_zslx_lxgndy": "知识类型-类型概念定义",
            "dong_fcbq_bq_fcgl_sc": "标签/分词管理-删除",
            "dong_zsdgl": "null-知识点管理",
            "dong_zslx_lxgndy_xg": "类型概念定义-修改",
            "dong_syfw_xz": "适用范围-新增"
        },
        "userName": "方升群",
        "userId": "20180905201255956-DD64-A3C7D971F"
    },
    "message": "Success",
    "status": 0
}
```

###  12功能 ：查询一条知识点信息

#### 请求方法：    /md/knowledge/selectOneKnowledgeinfo

#### 参数说明：

| 字段   | 类型     | 是否必填 | 描述及要求  |
| ---- | ------ | ---- | ------ |
| kiId | String | 必填   | 录入信息id |

#### 返回值说明：

| 字段         | 类型   | 描述           |
| ------------ | ------ | -------------- |
| data         | object | 数据           |
| message      | String | 返回值信息     |
| status       | int    | 返回值状态     |
| gmt_create   | String | 主动创建时间   |
| loadPerson   | String | 录入人员       |
| from         | String | 来源           |
| kiId         | String | 录入信息id     |
| text         | String | 知识点文本     |
| type         | String | 知识点类型名称 |
| fromMessage  | String | 来源详情       |
| recommend    | String | 推荐类型       |
|              |        |                |
| list         | list   | 解析后的知识点 |
| gmt_create   | String | 主动创建时间   |
| ana_name     | String | 解析人         |
| kdid         | String | 详情id         |
| details      | String | 详情           |
| type         | String | 知识点类型     |
| typeDescribe | String | 知识类型描述   |

**Success**

```json
{
    "data": {
        "gmt_create": "2020-07-10 10:16:41",
        "is_file": true,
        "loadPerson": "吴晗践",
        "recommend": "",
        "from": "手动录入",
        "kiId": 1281409547835015170,
        "text": "同义词:[上下文]:SSW=智鹏瑞尔软件（杭州）有限公司",
        "type": "代称|同义词",
        "list": [
            {
                "gmt_create": "2020-07-10 10:36:49",
                "ana_name": "吴晗践",
                "kdid": 9507,
                "typeDescribe": "同义词:[上下文]:[源词]=[同义词]",
                "details": "同义词:[上下文]:SSW=智鹏瑞尔软件（杭州）有限公司",
                "type": "同义词"
            },
            {
                "gmt_create": "2020-07-10 10:38:03",
                "ana_name": "吴晗践",
                "kdid": 9508,
                "typeDescribe": "同义词:[上下文]:[源词]=[同义词]",
                "details": "同义词:[上下文]:智鹏瑞尔=智鹏瑞尔软件（杭州）有限公司",
                "type": "同义词"
            },
            {
                "gmt_create": "2020-07-10 10:38:47",
                "ana_name": "吴晗践",
                "kdid": 9509,
                "typeDescribe": "代称:[上下文]:[代称词]=[实例词]",
                "details": "代称:[上下文]:SSW=智鹏瑞尔软件（杭州）有限公司",
                "type": "代称"
            },
            {
                "gmt_create": "2020-07-10 10:43:38",
                "ana_name": "吴晗践",
                "kdid": 9511,
                "typeDescribe": "代称:[上下文]:[代称词]=[实例词]",
                "details": "代称:[上下文]:智鹏瑞尔=智鹏瑞尔软件（杭州）有限公司",
                "type": "代称"
            }
        ],
        "fromMessage": "2020-07-10 10:16:40"
    },
    "message": "Success",
    "status": 0
}
```

###  15功能 ：来源详情内容

#### 请求方法：  /md/knowledge/getMessage

#### 参数说明：

| 字段   | 类型     | 是否必填 | 描述及要求  |
| ---- | ------ | ---- | ------ |
| kiId | String | 必填   | 录入信息id |

#### 返回值说明：

| 字段      | 类型     | 描述    |
| ------- | ------ | ----- |
| data    | object | 数据    |
| message | String | 返回值信息 |
| status  | int    | 返回值状态 |

**Success**

```json
{
    "data": "详细了解了一下鹭栖在省政府的项目，原来想简单了，其实并没有那么容易脱开，西门回来还是主要为省政府做支撑，争夺开发资源的斗争依然强烈。目前有三项开发内容一项日常运维，这两天还在运作一个新的项目，和金加和主任的对接。\r\n",
    "message": "Success",
    "status": 0
}
```

###  16功能 ：分页查询类型概念定义

#### 请求方法：  /md/type/selectType

#### 参数说明：

| 字段       | 类型    | 是否必填 | 描述及要求                            |
| ---------- | ------- | -------- | ------------------------------------- |
| pageNumber | int     | 必填     | 页码                                  |
| is_deleted | boolean | 必填     | 是否删除，不填默认false，回收站填true |

#### 返回值说明：

| 字段          | 类型    | 描述               |
| ------------- | ------- | ------------------ |
| data          | object  | 数据               |
| message       | String  | 返回值信息         |
| status        | int     | 返回值状态         |
| totalRow      | int     | 全部条数           |
| pageNumber    | int     | 当前页数           |
| lastPage      | boolean | 是否是最后一页     |
| firstPage     | boolean | 是否是第一页       |
| totalPage     | int     | 全部页数           |
| pageSize      | int     | 一页条数           |
| list          |         |                    |
| typeDescribe  | String  | 知识类型描述       |
| kid           | String  | 知识点类型表主键id |
| typeName      | String  | 知识类型名称       |
| isPersistence | boolean | 是否持久化         |

**Success**

```json
{
    "data": {
        "totalRow": 8,
        "pageNumber": 1,
        "lastPage": true,
        "firstPage": true,
        "totalPage": 1,
        "pageSize": 10,
        "list": [
            {
                "typeDescribe": "[事项名称]==办理条件==[办理条件] ==政策依据==[政策依据]==办理地点== [办理地点]==咨询方式==[咨询方式]==办理材料==[办理材料]==办理流程==[办理流程]  or  ==办理条件==[办理条件] ==政策依据==[政策依据]==办理地点== [办理地点]==咨询方式==[咨询方式]==办理材料==[办理材料]==办理流程==[办理流程]",
                "kid": "135870130428051456",
                "typeName": "行政服务事项",
                "id": 331,
                "isPersistence": false
            },
            {
                "typeDescribe": "bug:[问题描述]  or  bug:[问题描述]  or  Bug:[问题描述]  or  问题:[问题描述]",
                "kid": "5",
                "typeName": "bug",
                "id": 324,
                "isPersistence": false
            },
            {
                "typeDescribe": "评价:[被评对象],[评语]  or  评价:[评语]  or  评价:[评语]",
                "kid": "10",
                "typeName": "评价",
                "id": 318,
                "isPersistence": false
            },
            {
                "typeDescribe": "人员:[姓名]，[工作单位及职务]，联系电话[联系电话]  or  人员:[姓名],[工作单位及职务],联系电话[联系电话]  or  人员:[姓名],[工作单位],[备注说明]  or  人员:[姓名],[电话],[工作单位及职务]  or  人员:[姓名]([电话])[备注说明]  or  人员信息:[姓名]的[属性]是[值]  or  人员信息:[姓名]的[属性]好象是[值]  or  人员:[姓名]的[属性]是[值]  or  人员:[姓名],[工作单位],[联系电话]",
                "kid": "117363735932174336",
                "typeName": "人员信息",
                "id": 315,
                "isPersistence": false
            },
            {
                "typeDescribe": "催办次数[催办次数]  or  内容[上下文]包含[内容]的[下文]  or  内容[上下文]包含[内容]  or  内容[上下文]有[内容]  or  [上文催办人[中文]有[催办人]  or  [上文]催办人是[催办人]  or  催办[次]数[催办次数]的任务  or  [创建时间],[拟完成时间],[回复时间],[参与人],[发起人],[受理人],[内容],[催办次数],  or  发起人是[发起人]  or  发起人[中]有[发起人]  or  参与人是[参与人]  or  参与人[中]有[参与人]  or  [参与人],[发起人],[受理人],[内容],[催办次数]  or  搜索参与人是[参与人],发起人是[发起人],受理人是[受理人],内容包含[内容],催办次数是[催办次数]的1do  or  内容中包含[内容]的[下文]  or  催办次数是[催办次数]",
                "kid": "152148664591056896",
                "typeName": "1do搜索规则",
                "id": 277,
                "isPersistence": false
            },
            {
                "typeDescribe": "给[人员]发放垃圾袋  or  清理绿化带  or  处理小区[事物内容]  or  [社区日报内容1]清理绿化带[社区日报内容2]  or  [社区日报内容1]处理[社区日报内容2]  or  [社区日报内容1]缴纳[社区日报内容2]  or  [社区日报内容1]低保户[社区日报内容2]  or  [社区日报内容1]发放[社区日报内容2]  or  [社区日报内容1]材料[社区日报内容2]  or  [社区日报内容1]申请[社区日报内容2]  or  [社区日报内容1]企退[社区日报内容2]  or  [社区日报内容1]办理[社区日报内容2]  or  [社区日报内容1]登记[社区日报内容2]  or  [社区日报内容1]做[社区日报内容2]调查[社区日报内容3]",
                "kid": "135913501402071040",
                "typeName": "社区日报",
                "id": 112,
                "isPersistence": false
            },
            {
                "typeDescribe": "请[人员]牵头完成[工作内容]  or  请[人员]来一下[工作内容]  or  [人员]在吗[工作内容]  or  [工作备注]请[人员]安排[工作内容]  or  [工作备注]请[人员]牵头[工作内容]  or  [工作备注]请[人员]加快[工作内容]  or  请[工作内容]  or  [工作备注]请[工作内容]",
                "kid": "134830894564245504",
                "typeName": "下城领导批示",
                "id": 100,
                "isPersistence": false
            },
            {
                "typeDescribe": "需求:[需求描述]",
                "kid": "6",
                "typeName": "需求",
                "id": 5,
                "isPersistence": false
            }
        ]
    },
    "message": "Success",
    "status": 0
}
```

###   17功能 ：查询所有类型概念定义

#### 请求方法：  /md/type/selectAllType

#### 返回值说明：

| 字段           | 类型     | 描述         |
| ------------ | ------ | ---------- |
| data         | object | 数据         |
| message      | String | 返回值信息      |
| status       | int    | 返回值状态      |
| list         |        |            |
| typeDescribe | String | 知识类型描述     |
| kid          | String | 知识点类型表主键id |
| typeName     | String | 知识类型名称     |

**Success**

```json
{
    "data": [
        {
            "typeDescribe": "评价:[被评对象]([评价人],[评价时间])=[评语]  or  关联:[关联对象]([关联角色])([被关联角色])[被关联对象]",
            "kid": null,
            "typeName": "评价"
        },
        {
            "typeDescribe": "[上下文]:[源词]=[同义词]  or  [源词]就是[目标词]",
            "kid": "1",
            "typeName": "同义词"
        },
        {
            "typeDescribe": "[人员]但任[组织[的[职务]",
            "kid": "2",
            "typeName": "人员职务"
        },
        {
            "typeDescribe": "[人员]在[组织]负责[工作内容]",
            "kid": "3",
            "typeName": "工作职责"
        },
        {
            "typeDescribe": "bug:[问题描述] 产品:[产品名] 版本:[版本号] 重现步骤:[重现步骤]",
            "kid": "5",
            "typeName": "bug"
        },
        {
            "typeDescribe": "需求:[需求描述]",
            "kid": "6",
            "typeName": "需求"
        },
        {
            "typeDescribe": "术语:[术语]指[术语定义]",
            "kid": "7",
            "typeName": "术语解释"
        },
        {
            "typeDescribe": "[目标]到[结果]需要[步骤]  or  [需求人]需要[需求]请求[目标人]帮助",
            "kid": "71037658154926080",
            "typeName": "操作步骤"
        },
        {
            "typeDescribe": "[游戏名]需要[金钱]加[家族]",
            "kid": "71069914437255168",
            "typeName": "游戏人生"
        },
        {
            "typeDescribe": "问:[问题]答:[答案]",
            "kid": "8",
            "typeName": "问题解答"
        },
        {
            "typeDescribe": "代称:[代称词]=[实例词]",
            "kid": "9",
            "typeName": "代称"
        }
    ],
    "message": "Success",
    "status": 0
}
```

###  18功能 ：根据知识类型名称查询类型概念定义

#### 请求方法：  /md/type/getType

#### 参数说明：

| 字段       | 类型     | 是否必填 | 描述及要求  |
| -------- | ------ | ---- | ------ |
| typeName | String | 必填   | 知识类型名称 |

#### 返回值说明：

| 字段         | 类型   | 描述               |
| ------------ | ------ | ------------------ |
| data         | object | 数据               |
| message      | String | 返回值信息         |
| status       | int    | 返回值状态         |
| typeDescribe | String | 知识类型描述       |
| kid          | String | 知识点类型表主键id |
| typeName     | String | 知识类型名称       |

**Success**

```json
{
    "data": {
        "typeDescribe": "[上下文]:[源词]=[同义词]  or  [源词]就是[同义词]",
        "kid": "1",
        "typeName": "同义词"
    },
    "message": "Success",
    "status": 0
}
```

###   19功能 ：新增类型概念定义

#### 请求方法：  /md/type/insertType

#### 参数说明：

| 字段         | 类型   | 是否必填 | 描述及要求                                                   |
| ------------ | ------ | -------- | ------------------------------------------------------------ |
| kId          | String | 必填     | 知识点类型表主键id(没有值就填空)                             |
| typeName     | String | 必填     | 知识类型名称                                                 |
| typeDescribe | String | 必填     | 知识类型描述(例子：["([说话人])对([听众])说:[内容]","[某某人]说[某某]是[蘑菇]"]) |

#### 返回值说明：

| 字段      | 类型     | 描述    |
| ------- | ------ | ----- |
| data    | object | 数据    |
| message | String | 返回值信息 |
| status  | int    | 返回值状态 |

**Success**

```json
{
    "data": [
        1,
        1,
        1
    ],
    "message": "Success",
    "status": 0
}
```

###   20功能 ：分页查询类型实现定义

#### 请求方法：  /md/type/selectKtdef

#### 参数说明：

| 字段         | 类型   | 是否必填 | 描述及要求 |
| ---------- | ---- | ---- | ----- |
| pageNumber | int  | 必填   | 页码    |

#### 返回值说明：

| 字段           | 类型    | 描述                                     |
| -------------- | ------- | ---------------------------------------- |
| data           | object  | 数据                                     |
| message        | String  | 返回值信息                               |
| status         | int     | 返回值状态                               |
| totalRow       | int     | 全部条数                                 |
| pageNumber     | int     | 当前页数                                 |
| lastPage       | boolean | 是否是最后一页                           |
| firstPage      | boolean | 是否是第一页                             |
| totalPage      | int     | 全部页数                                 |
| pageSize       | int     | 一页条数                                 |
| list           |         |                                          |
| typeDescribe   | String  | 知识类型描述                             |
| kid            | String  | 知识点类型表主键id                       |
| typeName       | String  | 知识类型名称                             |
| typeTablesDef  | String  | 物理表定义，知识点存贮的分类知识表的表名 |
| typeDefinition | String  | 知识类型定义,正则语法表达式              |
|                |         |                                          |
|                |         |                                          |

**Success**

```json
{
    "data": {
        "totalRow": 11,
        "pageNumber": 1,
        "lastPage": false,
        "firstPage": true,
        "totalPage": 3,
        "pageSize": 5,
        "list": [
            {
                "typeTablesDef": "details_rela(关联词表)",
                "typeDescribe": "评价:[被评对象]([评价人],[评价时间])=[评语]or关联:[关联对象]([关联角色])([被关联角色])[被关联对象]",
                "typeDefinition": "评价[:：](.*?)[\\(（](.*?)[,，](.*?)[\\)）]=(.*?)$or关联:(.*?)\\((.*?)\\)\\(.*?\\)(.*?)$",
                "kid": null,
                "typeName": "评价"
            },
            {
                "typeTablesDef": "details_synonym(同义词表)ordetails_tongyici6(同义词表)",
                "typeDescribe": "[上下文]:[源词]=[同义词]or[源词]就是[目标词]",
                "typeDefinition": "(.*?)[:：](.*?)=(.*?)$or(.*?)就是(.*?)$",
                "kid": "1",
                "typeName": "同义词"
            },
            {
                "typeTablesDef": "details_personpost(人员职务表)",
                "typeDescribe": "[人员]但任[组织[的[职务]",
                "typeDefinition": "(.*?)担*任(.*?)的(.*?)$",
                "kid": "2",
                "typeName": "人员职务"
            },
            {
                "typeTablesDef": "details_Jobresponsibilities(工作职责表)",
                "typeDescribe": "[人员]在[组织]负责[工作内容]",
                "typeDefinition": "(.*?)在(.*?)负责(.*?)$",
                "kid": "3",
                "typeName": "工作职责"
            },
            {
                "typeTablesDef": "details_bug(bug表)",
                "typeDescribe": "bug:[问题描述] 产品:[产品名] 版本:[版本号] 重现步骤:[重现步骤]",
                "typeDefinition": "bug:(.*?)产品:(.*?)版本:(.*?)重现步骤:(.*?)$",
                "kid": "5",
                "typeName": "bug"
            }
        ]
    },
    "message": "Success",
    "status": 0
}
```

###   21功能 ：编辑类型实现定义

#### 请求方法：  /md/type/updateKtdef

#### 参数说明：

| 字段   | 类型     | 是否必填 | 描述及要求      |
| ---- | ------ | ---- | ---------- |
| kid  | String | 必填   | 知识点类型表主键id |

#### 返回值说明：

| 字段                 | 类型    | 描述                        |
| -------------------- | ------- | --------------------------- |
| data                 | object  | 数据                        |
| message              | String  | 返回值信息                  |
| status               | int     | 返回值状态                  |
| typeDescribe         | String  | 知识类型描述                |
| kid                  | String  | 知识点类型表主键id          |
| table_cname          | String  | 表中文名                    |
| typeTablesDef        | String  | 表英文名                    |
| typeDefinition       | String  | 知识类型定义,正则语法表达式 |
| id                   | int     | id                          |
| is_create            | boolean | 是否已创建表格              |
| base                 |         |                             |
| ename                | String  | 字段名                      |
| decimal_point        | int     | 小数点                      |
| is_key               | boolean | 是否主键                    |
| is_null              | boolean | 是否为空                    |
| length               | int     | 长度                        |
| comment              | String  | 注释                        |
| id                   | int     | id                          |
| type                 | String  | 字段类型                    |
| tag_strategy         | int     | 标签提醒策略                |
| is_party             | Boolean | 是否本体                    |
| tag_type_id          | long    | 标签类型                    |
|                      |         |                             |
| empiricalProbability | double  | 经验概率                    |
| sampleProbability    | double  | 样本概率                    |
| is_take_effect       | boolean | 是否生效                    |
| examples             | String  | 例句                        |
| scene                | list    | 适用场景                    |
| otherBase            | list    | 其他字段                    |

**Success**

```json
{
    "data": [
        {
            "typeTablesDef": "details_synonym",
            "table_cname": "同义词表",
            "typeDescribe": "[上下文]:[源词]=[同义词]",
            "typeDefinition": "(.*?)[:：](.*?)=(.*?)$",
            "kid": "1",
            "id": 1,
            "is_create": true,
            "sampleProbability":100.00,
            "empiricalProbability":0.00,
            "is_take_effect": false,
             "scene":[{"sceneId":"适用场景id","sceneName":"适用场景名称"},{"sceneId":"2","sceneName":"拱墅"}],"examples":"例句",
            "base": [
                {
                    "tag_strategy": 2,
                    "ename": "sjmc",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "事件名称",
                    "id": 1352,
                    "type": "text",
                    "is_party": false,
                    "tag_type_id": null,
                    "scene": []
                },
                {
                    "tag_strategy": 2,
                    "ename": "sjmc",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "事件名称",
                    "id": 1353,
                    "type": "text",
                    "is_party": false,
                    "tag_type_id": null,
                    "scene": []
                }
            ],
            "otherBase": [
                {
                    "tag_strategy": 2,
                    "ename": "sjmc",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "事件名称",
                    "id": 1352,
                    "type": "text",
                    "is_party": false,
                    "tag_type_id": null,
                    "scene": []
                },
                {
                    "tag_strategy": 2,
                    "ename": "sjmc",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "事件名称",
                    "id": 1353,
                    "type": "text",
                    "is_party": false,
                    "tag_type_id": null,
                    "scene": []
                }
            ]
        },
        {
            "typeTablesDef": "details_tongyici6",
            "table_cname": "同义词表",
            "typeDescribe": "[源词]就是[目标词]",
            "typeDefinition": "(.*?)就是(.*?)$",
            "kid": "1",
            "id": 21,
            "is_create": true,
            "sampleProbability":100.00,
            "empiricalProbability":0.00,x
            "base": [
                {
                    "ename": "yc",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "源词",
                    "id": 280,
                    "type": "text"
                },
                {
                    "ename": "mbc",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "目标词",
                    "id": 281,
                    "type": "text"
                }
            ]
        }
    ],
    "message": "Success",
    "status": 0
}
```

###    22功能 ：保存类型实现定义编辑

#### 请求方法：post  /md/type/saveEdit

#### 参数说明：json

| 字段           | 类型    | 描述                                                    |
| -------------- | ------- | ------------------------------------------------------- |
| typeDescribe   | String  | 知识类型描述                                            |
| kid            | String  | 知识点类型表主键id                                      |
| table_cname    | String  | 表中文名                                                |
| typeTablesDef  | String  | 表英文名                                                |
| typeDefinition | String  | 知识类型定义,正则语法表达式                             |
| id             | int     | id                                                      |
| is_create      | boolean | 是否已创建表格                                          |
| base           |         |                                                         |
| ename          | String  | 字段名                                                  |
| decimal_point  | int     | 小数点                                                  |
| is_key         | boolean | 是否主键                                                |
| is_null        | boolean | 是否为空                                                |
| length         | int     | 长度                                                    |
| comment        | String  | 注释                                                    |
| id             | int     | id(新增的id为0)                                         |
| type           | String  | 字段类型                                                |
| is_retain      | boolean | 是否保留已有的解析  保留传true  不保留false             |
| examples       | string  | 例句                                                    |
| is_take_effect | boolean | 是否生效                                                |
|                |         |                                                         |
| scene          | list    | 适用场景                                                |
| sceneName      | String  | 适用场景名称                                            |
| sceneId        | long    | 适用场景id                                              |
|                |         |                                                         |
| otherBase      | list    | 类型描述其他字段                                        |
| is_party       | boolean | 是否主体                                                |
| tag_strategy   | int     | 标签提醒策略（0新标签进行待审1新标签进正式2禁止新标签） |
| tag_type_id    | long    | 标签类型id，对应wellread.tag_categories数据id           |

```json
{
            "table_cname": "历史事件表",
            "typeDescribe": "历史事件[事件名称]",
            "kid": "493934951952023552",
            "typeName": "历史事件",
            "is_take_effect": true,
            "sampleProbability": 0.0,
            "empiricalProbability": 100.0,
            "isPersistence": true,
            "scene": [
                {
                    "sceneName": "钱塘",
                    "": 1
                },
                {
                    "sceneName": "通用",
                    "sceneId": 3
                }
            ],
            "typeTablesDef": "details_lishishijian",
            "examples": "第一个例子",
            "typeDefinition": "历史事件(.*?)$",
            "otherBase": [
                {
                    "tag_strategy": 2,
                    "ename": "sjmc",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "事件名称",
                    "id": 1352,
                    "type": "text",
                    "is_party": false,
                    "tag_type_id": null
                }
            ],
            "id": 587,
            "is_create": true,
            "base": [
                {
                    "tag_strategy": 2,
                    "ename": "sjmc",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "事件名称",
                    "id": 1351,
                    "type": "text",
                    "is_party": true,
                    "tag_type_id": 20214444,
                    "scene": [
                        {
                            "sceneName": "钱塘",
                            "sceneId": 1
                        },
                        {
                            "sceneName": "拱墅",
                            "sceneId": 2
                        }
                    ]
                },
                {
                    "tag_strategy": 0,
                    "ename": "sxw",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "上下文",
                    "id": 1354,
                    "type": "text",
                    "is_party": false,
                    "tag_type_id": null,
                    "scene": [
                        {
                            "sceneName": "钱塘",
                            "sceneId": 1
                        },
                        {
                            "sceneName": "通用",
                            "sceneId": 3
                        }
                    ]
                },
                {
                    "tag_strategy": 2,
                    "ename": "context",
                    "decimal_point": 0,
                    "is_key": false,
                    "is_null": true,
                    "length": 0,
                    "comment": "内容",
                    "id": 1355,
                    "type": "text",
                    "is_party": false,
                    "tag_type_id": null,
                    "scene": []
                }
            ]
        }
```

#### 返回值说明：

| 字段      | 类型     | 描述    |
| ------- | ------ | ----- |
| data    | object | 数据    |
| message | String | 返回值信息 |
| status  | int    | 返回值状态 |

**Success**

```json
{
    "data": null,
    "message": "details_bug表已存在",
    "status": 500
}
```

###  23功能 ：登出

#### 请求方法：  http://localhost:18080/md/loginOut

**Success**

```json
{
    "data": "成功退出",
    "message": "Success",
    "status": 0
}
```

### 24功能 ：解析一条知识点信息（只解析不保存）

#### 请求方法：  /md/knowledge/analysis

#### 参数说明：

| 字段    | 类型   | 是否必填 | 描述及要求 |
| ------- | ------ | -------- | ---------- |
| kiId    | String | 必填     | 录入信息id |
| details | String | 必填     | 详情       |

```
{"details":"公文术语:区数据资源管理局在阅办文件中的意见里\\\"传阅\"指的是\\\"请局领导阅示。请全局工作人员阅。\\\"","kiId":1}
```



#### 返回值说明：

| 字段           | 类型    | 描述                                     |
| -------------- | ------- | ---------------------------------------- |
| data           | object  | 数据                                     |
| message        | String  | 返回值信息                               |
| status         | int     | 返回值状态                               |
| typeDescribe   | String  | 知识类型描述                             |
| id             | String  | 正则配置表主键id                         |
| typeName       | String  | 知识类型名称                             |
| typeTablesDef  | String  | 物理表定义，知识点存贮的分类知识表的表名 |
| typeDefinition | String  | 知识类型定义,正则语法表达式              |
| typeKey        | String  | （程序分割符）配置                       |
| is_create      | boolean | 相关表是否已创建 1是0否                  |

**Success**

```json
{
    "data": [
        {
            "typeTablesDef": "details_Jobresponsibilities",
            "typeKey": "负责|的|",
            "typeDescribe": "[人员]负责[机构]的[工作内容]",
            "typeDefinition": "(.*?)负责(.*?)的(.*?)$",
            "typeName": "工作职责",
            "id": 24,
            "is_create": true
        },
        {
            "typeTablesDef": "details_Jobresponsibilities",
            "typeKey": "负责|",
            "typeDescribe": "[人员]负责[工作内容]",
            "typeDefinition": "(.*?)负责(.*?)$",
            "typeName": "工作职责",
            "id": 25,
            "is_create": true
        }
    ],
    "message": "Success",
    "status": 0
}
```

### 25功能 ：保存解析一条知识点信息（不解析只保存）

#### 请求方法：  /md/knowledge/analysis1

#### 参数说明：json格式

| 字段    | 类型   | 是否必填 | 描述及要求   |
| ------- | ------ | -------- | ------------ |
| kiId    | String | 必填     | 录入信息id   |
| details | String | 必填     | 详情         |
| list    | list   | 必填     | 解析后的类型 |

```
{"kiId":"1","details":"公文术语:区数据资源管理局在阅办文件中的意见里\"传阅\"指的是\"请局领导阅示。请全局工作人员阅。\"","list":[{"id":394}]}
```



#### 返回值说明：

| 字段    | 类型   | 描述       |
| ------- | ------ | ---------- |
| data    | object | 数据       |
| message | String | 返回值信息 |
| status  | int    | 返回值状态 |

**Success**

```json
{
    "data": "保存成功",
    "message": "Success",
    "status": 0
}
```

### 

### 26功能 ：修改或删除一条知识点解析（修改只解析不保存）

#### 请求方法：  /md/knowledge/updateOrDeleteAnalysis

#### 参数说明：json

| 字段    | 类型   | 是否必填 | 描述及要求                   |
| ------- | ------ | -------- | ---------------------------- |
| kdid    | String | 必填     | 详情id                       |
| details | String | 必填     | 详情                         |
| methods | String | 必填     | 修改填update，删除填写delete |

```
{
    "kdid": "6461",
    "details":"评价:老徐(张开代,2018-8-6=有“知心大叔”",
    "methods": "update"
}
```



#### 返回值说明：

| 字段           | 类型    | 描述                                     |
| -------------- | ------- | ---------------------------------------- |
| data           | object  | 数据                                     |
| message        | String  | 返回值信息                               |
| status         | int     | 返回值状态                               |
| typeDescribe   | String  | 知识类型描述                             |
| id             | String  | 正则配置表主键id                         |
| typeName       | String  | 知识类型名称                             |
| typeTablesDef  | String  | 物理表定义，知识点存贮的分类知识表的表名 |
| typeDefinition | String  | 知识类型定义,正则语法表达式              |
| typeKey        | String  | （程序分割符）配置                       |
| is_create      | boolean | 相关表是否已创建 1是0否                  |

**Success**

```json
{
    "data": true,
    "message": "Success",
    "status": 0
}

```

```
{
    "data": [
        {
            "typeTablesDef": "details_Jobresponsibilities",
            "typeKey": "负责|的|",
            "typeDescribe": "[人员]负责[机构]的[工作内容]",
            "typeDefinition": "(.*?)负责(.*?)的(.*?)$",
            "typeName": "工作职责",
            "id": 24,
            "is_create": true
        },
        {
            "typeTablesDef": "details_Jobresponsibilities",
            "typeKey": "负责|",
            "typeDescribe": "[人员]负责[工作内容]",
            "typeDefinition": "(.*?)负责(.*?)$",
            "typeName": "工作职责",
            "id": 25,
            "is_create": true
        },
        {
            "typeTablesDef": "details_ceshi",
            "typeKey": "负责|的|",
            "typeDescribe": "[人员]负责[机构]的[工作内容]",
            "typeDefinition": "(.*?)负责(.*?)的(.*?)$",
            "typeName": "测试",
            "id": 38,
            "is_create": true
        }
    ],
    "message": "Success",
    "status": 0
}
```

### 27功能 ：保存修改后的知识点解析

#### 请求方法：  /md/knowledge/updateOrDeleteAnalysis1

#### 参数说明：json格式

| 字段    | 类型   | 是否必填 | 描述及要求   |
| ------- | ------ | -------- | ------------ |
| kdid    | String | 必填     | 详情id       |
| details | String | 必填     | 详情         |
| list    | list   | 必填     | 解析后的类型 |

```
{
    "kdid": "6019",
    "details": "术语:后续城市大脑开发任务，DT研发部只负责后台Java代理开发和打包以及中枢接入指导部分工作，其余不负责",
    "list": [{"id":37},{"id":40}]
}
```



#### 返回值说明：

| 字段    | 类型   | 描述       |
| ------- | ------ | ---------- |
| data    | object | 数据       |
| message | String | 返回值信息 |
| status  | int    | 返回值状态 |

**Success**

```
{
    "data": "保存成功",
    "message": "Success",
    "status": 0
}
```

### 28功能 ：查询一条知识点的推荐类型

#### 请求方法：   /md/knowledge/recommend

#### 参数说明：

| 字段 | 类型   | 是否必填 | 描述及要求 |
| ---- | ------ | -------- | ---------- |
| kiId | String | 必填     | 录入信息id |

#### 返回值说明：

| 字段         | 类型   | 描述                   |
| ------------ | ------ | ---------------------- |
| type         | String | 类型                   |
| num          | int    | 数量                   |
| msg          | list   | 半自动解析后的文本内容 |
| typeDescribe | String | 主动创建时间           |
| text         | String | 文本内容               |
| rid          | long   | 推荐类型id             |

**Success**

```
{
    "data": [
        {
            "msg": [
                {
                    "typeDescribe": "[人员]担任[组织]的[职务]",
                    "text": "方升群担任dt的开发",
                    "rid": 5
                    
                },
                ........
                {
                    "typeDescribe": "需求:[需求描述]",
                    "text": "需求:sss叫sggg",
                    "rid": 102
                   
                },
                {
                    "typeDescribe": "需求:[需求描述]",
                    "text": "需求:111:111=gaga",
                    "rid": 104
                    
                }
            ],
            "num": 33,
            "type": "需求"
        }
    ],
    "message": "Success",
    "status": 0
}
```

### 29功能 ：批量解析推荐类型

#### 请求方法：post   /md/knowledge/batchAnalysis

#### 参数说明：json格式

| 字段 | 类型   | 是否必填 | 描述及要求     |
| ---- | ------ | -------- | -------------- |
| kiId | String | 必填     | 录入信息id     |
| rids | list   | 必填     | 推荐类型id集合 |

```json
{"kiId":3,"rids":[1,2,3,4,5,6,7,8,9]}
```

#### 返回值说明：

| 字段         | 类型   | 描述                   |
| ------------ | ------ | ---------------------- |
| type         | String | 类型                   |
| num          | int    | 数量                   |
| msg          | list   | 半自动解析后的文本内容 |
| typeDescribe | String | 主动创建时间           |
| text         | String | 文本内容               |
| rid          | long   | 推荐类型id             |

**Success**

```
{
    "data": "解析成功",
    "message": "Success",
    "status": 0
}
```

### 30功能 ：校验是否符合领导批示接口(对外接口)

#### 请求方法：post   /md/leader/isApprove

#### 参数说明：json格式

| 字段 | 类型   | 是否必填 | 描述及要求     |
| ---- | ------ | -------- | -------------- |
| text | String | 必填     | 校验的文本信息 |

```json
{"text":"关于1do工作,方升群作出工作安排,要求刘佳民在5月3日完成转日志,并请张城作好配合"}
```



#### 返回值说明：

| 字段              | 类型   | 描述               |
| ----------------- | ------ | ------------------ |
| jobmemo           | String | 工作备注           |
| otherNames        | String | 其他参与人         |
| otherNames_showid |        | 其他参与人的showid |
| jobTitle          | String | 事项名称           |
| name              | String | 人员               |
| name_showid       | String | 人员的showid       |
| jobowner          | String | 发起人员           |
| jobowner_showid   | String | 发起人员的showid   |
| deadline          | String | 时限要求           |
| job               | String | 工作内容           |

**Success**

```json
{
    "data": {
        "jobmemo": "工作",
        "name_showid": "297NKDKkDzHZe2da",
        "otherNames": "张城",
        "jobowner_showid": "PQV8oo3jeeiDkLbY",
        "otherNames_showid": "8BmEYpm9kQUlNN7m",
        "jobTitle": "1do",
        "name": "刘佳民",
        "jobowner": "方升群",
        "deadline": "5月3日",
        "job": "转日志"
    },
    "message": "Success",
    "status": 0
}
```

### 31功能 ：校验是否自动转日志的接口(对外接口)

#### 请求方法：post   /md/log/isApprove

#### 参数说明：json格式

| 字段     | 类型   | 是否必填 | 描述及要求     |
| -------- | ------ | -------- | -------------- |
| text     | String | 必填     | 校验的文本信息 |
| typeName | String | 必填     | 匹配规则清单   |

```json
{"text":"给人员发放垃圾袋","typeName":"社区日报"}
```

#### 返回值说明：

| 字段 | 类型    | 描述                |
| ---- | ------- | ------------------- |
| data | boolean | true符合false不符合 |

**Success**

```json
{
    "data": true,
    "message": "Success",
    "status": 0
}
```

### 32功能 ：归档和取消归档

#### 请求方法：   /md/knowledge/isFile

#### 参数说明：

| 字段 | 类型 | 是否必填 | 描述及要求 |
| ---- | ---- | -------- | ---------- |
| kiId | Long | 必填     | 录入信息id |

```json
localhost:8080/md/knowledge/isFile?kiId=1
```

#### 返回值说明：

| 字段 | 类型    | 描述                                  |
| ---- | ------- | ------------------------------------- |
| data | boolean | true归档成功和取消归档成功，false失败 |

**Success**

```json
{
    "data": true,
    "message": "Success",
    "status": 0
}
```

###   33功能 ：根据类型kid查询类型概念定义

#### 请求方法：   /md/type/getTypeBykid?kid=1

#### 参数说明：

| 字段       | 类型    | 是否必填 | 描述及要求                |
| ---------- | ------- | -------- | ------------------------- |
| kid        | String  | 必填     | 知识类型id                |
| is_deleted | boolean | 选填     | 默认false，回收站里填true |

```json
/md/type/getTypeBykid?kid=1
```

#### 返回值说明：

| 字段                 | 类型   | 描述                 |
| -------------------- | ------ | -------------------- |
| ktdef                | list   | 类型描述集合         |
| knowledgetype        | object | 知识类型             |
| keyword              | list   | 关键词集合           |
| typeDescribe         | String | 类型描述             |
| examples             | String | 例句                 |
| id                   | long   | 类型描述id           |
| operation            | string | 操作                 |
| kid                  | String | 知识类型id           |
| type                 | String | 知识类型             |
| word                 | String | 关键词               |
| id                   | long   | 关键词id             |
| des                  | String | 说明                 |
| sampleProbability    | double | 样本概率 保留2位小数 |
| empiricalProbability | double | 经验概率 保留2位小数 |
| orgBsListexamples    | list   | 适用范围             |
| scene                | list   | 适用场景             |
| sceneName            | String | 适用场景名称         |
| sceneId              | Long   | 适用场景id           |
|                      |        |                      |





**Success**

```json
{
    "data": {
        "ktdef": [
            {
                "typeDescribe": "同义词:[上下文]:[源词]=[同义词]",
                "id": 1,
                "operation": "",
                "sampleProbability":0.00,
                "empiricalProbability":100.00
            },
            ...
            {
                "typeDescribe": "同义词:[上下文]喜欢叫[源词]为[同义词]",
                "id": 90,
                "operation": "",
                "sampleProbability":0.00,
                "empiricalProbability":100.00
            }
        ],
        "knowledgetype": {
             "des": "",
            "examples": "列句",
            "kid": "1",
            "type": "同义词",
            "operation": ""
        },
        "keyword": [
            {
                "id": 1,
                "word": "好",
                "operation": ""
            },
           ...
            {
                "id": 4,
                "word": "天猫",
                "operation": ""
            }
        ]
    },
     "orgBsList": [
            {
                "business_name": "的富兰克林",
                "kid": "340667464159330304",
                "organization_id": 706153338148840508,
                "modify_time": "2020-09-29 17:02:07",
                "remark": null,
                "id": 2,
                "area_type_id": 2,
                "organization_name": "4448",
                "area_type_name": "具体范围",
                "business_id": 708153328107225372,
                "status": 1
            }
        ]
    ,
        "scene": [
            {
                "sceneName": "钱塘",
                "sceneId": 1
            },
            {
                "sceneName": "拱墅",
                "sceneId": 2
            }
        ]
    },
    "message": "Success",
    "status": 0
}
```

###  

###  34功能 ：类型概念定义增删改

#### 请求方法：   /md/type/insertAndUpdateAndDeleteType

#### 参数说明：json格式

| 字段      | 类型    | 是否必填 | 描述及要求                                                   |
| --------- | ------- | -------- | ------------------------------------------------------------ |
| data      | json    | 必填     | 字段描述参考33.1返回值                                       |
| operation | String  | 必填     | 无任何操作空值：“”，删除填delete，修改填update（修改后的值填在typeDescribe、type、word），新增填insert（id，kid填null） |
| is_retain | boolean | 必填     | 是否保留已有的解析  保留传true  不保留false                  |
| orgBsList | list    | 选填     | 适用范围插件选择后的值                                       |
| scene     | list    | 选填     | 适用场景                                                     |
| sceneName | String  | 选填     | 适用场景名称                                                 |
| sceneId   | Long    | 选填     | 适用场景id                                                   |

```json
{
        "is_retain":true
        "ktdef": [
            {
                "typeDescribe": "同义词:[上下文]:[源词]=[同义词]",
                "id": 1,
                "operation": "insert",
                "sampleProbability":0.00,
                "empiricalProbability":100.00
            },
            {
                "typeDescribe": "同义词:[源词]就是[同义词]",
                "id": 11,
                "operation": "delete",
                "sampleProbability":0.00,
                "empiricalProbability":100.00
            },
            {
                "typeDescribe": "同义词:[源词]==[同义词]",
                "id": 34,
                "operation": "update",
                "sampleProbability":0.00,
                "empiricalProbability":100.00
            },
            {
                "typeDescribe": "同义词:[源词]也叫[同义词]",
                "id": 43,
                "operation": "",
                "sampleProbability":0.00,
                "empiricalProbability":100.00
            }
        ],
        "knowledgetype": {
            "kid": "1",
            "type": "同义词",
            "operation": "update",
            "examples":"例句"
        },
        "keyword": [
            {
                "id": 1,
                "word": "好",
                "operation": "update"
            },
            {
                "id": 2,
                "word": "系统",
                "operation": "delete"
            },
            {
                "id": 3,
                "word": "明天",
                "operation": "insert"
            },
            {
                "id": 4,
                "word": "天猫",
                "operation": ""
            }
        ],
"orgBsList": [
        {
            "businessId": "708153328107225372",
            "organizationId": "706153338148840508",
            "areaTypeId": 2,
            "areaTypeName": "具体范围",
            "organizationName": "4448",
            "businessName": "的富兰克林",
            "activeFlag": {
                "isBOActive": false,
                "isScopeActive": false
            }
        }
    ], "scene":[{"sceneId":"适用场景id","sceneName":"适用场景名称"},{"sceneId":"2","sceneName":"拱墅"}],"examples":"例句"
    }
```

#### 返回值说明：

**Success**

```json
{
    "data": "成功",
    "message": "Success",
    "status": 0
}
```

###  

###  35功能 ：删除知识点类型

#### 请求方法：   /md/type/deleteType

#### 参数说明：

| 字段      | 类型    | 是否必填 | 描述及要求                     |
| --------- | ------- | -------- | ------------------------------ |
| is_retain | boolean | 必填     | 是否保留已有解析 是true否false |
| kid       | String  | 必填     | 知识类型id                     |

```
/md/type/deleteType?is_retain=true&kid=115999807968903168
```

#### 返回值说明：

**Success**

```json
{
    "data": "删除成功",
    "message": "Success",
    "status": 0
}
```

###  36功能 ：根据类型名称查询类型概念定义

#### 请求方法：/md/type/getTypeByType

#### 36参数说明：

| 字段 | 类型   | 是否必填 | 描述及要求 |
| ---- | ------ | -------- | ---------- |
| type | String | 必填     | 类型名称   |

```json
 /md/type/getTypeByType?type=111
```

#### 36返回值说明：

| 字段          | 类型   | 描述         |
| ------------- | ------ | ------------ |
| ktdef         | list   | 类型描述集合 |
| knowledgetype | object | 知识类型     |
| keyword       | list   | 关键词集合   |
| typeDescribe  | String | 类型描述     |
| id            | long   | 类型描述id   |
| operation     | string | 操作         |
| kid           | String | 知识类型id   |
| type          | String | 知识类型     |
| word          | String | 关键词       |
| id            | long   | 关键词id     |
| des           | String | 说明         |

**Success**

```json
{
    "data": {
        "ktdef": [
            {
                "typeDescribe": "同义词:[上下文]:[源词]=[同义词]",
                "id": 1,
                "operation": ""
            },
            ...
            {
                "typeDescribe": "同义词:[上下文]喜欢叫[源词]为[同义词]",
                "id": 90,
                "operation": ""
            }
        ],
        "knowledgetype": {
             "des": "",
            "kid": "1",
            "type": "同义词",
            "operation": ""
        },
        "keyword": [
            {
                "id": 1,
                "word": "好",
                "operation": ""
            },
           ...
            {
                "id": 4,
                "word": "天猫",
                "operation": ""
            }
        ]
    },
    "message": "Success",
    "status": 0
}
```



```json
{
    "data": null,
    "message": "Success",
    "status": 0
}
```

### 37功能 ：回收站移出知识类型

#### 请求方法：   /md/type/removeRecyclingBinByType

#### 参数说明：

| 字段 | 类型   | 是否必填 | 描述及要求 |
| ---- | ------ | -------- | ---------- |
| kid  | String | 必填     | 知识类型id |

```
/md/type/removeRecyclingBinByType?kid=kid
```

#### 返回值说明：

**Success**

```json
{
    "data": "移出成功",
    "message": "Success",
    "status": 0
}
```

### 38功能 ：查询操作日志列表

#### 请求方法：post  /md/log/getLog

#### 参数说明：json

| 字段       | 类型 | 是否必填 | 描述及要求 |
| ---------- | ---- | -------- | ---------- |
| pageNumber | int  | 必填     | 页码       |
| pageSize   | int  | 必填     | 一页条数   |

```
{
    "pageNumber": 1,
    "pageSize": 15
}
```



#### 返回值说明：

| 字段       | 类型    | 描述           |
| ---------- | ------- | -------------- |
| data       | object  | 数据           |
| message    | String  | 返回值信息     |
| status     | int     | 返回值状态     |
| totalRow   | int     | 全部条数       |
| pageNumber | int     | 当前页数       |
| lastPage   | boolean | 是否是最后一页 |
| totalPage  | int     | 全部页数       |
| pageSize   | int     | 一页条数       |
| list       |         |                |
| gmt_create | String  | 操作时间       |
| is_deleted | String  | 是否删除       |
| appName    | String  | 账号           |
| module     | String  | 操作模块       |
| id         | long    | id             |
| text       | String  | 详情           |
| userName   | String  | 姓名           |
| type       | String  | 操作类型       |

**Success**

```json
{
    "data": {
        "totalRow": 47,
        "pageNumber": 1,
        "lastPage": false,
        "firstPage": true,
        "totalPage": 10,
        "pageSize": 5,
        "list": [
            {
                "gmt_create": "2019-09-11 09:50:47",
                "is_deleted": false,
                "appName": "fangshengqun",
                "module": "知识点管理",
                "id": 1,
                "text": "录入:【13146】",
                "userName": "方升群",
                "type": "知识点录入"
            },
            {
                "gmt_create": "2019-09-11 09:52:06",
                "is_deleted": false,
                "appName": "fangshengqun",
                "module": "知识点管理",
                "id": 2,
                "text": "导入:批量导入知识点【鹅鹅鹅，曲项向天歌。白毛浮绿水，红掌拨清波。】;【知识点2】;【知识点3】;【知识点4】;【知识点5】;",
                "userName": "方升群",
                "type": "批量导入"
            },
            {
                "gmt_create": "2019-09-11 09:52:47",
                "is_deleted": false,
                "appName": "fangshengqun",
                "module": "知识点管理",
                "id": 3,
                "text": "录入:【知识点4】",
                "userName": "方升群",
                "type": "知识点录入"
            },
            {
                "gmt_create": "2019-09-11 10:14:29",
                "is_deleted": false,
                "appName": "fangshengqun",
                "module": "知识点管理",
                "id": 4,
                "text": "删除:【知识点4】",
                "userName": "方升群",
                "type": "知识点删除"
            },
            {
                "gmt_create": "2019-09-11 10:16:27",
                "is_deleted": false,
                "appName": "fangshengqun",
                "module": "知识点管理",
                "id": 5,
                "text": "删除:【知识点2】",
                "userName": "方升群",
                "type": "知识点删除"
            }
        ]
    },
    "message": "Success",
    "status": 0
}
```

### 

### 39功能 ：彻底删除知识点

#### 请求方法： /md/knowledge/deleteThoroughlyKnowledgeinfo

#### 参数说明：

| 字段 | 类型   | 是否必填 | 描述及要求 |
| ---- | ------ | -------- | ---------- |
| kiId | String | 必填     | 录入信息id |

```
localhost:8080/md/knowledge/deleteThoroughlyKnowledgeinfo?kiId=1
```

#### 返回值说明：

| 字段    | 类型    | 描述         |
| ------- | ------- | ------------ |
| data    | boolean | 彻底删除成功 |
| message | String  | 返回值信息   |
| status  | int     | 返回值状态   |

**Success**

```json
{
    "data": "彻底删除成功",
    "message": "Success",
    "status": 0
}
```

### 40功能 ：彻底删除知识类型

#### 请求方法： /type/deleteThoroughlyType

#### 参数说明：

| 字段 | 类型   | 是否必填 | 描述及要求 |
| ---- | ------ | -------- | ---------- |
| kid  | String | 必填     | 知识类型id |

```
/md/type/deleteThoroughlyType?kid=135870130428051456
```

#### 返回值说明：

| 字段    | 类型    | 描述         |
| ------- | ------- | ------------ |
| data    | boolean | 彻底删除成功 |
| message | String  | 返回值信息   |
| status  | int     | 返回值状态   |

**Success**

```json
{
    "data": "彻底删除成功",
    "message": "Success",
    "status": 0
}
```

###   41功能 ：修改知识类型持久化

#### 请求方法： /md/type/updatePersistence 

#### 参数说明：

| 字段          | 类型    | 是否必填 | 描述及要求         |
| ------------- | ------- | -------- | ------------------ |
| kid           | String  | 必填     | 知识点类型表主键id |
| isPersistence | boolean | 必填     | 修改之前是否持久化 |

#### 返回值说明：

**Success**

```json
{
    "data": "成功",
    "message": "Success",
    "status": 0
}
```

###   42功能 ：知识点合并

   #### 请求方法：GET  /md/knowledge/merge

   #### 参数说明：

| 字段          | 类型    | 是否必填 | 描述及要求         |
| ------------- | ------- | -------- | ------------------ |
| kIdList       | String  | 必填      | 知识点类型表主键id集合 |

```
/md/knowledge/merge?kIdList=1215459429722357762,1215459429722357761
```

   #### 返回值说明：

   **Success**

   ```json
   {
       "data": "成功",
       "message": "Success",
       "status": 0
   }
   ```

###   43功能 ：批量解析原始知识点

   #### 请求方法：post  /md/knowledge/batchParsing

   #### 参数说明：

| 字段     | 类型 | 是否必填 | 描述及要求             |
| -------- | ---- | -------- | ---------------------- |
| kiIdList | list | 必填     | 知识点类型表主键id集合 |

```
{
	"kiIdList":[1232209580230967365,1228600897114734622]
}
```

   #### 返回值说明：

   **Success**

```
{
    "data": "共2条知识点，成功2条，推荐和疑似0条，失败0条",
    "message": "Success",
    "status": 0
}
```

###   44功能 ：知识热榜

   #### 请求方法：post  md/hotList/getKnowledgeHotList

   #### 参数说明：

| 字段        | 类型   | 是否必填 | 描述及要求                                                   |
| ----------- | ------ | -------- | ------------------------------------------------------------ |
| rankingType | int    | 必填     | 排行类型：1、知识提供量排行榜：提供原始知识点数量的前十排行榜，对应1懂内来源详情。2、知识梳理量排行榜：提供知识点解析数量的前十排行榜，对应1懂内解析人员。3、知识引用量排行榜：提供原始知识点被引用的数量的人的前十排行、4、知识引用量排行榜（应用）：引用知识点数量的应用前十排行，5、知识提取量排行榜 |
| type        | String | 必填     | 知识类型：全部类型、1懂内的其他知识类型如：同义词、人员信息等 |
| time        | String | 必填     | 时间：全部时间、本周、本月、本年、上一年度                   |

```
{
    "rankingType":1,
    "type":"同义词",
    "time":"全部时间"
}
```

#### 返回值说明：

| 字段        | 类型   | 描述                   |
| ----------- | ------ | ---------------------- |
| rankingType | object | 排行类型               |
| time        | String | 表头显示的时间         |
| type        | int    | 表头显示知识类型       |
| num         | int    | 数量                   |
| name        | String | 指标名称如姓名或系统名 |

   **Success**

```
{
    "data": {
        "rankingType": 1,
        "time": "全部时间",
        "type": "同义词",
        "list": [
            {
                "num": 45,
                "name": "徐杰"
            },
            {
                "num": 27,
                "name": "詹子恒"
            },
            {
                "num": 14,
                "name": "吴晗践"
            },
            {
                "num": 5,
                "name": "张开代"
            },
            {
                "num": 4,
                "name": "蒋娅楠"
            },
            {
                "num": 4,
                "name": "杨蔷     "
            },
            {
                "num": 3,
                "name": "陈清清"
            },
            {
                "num": 3,
                "name": "朱玲瑶"
            },
            {
                "num": 2,
                "name": "高楠"
            },
            {
                "num": 2,
                "name": "金江锋"
            }
        ]
    },
    "message": "Success",
    "status": 0
}
```

### 45功能 ：知识点解析详情

#### 请求方法：  /md/knowledge/details

#### 参数说明：json格式

| 字段 | 类型   | 是否必填 | 描述及要求 |
| ---- | ------ | -------- | ---------- |
| kdid | String | 必填     | 详情id     |

```
{
    "kdid": "6019"
}
```



#### 返回值说明：

| 字段    | 类型   | 描述       |
| ------- | ------ | ---------- |
| data    | object | 数据       |
| message | String | 返回值信息 |
| status  | int    | 返回值状态 |

**Success**

```
{
    "data": [
        "被评对象:|死亡证明",
        "评价人:死亡证明包括:合法医疗机构按规定出具的死亡医学证明或公安部门出具的死亡证明;外国籍的死亡人员",
        "评价时间:需提供经居住国有关机构公证并经中国驻外使、领馆确认的相关法律文件;在国外死亡的,需提交该国死亡证明及有翻译资质的专门机构翻译的中文版本;遗体捐献的,需提供相关职能部门的证明材料等",
        "评语:"
    ],
    "message": "Success",
    "status": 0
}
```

### 46功能 ：例句测试

#### 请求方法：  /md/type/examplesTest

#### 参数说明：json格式

| 字段     | 类型   | 是否必填 | 描述及要求 |
| -------- | ------ | -------- | ---------- |
| id       | long   | 必填     | 类型定义id |
| examples | String | 必填     | 例句       |

```
{
    "examples": "同步[系统名称]到[数据库]/n少时诵诗书",
    "id": 585
}
```



#### 返回值说明：

| 字段    | 类型   | 描述       |
| ------- | ------ | ---------- |
| data    | object | 数据       |
| message | String | 返回值信息 |
| status  | int    | 返回值状态 |

**Success**

```
{
    "data": "成功",
    "message": "Success",
    "status": 0
}
```

### 