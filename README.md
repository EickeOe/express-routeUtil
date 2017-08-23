# routeUtil使用说明
  ### 用途：
    适用于express框架，自动注入路由配置，避免手动配置等机械操作
  ### 1.引用
    将routeUtil.js放入express项目中，看个人喜好啦，我是放在了root/util目录下
  ### 2.配置
    在express项目根目录新建route.json文件，用于存放routeUtil的配置
    json文件内容：
```javascript
        {
          "class-route-path":boolean,
          "scan-path":string,
          "route-property":string
        }
```
     class-route-path：表示是否启用路由js文件名级的路径,默认为true。
        例如：路由js名为demo.js，则此js中的接口路径为/demo/xxx
     scan-path：表示route目录的文件夹名或相对路径，默认为'routes'。
        例如：我的路由js存放在routes文件夹下，则工具就会扫描routes目录
      route-property：表示工具引用的属性入口，默认为autowired。
        例如：我的路由js设置exports.autowired = {...}，则此工具就会引用autowired自动配置路由
   ### 3.route.js写法
    例如：
        routes/demo.js
```javascript
            exports.autowired = {
                'get' : {
                    '/' : (req, res, next)=>{
                        res.send('demo root');
                    },
                    '/child : (req, res, next)=>{
                        res.send('demo child');
                     }
                },
                'post' : {
            
                }
            };
```
         访问localhost:port/demo/时，展示demo root'
         访问localhost:port/demo/child/时，展示demo child'
   ### 4.加入项目
```javascript
    let route = require('./util/routeUtil');
    app.use(route);
```
    这时，此工具已经加入项目中
