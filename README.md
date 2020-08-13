### 命令说明
  - 打包测试环境
    - npm run build:dev
  - 打包生产环境
    - npm run build:huawei
  - 本地开发环境
    - npm run dev
  - 生产开发环境
    - npm run dev:huawei
    
### 目录说明
  - page/index                  会员网站
  - page/activate               EDM邮件激活模板
  - page/activationSuccessful   EDM邮件激活成功页
  - page/privacyPolicy          华为隐私协议
  - page/termsOfUse             华为用户手册
  - page/registrationForm       华为注册表单
  - page/SouthAfricaActivation  EMD邮件南非激活模板
    
### dev环境配置代理服务器
  - /src/config/proxy.config 配置代理规则

### [原脚手架demo地址](https://github.com/Blubiubiu/webpack4_mpa_demo)

### EDM改造变量插入说明（模板插入约定变量，由后台替换为具体值）
  * ![edm图片说明](.//edm.jpg)
    - 1： {{registerUrl}}: 该edm邮件发布于生产环境
    - 2： [Customer Name]: 接受邮件用户的用户名
    - 3： 用户同意协议才可以激活，作为模板上传时，需注释这一部分代码。
    - 4： {{registerUrl}}: 该edm邮件发布于生产环境
    
### EDM说明
  1. EDM在邮件中会过滤掉所有的js脚本及link标签，所以需删除所有的js、css外部资源引用
  2. 结构使用table布局，更好的兼容
  3. 样式使用行内
  4. 图片有时候会被过滤或默认禁用图片请求（例如outlook客户端及垃圾箱），关键按钮最好使用文本撑开的形式调整样式
  5. 由于EDM会过滤脚本，所有记录邮件打开的请求需要在顶部插入一个img标签，通过src去发起请求
  6. 图片资源需要使用外网能访问的url，不可以使用本地图片（可以上传到文件服务器）
  7. 项目中监控的EDM页面同时用于：
     - EDM推送模板（即上传到后台管理的模板管理），此时需要先注释同意协议的勾选部分，并不需要引用js脚本
        - PS：原因是EDM过滤js脚本，无法获取单选框的勾选状态。 所以需要跳转至浏览器再进行后续操作
     - 作为生产环境发布（会打包发布到生产环境），用于EDM模板点击激活（{{registerUrl}}）时跳转至该页面
        - PS：这里需要放开同意协议勾选部分的注释，js脚本打包的时候会自动引入无需手动引用，具体需要处理的的参数机接口调用参考`src/pages/activate`
  
  
