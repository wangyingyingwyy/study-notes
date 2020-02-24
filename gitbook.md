# 手动构建过程

1. 创建仓库
    * 克隆仓库到本地
    * 创建文件(SUMMART.md必须的，作为左侧目录)
2. 全局安装gitbook-cli脚手架(`npm i -g gitbook-cli`)
3. gitbook build进行构建(把md文件构建为HTML文件)
4. 上传除了_book文件夹之外所有文件
5. 创建分支gh-pages(git checkout -b gh-pages),将_book中的文件上传到这个分支

# 自动化构建过程

#### 先在travis ci官网手动关联项目

1. 创建自动化构建配置文件.travis.yml
    > .tavis.yml文件
    
    ```
    language: node_js
    node_js:
    - "node"

    after_script:
    - gitbook build
    - cd ./_book
    - git init
    - git config user.name "${USER_NAME}"
    - git config user.email "${USER_EMAIL}"
    - git add .
    - git commit -m "publish gitbook"
    - git push --force --quiet "https://${ACC_TOKEN}@${GH_REF}" master:${BRANCH}

    branches:
    only:
        - master
    ```
2. 在自动化构建服务器travis ic上安装gitbook build命令行工具
    - `npm init` (加入package.json文件)
    - 加项目依赖(npm i -D gitbook-cli)
    > "devDependencies": {
    			"gitbook-cli": "^2.3.2"
  		}
3. 填写5个环境变量
>ACC_TOKEN: ab91dce290ca32642b1424bddd8856cbee8acc69

>BRANCH: gh-pages

>GH_REF: github.com/wangyingyingwyy/SPA-novel

>USER_EMAIL:2423457156@qq.com

>USER_NAME: wangyingyingwyy

