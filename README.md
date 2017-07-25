# linux-swagger-php
linux下安装swagger+php
以上的项目是已经配置完成了的，只需要下载下来配置域名访问（xxx.com/swagger-ui/dist/index.html）这是swagger-ui前台文档展示页面。此demo全部基于linux！

第一种情况：下载swagger自己搭建服务端，客户端 //双斜杠为注释结束说明，请忽略

           php服务端配置 swagger-php目录下的配置
           第一步：mkdir sw //在网站目录下新建sw并将xxx.com域名解析，我这里用的apache，修改httpd.conf讲xxx.com解析到sw目录
          
           第二步：cd sw   //进入sw目录
          
           第三步：mkdir // 新建你的api目录，也就是你的接口代码目录
          
           第四步：git clone https://github.com/swagger-api/swagger-ui.git  //下载swagger前端ui，也就是doc文档页面
                  git clone https://github.com/zircote/swagger-php.git     //下载swagger服务端，用于生成swagger.json
                  //此时你的sw目录下应该有这三个目录
                  ./api
                  ./swagger-php
                  ./swagger-ui
           
           第五步：cd swagger-php // 进入服务端使用composer安装更新所需组件如果未安装composer请先安装：http://jingyan.baidu.com/article/2a138328969f8d074a134f01.html
           
           第六步：mkdir json_docs // 进入swagger-php新建json_docs用于存放swagger.json. swagger.json是整个api文档的核心，需要生成它才能在前端浏览
           
           第七步：composer update // 前提是你已经安装了composer 这里用于更新swagger所需组件 composer是一种新的项目管理方式类似于java的maven
                                  // composer update更新完成后，会在你的swagger-php目录下新增一个vendor目录存放的是一写swagger运行所需要的一些类库
           
           第八步：php ./bin/swagger ../api -o json_docs  //在swagger-php中配置生成swagger.json，api目录可以根据你真是的代码目录进行更改
                                                         //此时会在你的swagger-php/json_docs目录下生成一个swagger.json这个json是整个文档的核心，没有该json就无法查看！如果修改api文档和注释需要重新生成swagger.json 
                                                         
                                                         
                                                         
           html客户端配置 swagger-ui 下 的配置 
           第九步：cd ../ //回到sw目录
           
           第十步：cd swagger-ui // 进入swagger-ui目录
           
           第十一步： cd dist // 在swagger-ui目录下找到dist目录进入dist目录发现有个index.html
           
           第十二步： vim index.html //在/sw/swagger-ui/dist/ 下找到index.html修改配置，引入刚刚我们生成的swagger.json文件
                                    // 找到url配置，这里他配置的是swagger自己的json这里我们需要配置我们自己api站点的域名xxx.com改成你自己的域名即可
                                    //window.onload = function() {
                                      // Build a system
                                      const ui = SwaggerUIBundle({
                                       // url: "http://petstore.swagger.io/v2/swagger.json",
                                        url: "http://xxx.com/swagger-php/json_docs/swagger.json", //将这里的xxx.com修改成你自己最先配置的域名即可
                                        dom_id: '#swagger-ui',
                                        deepLinking: true,
                                        presets: [
                                          SwaggerUIBundle.presets.apis,
                                          SwaggerUIStandalonePreset
                                        ],
                                        plugins: [
                                          SwaggerUIBundle.plugins.DownloadUrl
                                        ],
                                        layout: "StandaloneLayout"
                                      })

                                      window.ui = ui
                                    }
           第十三步：访问：http://xxx.com/swagger-ui/dist/index.html //xxx.com换成你自己的域名
           
           
                
                
第二种情况：下载我的demo直接安装 
           第一步：mkdir sw   //在api站点更目录新建sw木库 修改apache 或者nginx 将你的域名xxx.com解析到sw目录下
                             // 我这里是apache大概是vim httpd.conf后大概是这样配置的：
                             <VirtualHost *:80>
                                  ServerAdmin 2644389987@qq.com
                                  DocumentRoot /www/sw
                                  ServerName api.bubucom.com
                              </VirtualHost>

           第二步：git clone xxxx //下载我的demo直接放进sw目录里，此时sw下的目录下应该有三个文件夹 
                                 // ./api //api为你自己的api代码目录里面我放了两个demo文件，一个Swagger.php 这是swagger文档的描述基本例子 demo.class.php这是我自己写的一个swagger注释api。
                                 // ./swagger-ui
                                 // .swagger-php
           第三步：访问：http://api.bubucom.com/swagger-ui/dist/index.html // 即可查看你api文档了。
          


注意：执行上述操作前需要先安装composer
     xxx.com为你自己的域名
     另外注意：每次修改api文档的注释后需要重新生成新的swagger.json。命令：php ./bin/swagger ../api -o json_docs
                
具体swagger注释写法请参考官网教程：https://swagger.io/ 希望对你有帮助
           
           
