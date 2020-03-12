# mp-weixin-region-data
微信小程序省市区选择器数据字典

## 说明
数据来源微信小程序的省市区选择器，主要有两个用处：

- 自定义省市区选择器组件
- 服务端数据字典与客户端一致

## 数据格式
有三种模式

**multi**

省、市、区（县）的数据独立存放，通过 value 作为 key 进行关联。
```json
// province.json 省
{
    "value": "110000",
    "text": "北京"
}
// city.json 市
{
    "110000": [{
        "value": "110100",
        "text": "北京市"
    }]
}
// district.json 区
{
    "110100": [{
        "value": "110101",
        "text": "东城区"
    }, ...]
}
```

**single**

数据在一个文件中，类似父子结构存放。

```json
{
    "value": "110000",
    "text": "北京市",
    "children": [{
        "value": "110100",
        "text": "北京市",
        "children": [{
            "value": "110101",
            "text": "东城区"
        }, {
            "value": "110102",
            "text": "西城区"
        }, {
            "value": "110105",
            "text": "朝阳区"
        }, {
            "value": "110106",
            "text": "丰台区"
        }, {
            "value": "110107",
            "text": "石景山区"
        }, {
            "value": "110108",
            "text": "海淀区"
        }, {
            "value": "110109",
            "text": "门头沟区"
        }, {
            "value": "110111",
            "text": "房山区"
        }, {
            "value": "110112",
            "text": "通州区"
        }, {
            "value": "110113",
            "text": "顺义区"
        }, {
            "value": "110114",
            "text": "昌平区"
        }, {
            "value": "110115",
            "text": "大兴区"
        }, {
            "value": "110116",
            "text": "怀柔区"
        }, {
            "value": "110117",
            "text": "平谷区"
        }, {
            "value": "110118",
            "text": "密云区"
        }, {
            "value": "110119",
            "text": "延庆区"
        }]
    }]
}
```

**SQL**

```
CREATE TABLE IF NOT EXISTS `region` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `pid` int(11) NOT NULL DEFAULT '0',
  `name` varchar(100) NOT NULL DEFAULT '',
  `code` int(11) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `code` (`code`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 AUTO_INCREMENT=3371 ;
```

数据格式形如：
```
+----+-----+--------------+--------+
| id | pid | name         | code   |
+----+-----+--------------+--------+
|  1 |   0 | 北京市       | 110000 |
|  2 |   1 | 北京市       | 110100 |
|  3 |   2 | 东城区       | 110101 |
|  4 |   2 | 西城区       | 110102 |
|  5 |   2 | 朝阳区       | 110105 |
|  6 |   2 | 丰台区       | 110106 |
|  7 |   2 | 石景山区     | 110107 |
|  8 |   2 | 海淀区       | 110108 |
|  9 |   2 | 门头沟区     | 110109 |
| 10 |   2 | 房山区       | 110111 |
+----+-----+--------------+--------+
```
