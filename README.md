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
### canvas识别图片颜色
```
1.页面上放置一个dispplay:none的canvas标签，内部放置要识别颜色的图片img
2. let imgs = document.querySelectorAll(".imgColor");//获取所有图片
   let canvas = document.getElementById("mycanvas");
   for (var i = 0; i < imgs.length; i++) {
     let img = imgs[i];
     getImgColor(canvas, img, i, $this);
   }
3.//获取图片颜色
    getImgColor(canvas, img, index, $this) {
      img.onload = function() {
        canvas.width = img.width;
        canvas.height = img.height;
        var context = canvas.getContext("2d");
        context.drawImage(img, 0, 0);
        // 获取像素数据
        let data = context.getImageData(0, 0, img.width, img.height).data;
	/* 以下获取图片头尾两点的颜色 */
        let r1 = 0,
          r2 = 0,
          g1 = 0,
          g2 = 0,
          b1 = 0,
          b2 = 0;
        // 索引值获取方式：纵坐标(y)*图像宽度(img.width)+横坐标(x)
        var index1 = 0 * img.width + 0;
        // 取开始像素的颜色
        r1 += data[index1 * 4 + 0];
        g1 += data[index1 * 4 + 1];
        b1 += data[index1 * 4 + 2];

        // 将最终的值取整
        r1 = Math.round(r1);
        g1 = Math.round(g1);
        b1 = Math.round(b1);

        var index2 = 0 * img.width + img.width;

        r2 += data[index2 * 4 + 0];
        g2 += data[index2 * 4 + 1];
        b2 += data[index2 * 4 + 2];

        // 将最终的值取整
        r2 = Math.round(r2);
        g2 = Math.round(g2);
        b2 = Math.round(b2);
        let color1 = "rgb(" + r1 + "," + g1 + "," + b1 + ")";
        let color2 = "rgb(" + r2 + "," + g2 + "," + b2 + ")";
        //rgb转16进制 位运算
        // const color = ((r << 16) | (g << 8) | b).toString(16);
        let style = "linear-gradient(to right," + color1 + "," + color2 + ")";
        $this.banners[index].bc = style;//vue中根据获取的颜色修改背景渐变色
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
