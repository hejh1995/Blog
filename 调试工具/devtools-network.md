1. 面板：
![image](https://github.com/hejh1995/project-img/blob/master/1.png)
2. 截取加载瞬间；
![image](https://github.com/hejh1995/project-img/blob/master/1.png)
- 当鼠标悬浮在一张截图上时，下面的请求表格面板上出现了这张截图加载时的时间；
- 点击一张截图时，请求表格面板也会显示相应时间内加载的资源及其信息；
- 双击一张截图，可以查看这张截图的大图，可通过左右键进行切换。
3. 过滤：
- 过滤文本域：
  - 直接输入字符串，可以过滤 出 哪些资源名称中包含相应字符串的资源。
  - domain：刷选来自特定域的请求
  - has-response-header：刷选 HTTP 返回值包含特定头部信息的请求
  - is：可以用 is:running 查看 WebSocket 资源
  - larger-than：筛选文件大小超过特定数字的请求，默认单位是 byte
  - method：刷选特定 HTTP 请求方法的请求
  - mime-type：刷选特定 MIME 类型的请求
  - mixed-content：有 mixed-content:all 和 mixed-content:displayed 两种
  - scheme：刷选特定 scheme 的请求
  - set-cookie-domain：刷选特定的 HTTP 返回头部的 set-cookie 属性的请求
  - set-cookie-name：也是对返回的 HTTP 头部中某个属性进行刷选的关键词
  - set-cookie-value：同上
  - status-code：对请求的状态值进行刷选
  - 还有几点需要注意一下：1) 冒号后面不能有空格；2) 大小写敏感。
