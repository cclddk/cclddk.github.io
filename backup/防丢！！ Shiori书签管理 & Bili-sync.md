友人推荐了一款本地nas存储的书签工具，可实现对网页的缓存，防止页面丢失后找不到。
Win系统的docker直接拉取镜像，运行时只需配置页面存储位置。

<img width="770" height="1143" alt="Image" src="https://github.com/user-attachments/assets/51d56a6c-5a25-4ce2-95d3-21bfcb432de6" />

<img width="770" height="1143" alt="Image" src="https://github.com/user-attachments/assets/d98187f4-a511-485c-8ad1-61ff3f7d8381" />

<img width="532" height="654" alt="Image" src="https://github.com/user-attachments/assets/22417a87-d634-4d64-a67f-78ec6b373533" />
可在书签信息中保存该网页的账号密码信息，本地化存储。



微信公众号刷到哔哩哔哩视屏缓存工具，可缓存收藏夹/合计/投稿/稍后再看/UP主等，防丢！

<img width="2492" height="1202" alt="Image" src="https://github.com/user-attachments/assets/d8f11ed3-2984-4f26-9a68-6b2bdf25e208" />

<img width="2220" height="1213" alt="Image" src="https://github.com/user-attachments/assets/f36d88bd-06fd-48c2-90e4-74b48631a22a" />

<img width="2340" height="1189" alt="Image" src="https://github.com/user-attachments/assets/cf815787-400f-4571-8927-57ba9790bea8" />本地打开后有弹幕，好评一下！要是也能缓存评论区就好了

ps：报错数据库锁定时，按下面方法解决即可！

<img width="929" height="324" alt="Image" src="https://github.com/user-attachments/assets/22dcc9ce-5ff1-48a0-af85-b917f4061c62" />

services:
  bili-sync-rs:
    # 不推荐使用 latest 这种模糊的 tag，最好直接指明版本号
    image: amtoaer/bili-sync-rs:latest
    restart: unless-stopped
    network_mode: bridge
    # 该选项请仅在日志终端支持彩色输出时启用，否则日志中可能会出现乱码
    tty: true
    # 非必需设置项，推荐设置为宿主机用户的 uid 及 gid (`$uid:$gid`)
    # 可以执行 `id ${user}` 获取 `user` 用户的 uid 及 gid
    # 程序下载的所有文件权限将与此处的用户保持一致，不设置默认为 Root
    user: 1000:1000
    hostname: bili-sync-rs
    container_name: bili-sync-rs
    # 程序默认绑定 0.0.0.0:12345 运行 http 服务
    # 可同时修改 compose 文件与 config.toml 变更服务运行的端口
    ports:
      - 12345:12345
    volumes:
      - H:/docker/bilibili/config:/app/.config/bili-sync  # 配置文件路径
      - H:/docker/bilibili/media:/videos  # 视频存储路径
    logging:
      driver: "local"