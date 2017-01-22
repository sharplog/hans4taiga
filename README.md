# hans4taiga

[Taiga](https://taiga.io/)是一个敏捷项目管理软件。当前在发行的代码中还没有汉化，从其github上的代码中找到汉化文件（https://github.com/taigaio/taiga-front/tree/master/app/locales/taiga ）。但感觉其中有些内容汉化得不是很合适，便进行了修改。适应于taiga的3.0.0-stable。

汉化过程如下：
### 汉化后台
1. 下载https://github.com/taigaio/taiga-back/tree/master/taiga/locale/zh-Hans/LC_MESSAGES下的django.po，或将其文件内容拷贝到本地同名文件（utf-8编码）中 。
2.  在taiga-back目录下执行如下命令：
` django-admin.py makemessages -l zh_Hans（注意这儿是下划线）`
会在taiga/locale下面生成zh_Hans目录及相关文件
3. 将前面下载的django.po拷贝到zh_Hans/LC_MESSAGES目录下，覆盖上一命令生成的django.po
4.  在taiga-back目录下执行如下命令：
`django-admin.py compilemessages -l zh_Hans`
会在zh_Hans/LC_MESSAGES目录下生成django.mo文件
5. 修改~/taiga-back/settings/common.py：
将 ("zh-hans", "中文(简体)"),  # Simplified Chinese 这一行的注释放开
6. settings/local.py中添加如下一行：
`LANGUAGE_CODE = "zh-hans"（注意这儿是横线）`
7. 重启后台：
` circusctl restart taiga`

### 汉化前台
1. 下载https://github.com/taigaio/taiga-front/tree/master/app/locales/taiga下的locale-zh-hans.json，或将其文件内容拷贝到本地同名文件（utf-8编码）中
2.  将下载的这个locale-zh-hans.json 文件放到~/taiga-front-dist/dist/v-1477393748631/locales/taiga目录下
3.  修改dist/conf.json，将"defaultLanguage"的值改为"zh-hans":
`"defaultLanguage": "zh-hans"`
4.  这时，界面上可以显示中文了，但会报找不到脚本的错误，提示找不到v-1477393748631/locales/moment-locales/zh-hans.js文件，但该目录下有zh-cn.js文件（从django1.9开始，不用zh-cn，改用zh-hans了）。将zh-cn.js复制一份，改名为zh-hans.js即可。


