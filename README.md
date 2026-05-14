# 婚礼电子请帖 H5

这是一个纯静态婚礼电子请帖页面，适合通过 GitHub Pages 免费部署。项目不需要后端、数据库、登录、构建工具或付费服务，也不会收集访客信息。

## 文件结构

```text
/
├── index.html
├── README.md
├── robots.txt
├── .nojekyll
└── assets/
    ├── invite.jpg 或 invite.png
    ├── music.mp3
    └── 可选图片素材
```

当前仓库没有放入真实婚礼素材时，页面会显示温和的缺图提示，音乐按钮会显示“无音乐”或“点按开启”，不会导致页面崩溃。

## 替换请帖图

将主体电子请帖长图放到 `assets/` 目录，并命名为以下任意一种：

- `assets/invite.jpg`
- `assets/invite.png`

页面会优先读取 `invite.jpg`，如果不存在再尝试读取 `invite.png`。图片会按原始比例以 100% 宽度显示，并支持点击或点击“查看大图”打开预览。

## 替换背景音乐

将背景音乐文件放到：

```text
assets/music.mp3
```

页面会使用 `HTMLAudioElement` 播放，配置为循环播放、预加载，音量约为 0.35。建议使用体积适中的 MP3，避免移动网络下加载太慢。

浏览器、微信内置浏览器、iOS Safari 和 Android Chrome 都可能限制自动播放音乐。页面加载后会先尝试自动播放；如果被拦截，会显示“轻触开启请帖音乐”。用户点击页面、触摸页面或点击音乐按钮后，页面会再次尝试播放。若 `music.mp3` 不存在，按钮会显示“无音乐”。

## 可选素材

以下文件不是必须的。如果存在，页面会自动加载并作为像素小角色展示：

- `assets/pixel-cat.png`
- `assets/pixel-red-panda.png`
- `assets/pixel-sprite-1.png`
- `assets/pixel-sprite-2.png`

分享图可放在：

```text
assets/share.jpg
```

当前页面已经写入基础分享标题和描述。若需要让 `share.jpg` 作为 Open Graph 分享图，请在 `index.html` 的 `head` 中增加：

```html
<meta property="og:image" content="assets/share.jpg">
```

## 本地预览

可以直接双击打开 `index.html` 预览页面。部分浏览器在本地文件模式下会更严格地限制音频播放，这是正常现象。

也可以启动一个本地静态服务，效果更接近 GitHub Pages：

```powershell
python -m http.server 4173
```

然后访问：

```text
http://localhost:4173/
```

## GitHub Pages 部署

推荐使用 GitHub 仓库自带的 Pages 分支部署，不需要额外 workflow：

1. 将本项目提交并推送到 GitHub 仓库。
2. 打开仓库 `Settings`。
3. 进入 `Pages`。
4. `Source` 选择 `Deploy from a branch`。
5. `Branch` 选择 `main`，目录选择 `/root`。
6. 保存后等待 GitHub Pages 生成访问地址。

项目已包含 `.nojekyll`，GitHub Pages 会按普通静态文件发布。

## 隐私和 SEO

这是私人婚礼请帖，项目已经做了以下处理：

- `index.html` 中加入 `meta robots noindex,nofollow`。
- `robots.txt` 设置为拒绝搜索引擎抓取。
- 未接入 Google Analytics、百度统计、广告脚本或任何第三方追踪脚本。
- 不请求位置、相机、麦克风、通讯录等用户隐私权限。
- 地图按钮仅打开腾讯地图地址搜索链接，不上传表单或收集访客信息。

## 维护说明

婚礼信息集中写在 `index.html` 底部脚本的 `config` 对象中，同时页面正文也已同步写入。若要修改新人姓名、时间、地点或地址，请同时检查正文和 `config.address`，避免复制地址和地图搜索仍使用旧地址。
