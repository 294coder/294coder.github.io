---
title: VSCode Python import 自己写的模块报错ModuleNotFoundError
---

[参考链接](https://blog.csdn.net/weixin_41857881/article/details/127342287?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EYuanLiJiHua%7EPosition-3-127342287-blog-88385332.pc_relevant_3mothn_strategy_recovery&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EYuanLiJiHua%7EPosition-3-127342287-blog-88385332.pc_relevant_3mothn_strategy_recovery&utm_relevant_index=6)

在settings.json文件中加入红色框中的配置文件

<img src="https://raw.githubusercontent.com/294coder/blog_img_bed/main/img2/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202022-12-13%20175757.png" alt="屏幕截图 2022-12-13 175757" style="zoom:50%;" />

```json
    "terminal.integrated.env.osx": {
        "PYTHONPATH": "${workspaceFolder}/",
    },
    "terminal.integrated.env.linux": {
        "PYTHONPATH": "${workspaceFolder}/",
    },
    "terminal.integrated.env.windows": {
        "PYTHONPATH": "${workspaceFolder}/",
    }
```

然后打开设置，搜索`@ext:ms-python.python Execute In File Dir`，勾选选项

![image-20221213181626559](https://raw.githubusercontent.com/294coder/blog_img_bed/main/img2/image-20221213181626559.png)

重启VSCode即可。