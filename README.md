# 备忘录
### git常用操作
```
1. git init
2. git add .
3. git commit -m "备注"
4. git remote add origin https://... 项目地址
5. git push -u origin master
//登录用户操作
git config --global user.name "你的名称"
git config --global user.email "你的邮箱"
//切换库
git remote set-url origin xxx(新的仓库地址)
```
### vue项目初始化
```
1.安装vue
	npm i vue
2.安装vue-cli3
 	npm i @vue/cli -g
3.打开vue-cli3自带的项目管理界面创建项目或者命令行创建
	vue ui（推荐，可视化操作更方便） 或 vue create my-project(cd 到想要创建项目的目录)  如果提示vue不是内部命令，需在电脑中找到vue.cmd文件，并保存路径添加到系统环境变量中。
	配置中可以勾选需要的选项
4.安装element-ui
	npm i element-ui -S
	然后在main.js中引入element-ui
	import ElementUI from 'element-ui'
	import 'element-ui/lib/theme-chalk/index.css'

	Vue.use(ElementUI)
 ```
