# blog-image
用来存储博客文章需要使用的图片

## 下面为你详细介绍 PicGo（以命令行版 PicGo-Core 为例）的完整配置流程，包括图床选择、参数配置、测试验证等步骤：
### 一、准备工作
安装 PicGo-Core（已安装可跳过）
```bash
npm install picgo -g
```

选择并安装图床插件
根据需求安装对应图床的插件，以常用的 GitHub 图床 为例：
```bash
picgo install github-plus  # GitHub 增强插件，支持自定义路径等
```

其他常用插件：
- 阿里云 OSS：picgo install aliyun-oss
- 腾讯云 COS：picgo install tencent-cos
- 七牛云：picgo install qiniu

### 二、配置图床参数
以 GitHub 图床 为例，配置步骤如下：
1. 创建 GitHub 仓库
2. 新建一个公开仓库（如 blog-images），用于存储图片
3. 记住仓库路径：用户名/仓库名（如 username/blog-images）
4. 生成 GitHub 访问令牌
- 打开 GitHub → 点击头像 → Settings → Developer settings → Personal access tokens → Generate new token
- 勾选 repo 权限（必须），生成后复制令牌（仅显示一次，需保存）
5. 配置 PicGo
在命令行输入：
```bash
picgo set uploader  # 进入配置向导
```

按提示操作：
选择上传器：输入 `github-plus` 并回车
依次填写参数：
plaintext
- repo：用户名/仓库名（如 username/blog-images）
- branch：分支名（默认 main 或 master）
- token：刚才生成的 GitHub 令牌
- path：图片存储路径（可选，如 images/2024/）
- customUrl：自定义 CDN 域名（可选，如 https://cdn.jsdelivr.net/gh/用户名/仓库名）

配置完成后，选择 Set as default uploader（设为默认上传器）
### 三、验证配置是否生效
测试上传图片
执行命令上传本地图片（替换为你的图片路径）：
```bash
picgo upload C:\Users\Legion\Pictures\test.jpg
```

成功：会返回图片的在线链接（如 https://cdn.jsdelivr.net/gh/username/blog-images/images/2024/test.jpg）
失败：检查参数是否正确（尤其是 token 和 repo 路径）
查看上传记录
查看历史上传记录：
```bash
picgo list
```

### 四、进阶配置（可选）
修改默认配置
如需修改参数，可重新执行 `picgo set uploader`，或直接编辑配置文件：
配置文件路径：`C:\Users\你的用户名\.picgo\config.json（Windows）`或 `~/.picgo/config.json（Mac/Linux）`
设置快捷键上传（配合剪贴板）
安装剪贴板上传插件：
```bash
picgo install clipboard-upload
```

之后可直接复制图片（如截图），执行命令上传：
```bash
picgo upload
```

与 `Hexo` 集成
在 `Hexo`文章中直接使用上传后的图片链接，例如：
```markdown
![示例图片](https://cdn.jsdelivr.net/gh/username/blog-images/images/2024/test.jpg)
```
