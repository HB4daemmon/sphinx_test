
Base — 基本接口规范
====================

Query - 基本查询规范
--------------------

* 预定义参数
**以下参数不能作为 筛选条件** :

==============      ==============
`s`                 排序关键字参数
`fields`            返回指定关键字参数
`access_token`      验证token
`embed`             管理文档名
`page`              分页页数
`page_size`         分页显示条数
`_ids`              objectid的列表
==============      ==============


* 概览
以下为列表的基本查询规范::

    http://www.igeek.top:8500/api/v1.0/city?access_token=3def698a-d539-460c-bd01-879ce7693772

其中 ``access_token`` 为登录获取的oauth2 的token

返回的结果类似于::

    {
      "response": {
        "error_msg": "",
        "data": [
          {
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "_id": "58083a661f38707b2eaf8987",
            "city_name": "南京市",
            "add_time": "2016-10-20 11:30:46.030",
            "last_updated_time": "2016-10-20 11:30:46.030"
          },
          {
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "_id": "58083a6c1f38707b2eaf8997",
            "city_name": "上海市",
            "add_time": "2016-10-20 11:30:52.727",
            "last_updated_time": "2016-10-20 11:30:52.727"
          },
          {
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "_id": "58083a771f38707b2eaf89a7",
            "city_name": "北京市",
            "add_time": "2016-10-20 11:31:03.861",
            "last_updated_time": "2016-10-20 11:31:03.861"
          },
          {
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "_id": "58083a7f1f38707b2eaf89b7",
            "city_name": "天津市",
            "add_time": "2016-10-20 11:31:11.805",
            "last_updated_time": "2016-10-20 11:31:11.805"
          }
        ],
        "pager": {
          "enable": false
        },
        "success": 1,
        "return_code": "success"
      },
      "meta": {
        "code": 200
      }
    }

* 筛选
 - `筛选语法`
 ==============      ==============
 `=`                 精确筛选
 `^=`                匹配筛选
 `>=`                数字类型的大于等于筛选
 `<=`                数字类型的小于等于筛选
 `@>=`               日期类型的大于等于筛选
 `@<=`               日期类型的小于等于筛选
 ==============      ==============

基本筛选直接添加在get参数::

    http://www.igeek.top:8500/api/v1.0/city?access_token=3def698a-d539-460c-bd01-879ce7693772&city_name^=京市&add_time@>=2016-10-20 11:30:45

其中 ``city_name`` 以及 ``add_time`` 为传入的参数, ``^=`` 以及 ``@>=`` 为筛选语法
返回的结果类似于::

    {
      "meta": {
        "code": 200
      },
      "response": {
        "pager": {
          "enable": false
        },
        "data": [
          {
            "add_time": "2016-10-20 11:30:46.030",
            "_id": "58083a661f38707b2eaf8987",
            "city_name": "南京市",
            "last_updated_time": "2016-10-20 11:30:46.030",
            "access_token": "3def698a-d539-460c-bd01-879ce7693772"
          },
          {
            "add_time": "2016-10-20 11:31:03.861",
            "_id": "58083a771f38707b2eaf89a7",
            "city_name": "北京市",
            "last_updated_time": "2016-10-20 11:31:03.861",
            "access_token": "3def698a-d539-460c-bd01-879ce7693772"
          }
        ],
        "error_msg": "",
        "return_code": "success",
        "success": 1
      }
    }

* 排序
排序是将需要排序的字段以 ``s=[-][field_name],[[-][field_name]...]``  的方式直接添加在get参数
使用 ``,`` 分割字段，如果是逆序则在字段名前添加 ``-`` ,例::

     http://www.igeek.top:8500/api/v1.0/city?access_token=3def698a-d539-460c-bd01-879ce7693772&s=-add_time,city_name

返回的结果类似于::

    {
      "response": {
        "data": [
          {
            "city_name": "天津市",
            "add_time": "2016-10-20 11:31:11.805",
            "last_updated_time": "2016-10-20 11:31:11.805",
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "_id": "58083a7f1f38707b2eaf89b7"
          },
          {
            "city_name": "北京市",
            "add_time": "2016-10-20 11:31:03.861",
            "last_updated_time": "2016-10-20 11:31:03.861",
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "_id": "58083a771f38707b2eaf89a7"
          },
          {
            "city_name": "上海市",
            "add_time": "2016-10-20 11:30:52.727",
            "last_updated_time": "2016-10-20 11:30:52.727",
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "_id": "58083a6c1f38707b2eaf8997"
          },
          {
            "city_name": "南京市",
            "add_time": "2016-10-20 11:30:46.030",
            "last_updated_time": "2016-10-20 11:30:46.030",
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "_id": "58083a661f38707b2eaf8987"
          }
        ],
        "success": 1,
        "pager": {
          "enable": false
        },
        "error_msg": "",
        "return_code": "success"
      },
      "meta": {
        "code": 200
      }
    }

* 返回指定字段
返回指定字段是将需要返回的字段以 ``fields=[field_name][,[field_name]...]``  的方式直接添加在get参数
使用 ``,`` 分割字段例::

     http://www.igeek.top:8500/api/v1.0/city?access_token=3def698a-d539-460c-bd01-879ce7693772&fields=city_name,_id

返回的结果类似于::

    {
      "response": {
        "data": [
          {
            "city_name": "南京市",
            "_id": "58083a661f38707b2eaf8987"
          },
          {
            "city_name": "上海市",
            "_id": "58083a6c1f38707b2eaf8997"
          },
          {
            "city_name": "北京市",
            "_id": "58083a771f38707b2eaf89a7"
          },
          {
            "city_name": "天津市",
            "_id": "58083a7f1f38707b2eaf89b7"
          }
        ],
        "success": 1,
        "pager": {
          "enable": false
        },
        "error_msg": "",
        "return_code": "success"
      },
      "meta": {
        "code": 200
      }
    }

* 关联文档
关联文档可以方便的将 ``[collection_name]_id`` 形式的查询返回的字段直接获取相连的文档
将需要关联的集合以 ``embed=[collection_name][,[collection_name]...]``  的方式直接添加在get参数
使用 ``,`` 分割字段 例::

     http://www.igeek.top:8500/api/v1.0/area?access_token=3def698a-d539-460c-bd01-879ce7693772&embed=city

返回的结果类似于::

    {
      "meta": {
        "code": 200
      },
      "response": {
        "return_code": "success",
        "pager": {
          "enable": false
        },
        "error_msg": "",
        "success": 1,
        "data": [
          {
            "add_time": "2016-10-20 13:40:16.725",
            "area_name": "雨花台区",
            "last_updated_time": "2016-10-20 13:40:16.725",
            "city": {
              "add_time": "2016-10-20 11:30:46.030",
              "_id": "58083a661f38707b2eaf8987",
              "city_name": "南京市",
              "access_token": "3def698a-d539-460c-bd01-879ce7693772",
              "last_updated_time": "2016-10-20 11:30:46.030"
            },
            "city_id": "58083a661f38707b2eaf8987",
            "_id": "580858c01f38700338b60de8"
          },
          {
            "add_time": "2016-10-20 13:40:30.454",
            "area_name": "玄武区",
            "last_updated_time": "2016-10-20 13:40:30.454",
            "city": {
              "add_time": "2016-10-20 11:30:46.030",
              "_id": "58083a661f38707b2eaf8987",
              "city_name": "南京市",
              "access_token": "3def698a-d539-460c-bd01-879ce7693772",
              "last_updated_time": "2016-10-20 11:30:46.030"
            },
            "city_id": "58083a661f38707b2eaf8987",
            "_id": "580858ce1f38700338b60df8"
          },
          {
            "add_time": "2016-10-20 13:40:37.453",
            "area_name": "建邺区",
            "last_updated_time": "2016-10-20 13:40:37.453",
            "city": {
              "add_time": "2016-10-20 11:30:46.030",
              "_id": "58083a661f38707b2eaf8987",
              "city_name": "南京市",
              "access_token": "3def698a-d539-460c-bd01-879ce7693772",
              "last_updated_time": "2016-10-20 11:30:46.030"
            },
            "city_id": "58083a661f38707b2eaf8987",
            "_id": "580858d51f38700338b60e08"
          },
          {
            "add_time": "2016-10-20 13:40:46.261",
            "area_name": "朝阳区",
            "last_updated_time": "2016-10-20 13:40:46.261",
            "city": {
              "add_time": "2016-10-20 11:31:03.861",
              "_id": "58083a771f38707b2eaf89a7",
              "city_name": "北京市",
              "access_token": "3def698a-d539-460c-bd01-879ce7693772",
              "last_updated_time": "2016-10-20 11:31:03.861"
            },
            "city_id": "58083a771f38707b2eaf89a7",
            "_id": "580858de1f38700338b60e18"
          },
          {
            "add_time": "2016-10-20 13:40:54.879",
            "area_name": "丰台区 ",
            "last_updated_time": "2016-10-20 13:40:54.880",
            "city": {
              "add_time": "2016-10-20 11:31:03.861",
              "_id": "58083a771f38707b2eaf89a7",
              "city_name": "北京市",
              "access_token": "3def698a-d539-460c-bd01-879ce7693772",
              "last_updated_time": "2016-10-20 11:31:03.861"
            },
            "city_id": "58083a771f38707b2eaf89a7",
            "_id": "580858e61f38700338b60e28"
          }
        ]
      }
    }

* 分页
通过传入 ``page`` 和 ``page_size`` 返回相应的分页信息
`注:page以及page_size需传入大于1的整数，默认page=1,page_size=15`

例::

    http://www.igeek.top:8500/api/v1.0/city?access_token=3def698a-d539-460c-bd01-879ce7693772&page=2&page_size=2

返回结果类似为::

    {
      "meta": {
        "code": 200
      },
      "response": {
        "return_code": "success",
        "pager": {
          "page_size": 2,
          "has_more": false,
          "enable": true,
          "pages": [
            1,
            2
          ],
          "skip": 2,
          "page_num": 1,
          "max_page": 2,
          "page": 2
        },
        "error_msg": "",
        "success": 1,
        "data": [
          {
            "add_time": "2016-10-20 11:31:03.861",
            "_id": "58083a771f38707b2eaf89a7",
            "city_name": "北京市",
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "last_updated_time": "2016-10-20 11:31:03.861"
          },
          {
            "add_time": "2016-10-20 11:31:11.805",
            "_id": "58083a7f1f38707b2eaf89b7",
            "city_name": "天津市",
            "access_token": "3def698a-d539-460c-bd01-879ce7693772",
            "last_updated_time": "2016-10-20 11:31:11.805"
          }
        ]
      }
    }

Query - 高级查询规范
--------------------

在list的相关接口中，在基本查询的所有方法都可以组合查询
基本规则为:
 -  `先查询再排序最后分页`
 -  `关联文档以及返回指定字段一定可用`

基本查询::

    http://www.igeek.top:8500/api/v1.0/area?access_token=3def698a-d539-460c-bd01-879ce7693772

结果::

    {
      "meta": {
        "code": 200
      },
      "response": {
        "return_code": "success",
        "error_msg": "",
        "pager": {
          "enable": false
        },
        "data": [
          {
            "last_updated_time": "2016-10-20 13:40:16.725",
            "area_name": "雨花台区",
            "add_time": "2016-10-20 13:40:16.725",
            "city_id": "58083a661f38707b2eaf8987",
            "_id": "580858c01f38700338b60de8"
          },
          {
            "last_updated_time": "2016-10-20 13:40:30.454",
            "area_name": "玄武区",
            "add_time": "2016-10-20 13:40:30.454",
            "city_id": "58083a661f38707b2eaf8987",
            "_id": "580858ce1f38700338b60df8"
          },
          {
            "last_updated_time": "2016-10-20 13:40:37.453",
            "area_name": "建邺区",
            "add_time": "2016-10-20 13:40:37.453",
            "city_id": "58083a661f38707b2eaf8987",
            "_id": "580858d51f38700338b60e08"
          },
          {
            "last_updated_time": "2016-10-20 13:40:46.261",
            "area_name": "朝阳区",
            "add_time": "2016-10-20 13:40:46.261",
            "city_id": "58083a771f38707b2eaf89a7",
            "_id": "580858de1f38700338b60e18"
          },
          {
            "last_updated_time": "2016-10-20 13:40:54.880",
            "area_name": "丰台区 ",
            "add_time": "2016-10-20 13:40:54.879",
            "city_id": "58083a771f38707b2eaf89a7",
            "_id": "580858e61f38700338b60e28"
          },
          {
            "last_updated_time": "2016-10-20 14:12:21.072",
            "area_name": "雨花台区",
            "add_time": "2016-10-20 14:12:21.072",
            "city_id": "58083a6c1f38707b2eaf8997",
            "_id": "580860451f38700381223026"
          },
          {
            "last_updated_time": "2016-10-20 14:13:56.818",
            "area_name": "雨花台区",
            "add_time": "2016-10-20 14:13:56.818",
            "city_id": "58083a7f1f38707b2eaf89b7",
            "_id": "580860a41f387003c462035e"
          }
        ],
        "success": 1
      }
    }

组合查询例::

    http://www.igeek.top:8500/api/v1.0/area?access_token=3def698a-d539-460c-bd01-879ce7693772&area_name=雨花台区&s=-add_time&embed=city&fields=_id,area_name,city&page=1&page_size=2

结果为::

    {
      "meta": {
        "code": 200
      },
      "response": {
        "return_code": "success",
        "error_msg": "",
        "pager": {
          "skip": 0,
          "pages": [
            1,
            2
          ],
          "max_page": 2,
          "page_size": 2,
          "page_num": 1,
          "has_more": true,
          "enable": true,
          "page": 1
        },
        "data": [
          {
            "city": {
              "add_time": "2016-10-20 11:31:11.805",
              "last_updated_time": "2016-10-20 11:31:11.805",
              "access_token": "3def698a-d539-460c-bd01-879ce7693772",
              "_id": "58083a7f1f38707b2eaf89b7",
              "city_name": "天津市"
            },
            "area_name": "雨花台区",
            "_id": "580860a41f387003c462035e"
          },
          {
            "city": {
              "add_time": "2016-10-20 11:30:52.727",
              "last_updated_time": "2016-10-20 11:30:52.727",
              "access_token": "3def698a-d539-460c-bd01-879ce7693772",
              "_id": "58083a6c1f38707b2eaf8997",
              "city_name": "上海市"
            },
            "area_name": "雨花台区",
            "_id": "580860451f38700381223026"
          }
        ],
        "success": 1
      }
    }
