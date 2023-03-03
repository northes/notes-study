
## 添加页面

在对应的目录下新建 `page.tpl` ``

修改 `resource/views/sidebar.json` 添加侧边栏目录与页面

在 `design` 下添加欲增加的页面
在 `page` 下添加欲增加侧边栏的页面

```json
[
    {
        "id": 3,
        "remark": "统计",
        "design": [
            {
                "title": "统计管理",
                "list": [
                    {
                        "title": "广告统计",
                        "folder": "statis",
                        "file": "ad_statis",
                        "params": []
                    },
                    {
                        "title": "新手关卡统计",
                        "folder": "statis",
                        "file": "new_player_statis",
                        "params": []
                    },
                    {
                        "title": "新手历史最大关卡统计",
                        "folder": "statis",
                        "file": "new_player_dungeon_history_statis",
                        "params": []
                    },
                    {
                        "title": "统计任务历史",
                        "folder": "statis",
                        "file": "statis_task_history",
                        "params": []
                    }
                ]
            }
        ],
        "page": [
            {
                "folder": "statis",
                "file": "ad_statis"
            },
            {
                "folder": "statis",
                "file": "home"
            },
            {
                "folder": "statis",
                "file": "new_player_statis"
            },
            {
                "folder": "statis",
                "file": "new_player_dungeon_history_statis"
            },
            {
                "folder": "statis",
                "file": "statis_task_history"
            }
        ],
        "all_page": false
    }
]
```

并在 `page.tpl` 上添加

```html
{{template "/auto_backend/base/header.tpl" .}}
```