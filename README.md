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
//修改远程仓库地址
	方法有三种：
	1.修改命令
	git remote set-url origin [url]
	2.先删后加
	git remote rm origin
	git remote add origin [url]
	3.直接修改config文件
# ssh配置
	1.查看配置 ls ~/.ssh 如果有id_rsa id_rsa.pub两个文件表示已经配置了ssh
	2.生成ssh key文件，执行ssh-keygen -t rsa -C "xxx.xxx.com"; 
	    - t 指定密钥类型，默认是 rsa ，可以省略
	    -C 设置注释文字，比如git的地址。
	    -f 指定密钥文件存储文件名，我们省略了命令执行的时候会让你选择文件名，直接回车就会保存在默认的位置。
	    然后会让你输入两次密码，最后出现 key fingerprint和 key's randomart 就表示创建成功了。
	3.将ssh key添加到git中， vi id_rsa.pub 然后复制文件内容，进入git页面，个人设置，SSH Keys设置页面，在Key文本框中输入复制的内容，然后点Add Key按钮完成添加。
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
### canvas识别图片颜色
```
1.页面上放置一个dispplay:none的canvas标签
2. let canvas = document.getElementById("mycanvas");
   //下面是vue中读取banners图片颜色
   let $this = this;
   for (var i = 0; i < $this.banners.length; i++) {
      // let img = imgs[i];
      $this.getImgColor(canvas, i, $this);
    }
3.//获取图片颜色
    getImgColor(canvas, index, $this) {
      var img = new Image();
      img.crossOrigin = "";//处理canvas图片跨域问题
      img.src = $this.banners[index].src;
      img.onload = function() {
        canvas.width = img.width;
        canvas.height = img.height;
        var context = canvas.getContext("2d");
        context.drawImage(img, 0, 0);
        // 获取像素数据
        let data1 = context.getImageData(0, 0, 1, 1).data;
        let data2 = context.getImageData(
          img.width - 1,
          img.height - 1,
          img.width,
          img.height
        ).data;
        // 取所有像素的平均值
        let r1 = 0,
          r2 = 0,
          g1 = 0,
          g2 = 0,
          b1 = 0,
          b2 = 0;
        var index1 = 0;
        // 取开始像素的颜色
        r1 += data1[index1 * 4 + 0];
        g1 += data1[index1 * 4 + 1];
        b1 += data1[index1 * 4 + 2];

        // 将最终的值取整
        r1 = Math.round(r1);
        g1 = Math.round(g1);
        b1 = Math.round(b1);
        var index2 = 0;

        r2 += data2[index2 * 4 + 0];
        g2 += data2[index2 * 4 + 1];
        b2 += data2[index2 * 4 + 2];

        // 将最终的值取整
        r2 = Math.round(r2);
        g2 = Math.round(g2);
        b2 = Math.round(b2);
        let color1 = "rgb(" + r1 + "," + g1 + "," + b1 + ")";
        let color2 = "rgb(" + r2 + "," + g2 + "," + b2 + ")";
        //rgb转16进制 位运算
        // const color = ((r << 16) | (g << 8) | b).toString(16);
        let style = "linear-gradient(to right," + color1 + "," + color2 + ")";
        $this.banners[index].bc = style;
      };
4. // 取所有像素的平均值（以下获取图片颜色主色方法）
                let r = 0,
                    g = 0,
                    b = 0;
                // 取所有像素的平均值
                for (let row = 0; row < img.height; row++) {
                    for (let col = 0; col < img.width; col++) {
                        r += data[(img.width * row + col) * 4]
                        g += data[(img.width * row + col) * 4 + 1]
                        b += data[(img.width * row + col) * 4 + 2]
                    }
                }
                // 求取平均值
                r /= img.width * img.height
                g /= img.width * img.height
                b /= img.width * img.height

                // 将最终的值取整
                r = Math.round(r)
                g = Math.round(g)
                b = Math.round(b)

```
### koa2安装及启动
```
1.安装koa-generator
npm i -g koa-generator
2.创建koa2项目
koa2 test[项目名称]
3.初始化
cd test
npm i
4.启动
npm run start
5.连接mysql
	安装sequelize
	npm install sequelize --save
	安装 mysql ， mysql2模块
	npm install mysql mysql2 --save
	

```
