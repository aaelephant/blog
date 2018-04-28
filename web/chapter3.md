#React 项目部署到tomcat

1. 运行npm run build命令生成build编译后的文件
2. 把build放到tomcat下。
3. 访问时是空白界面

* 这里的问题，需要改一下react-scripts/config/paths.js配置
 绝对路径改为相对路径，如图中圈中的地方。
![](assets/react-scripts-path.png)
