# GitBook 插件

[插件官网](https://plugins.gitbook.com/)


## Search Plus

支持中文搜索, 需要将默认的 `search` 和 `lunr` 插件去掉。

[插件地址](https://plugins.gitbook.com/plugin/search-plus)

```json
{
    "plugins": ["-lunr", "-search", "search-plus"]
}
```

## advanced-emoji

支持emoji表情

[emoij表情列表](https://www.webpagefx.com/tools/emoji-cheat-sheet/)

[插件地址](https://plugins.gitbook.com/plugin/advanced-emoji)

```json
{
    "plugins": [
        "advanced-emoji"
    ]
}
```

使用示例：

:smile: :blush: :stuck_out_tongue_closed_eyes:

## Github

添加github图标

[插件地址](https://plugins.gitbook.com/plugin/github)

```json
{
    "plugins": [
        "github"
    ],
    "pluginsConfig": {
        "github": {
            "url": "https://github.com/zhangjikai"
        }
    }
}
```

## Github Buttons

添加项目在 github 上的 star，watch，fork情况

[插件地址](https://plugins.gitbook.com/plugin/github-buttons)

```json
{
    "plugins": [
        "github-buttons"
    ],
    "pluginsConfig": {
        "github-buttons": {
            "repo": "zhangjikai/gitbook-use",
            "types": [
                "star",
                "watch",
                "fork"
            ],
            "size": "small"
        }
    }
}
```

## Sharing-plus

分享当前页面，比默认的 sharing 插件多了一些分享方式。

[插件地址](https://plugins.gitbook.com/plugin/sharing-plus)

```
 plugins: ["-sharing", "sharing-plus"]
```

配置:

```json
{
    "pluginsConfig": {
        "sharing": {
           "douban": false,
           "facebook": false,
           "google": true,
           "hatenaBookmark": false,
           "instapaper": false,
           "line": true,
           "linkedin": true,
           "messenger": false,
           "pocket": false,
           "qq": false,
           "qzone": true,
           "stumbleupon": false,
           "twitter": false,
           "viber": false,
           "vk": false,
           "weibo": true,
           "whatsapp": false,
           "all": [
               "facebook", "google", "twitter",
               "weibo", "instapaper", "linkedin",
               "pocket", "stumbleupon"
           ]
       }
    }
}
```

## Tbfed-pagefooter

为页面添加页脚

[插件地址](https://plugins.gitbook.com/plugin/tbfed-pagefooter)

```json
{
    "plugins": [
       "tbfed-pagefooter"
    ],
    "pluginsConfig": {
        "tbfed-pagefooter": {
            "copyright":"Copyright &copy MinGRn 2018",
            "modify_label": "该文件修订时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        }
    }
}
```

## Favicon

更改网站的 favicon.ico

[插件地址](https://plugins.gitbook.com/plugin/favicon)

```json
{
    "plugins": [
        "favicon"
    ],
    "pluginsConfig": {
        "favicon": {
            "shortcut": "assets/images/favicon.ico",
            "bookmark": "assets/images/favicon.ico",
            "appleTouch": "assets/images/apple-touch-icon.png",
            "appleTouchMore": {
                "120x120": "assets/images/apple-touch-icon-120x120.png",
                "180x180": "assets/images/apple-touch-icon-180x180.png"
            }
        }
    }
}
```

## Alerts

添加不同 alerts 样式的 blockquotes，目前包含 info, warning, danger 和 success 四种样式。

[插件地址](https://plugins.gitbook.com/plugin/alerts)

```json
{
    "plugins": ["alerts"]
}
```

下面是使用示例：

```
Info styling
> **[info] For info**
>
> Use this for infomation messages.

Warning styling
> **[warning] For warning**
>
> Use this for warning messages.

Danger styling
> **[danger] For danger**
>
> Use this for danger messages.

Success styling
> **[success] For info**
>
> Use this for success messages.
```

效果如下所示：

Info styling
> **[info] For info**
>
> Use this for infomation messages.

Warning styling
> **[warning] For warning**
>
> Use this for warning messages.

Danger styling
> **[danger] For danger**
>
> Use this for danger messages.

Success styling
> **[success] For info**
>
> Use this for success messages.

## Sectionx

将页面分块显示，标签的 tag 最好是使用 b 标签，如果使用 h1-h6 可能会和其他插件冲突。  

[插件地址](https://plugins.gitbook.com/plugin/sectionx)  

```json
{
    "plugins": [
       "sectionx"
   ],
    "pluginsConfig": {
        "sectionx": {
          "tag": "b"
        }
      }
}
```
使用示例

```
<!--sec data-title="Sectionx Demo" data-id="section0" data-show=true ces-->

Insert markdown content here (you should start with h3 if you use heading).  

<!--endsec-->
```

<!--sec data-title="Sectionx Demo" data-id="section0" data-show=true ces-->

Insert markdown content here (you should start with h3 if you use heading).  

<!--endsec-->

## Chart

使用 C3.js 或者 Highcharts 绘制图形。

[插件地址](https://plugins.gitbook.com/plugin/chart)  

[C3.js GitHub](https://github.com/c3js/c3)  

[highcharts GitHub](https://github.com/highcharts/highcharts)

```json
{
  "plugins": ["chart"],
  "pluginsConfig": {
      "chart": {
          "type": "highcharts"
      }
  }
}
```

[Highcharts 官网](https://www.highcharts.com/) 示例：

**注意：** 不能为图表指定 `renderTo` 属性

```
{% chart %}
{
    "chart": {
        "type": "spline"
    },
    "title": {
        "text": "Monthly Average Temperature"
    },
    "subtitle": {
        "text": "Source: WorldClimate.com"
    },
    "xAxis": {
        "categories": ["Jan", "Feb", "Mar", "Apr", "May", "Jun","Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
    },
    "yAxis": {
        "title": {
            "text": "Temperature"
        },
        "labels": {
            "format": "{value}°"
        }
    },
    "tooltip": {
        "crosshairs": true,
        "shared": true
    },
    "plotOptions": {
        "spline": {
            "marker": {
                "radius": 4,
                "lineColor": "#666666",
                "lineWidth": 1
            }
        }
    },
    "series": [{
        "name": "Tokyo",
        "marker": {
            "symbol": "square"
        },
        "data": [7.0, 6.9, 9.5, 14.5, 18.2, 21.5, 25.2, {
            "y": 26.5,
            "marker": {
                "symbol": "url(https://www.highcharts.com/samples/graphics/sun.png)"
            }
        }, 23.3, 18.3, 13.9, 9.6]
    }, {
        "name": "London",
        "marker": {
            "symbol": "diamond"
        },
        "data": [{
            "y": 3.9,
            "marker": {
                "symbol": "url(https://www.highcharts.com/samples/graphics/snow.png)"
            }
        }, 4.2, 5.7, 8.5, 11.9, 15.2, 17.0, 16.6, 14.2, 10.3, 6.6, 4.8]
    }]
}
{% endchart %}
```

{% chart %}
{
    "chart": {
        "type": "spline"
    },
    "title": {
        "text": "Monthly Average Temperature"
    },
    "subtitle": {
        "text": "Source: WorldClimate.com"
    },
    "xAxis": {
        "categories": ["Jan", "Feb", "Mar", "Apr", "May", "Jun","Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
    },
    "yAxis": {
        "title": {
            "text": "Temperature"
        },
        "labels": {
            "format": "{value}°"
        }
    },
    "tooltip": {
        "crosshairs": true,
        "shared": true
    },
    "plotOptions": {
        "spline": {
            "marker": {
                "radius": 4,
                "lineColor": "#666666",
                "lineWidth": 1
            }
        }
    },
    "series": [{
        "name": "Tokyo",
        "marker": {
            "symbol": "square"
        },
        "data": [7.0, 6.9, 9.5, 14.5, 18.2, 21.5, 25.2, {
            "y": 26.5,
            "marker": {
                "symbol": "url(https://www.highcharts.com/samples/graphics/sun.png)"
            }
        }, 23.3, 18.3, 13.9, 9.6]
    }, {
        "name": "London",
        "marker": {
            "symbol": "diamond"
        },
        "data": [{
            "y": 3.9,
            "marker": {
                "symbol": "url(https://www.highcharts.com/samples/graphics/snow.png)"
            }
        }, 4.2, 5.7, 8.5, 11.9, 15.2, 17.0, 16.6, 14.2, 10.3, 6.6, 4.8]
    }]
}
{% endchart %}