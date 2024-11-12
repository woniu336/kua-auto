

## 安装依赖



```
pip3 install aiohttp
sudo apt-get install jq
```



## 下载文件



```
cd ~
git clone https://github.com/woniu336/kua-auto.git
```



重命名目录:

```
mv kua-auto kua-update
```


**设置cookie**

在quark_config.json设置cookie和钉钉通知



**添加转存**

在movie_links.txt添加转存信息，格式,例如



```
如龙=https://pan.quark.cn/s/df4a1b9ceb00=/yyds/如龙
```



每行一条信息



前面是名称，中间是转存的链接，后面是转存的目录，使用等号区分



## 运行脚本

```
cd kua-update
python3 movie_list.py
python3 quark_auto_save.py quark_config.json
```





**自动化脚本**



```
#!/bin/bash

# 设置错误处理
set -euo pipefail
IFS=$'\n\t'

# 更新json配置
echo "开始更新json配置..."
cd /www/wwwroot/脚本所在目录 || { echo "切换目录失败"; exit 1; }

if python3 movie_list.py; then
    echo "movie_list.py 执行成功"
else
    echo "movie_list.py 执行失败" >&2
    exit 1
fi

# 转存
echo "开始转存..."
if python3 quark_auto_save.py quark_config.json; then
    echo "quark_auto_save.py 执行成功"
else
    echo "quark_auto_save.py 执行失败" >&2
    exit 1
fi

echo "脚本执行完毕"
```

