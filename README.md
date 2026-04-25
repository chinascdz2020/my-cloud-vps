________________________________________
第一步：创建一个新的仓库 (Repository)
Codespaces 必须依托于一个仓库才能运行。
1.	在 GitHub 首页（右上角），点击加号 + 图标，选择 New repository。
2.	Repository name: 随便起个名字，比如 my-cloud-vps。
3.	Public/Private: 建议选 Private（私有），这样别人看不到你的服务器配置。
4.	勾选 Add a README file（这能确保仓库不是空的，方便直接创建空间）。
5.	点击底部的绿色按钮 Create repository。
________________________________________
第二步：启动 Codespace 环境
仓库创建好后，你会进入仓库主页。
1.	找到绿色的 <> Code 按钮并点击。
2.	在弹出的菜单中，选择 Codespaces 选项卡。
3.	点击底部的 Create codespace on main。
4.	提示：GitHub 会开始初始化环境，这可能需要 30 秒到 1 分钟。完成后，你会看到一个和 VS Code 一模一样的网页版编辑器。
________________________________________
第三步：进入终端操作
1.	环境启动后，你会看到屏幕下方有一个 Terminal（终端） 窗口（如果没有看到，按快捷键 Ctrl + ` 即可呼出）。
2.	输入sudo su获取root权限：
~~~~~~
sudo su 
~~~~~~
________________________________________
第四步：环境初始化
1. 下载 sing-box 官方程序包
~~~~~~
wget https://github.com/SagerNet/sing-box/releases/download/v1.10.1/sing-box-1.10.1-linux-amd64.tar.gz
~~~~~~
2. 解压安装包
~~~~~~
tar -zxvf sing-box-1.10.1-linux-amd64.tar.gz
~~~~~~
3. 进入程序目录
~~~~~~
cd sing-box-1.10.1-linux-amd64
~~~~~~
________________________________________
第五步：配置
~~~~~~
cat <<EOF > ./config.json
{
  "log": { "level": "info" },
  "inbounds": [{
    "type": "vless",
    "tag": "vless-in",
    "listen": "::",
    "listen_port": 8080,
    "users": [{ "uuid": "6b582416-d36e-4a2f-82ea-a059eb108a22" }],
    "transport": { "type": "ws", "path": "/vless" }
  }],
  "outbounds": [{ "type": "direct", "tag": "direct" }]
}
EOF
~~~~~~
________________________________________
第六步：启动
~~~~~~
./sing-box run -c ./config.json
~~~~~~
 ________________________________________
第七步：权限设置
1.	点击底部的 Ports 标签页。
2.	找到 8080 端口对应的 Local Address（或者右键点击端口选择 Copy Local Address），这才是填入客户端的“地址”。
3.	在 Visibility 那一列，右键点击并将 Private 改为 Public。
 
 配置参数对照表（以 v2rayN 为例）：
 ~~~~~~
•	地址 (Address): 填你的 GitHub 预览域名 (不带 https://)
•	端口 (Port): 443 
•	用户 ID (UUID): 6b582416-d36e-4a2f-82ea-a059eb108a22
•	传输协议 (Network): ws
•	伪装类型 (Header type): none
•	路径 (Path): /vless
•	底层传输安全 (TLS): tls
•	SNI: 填你的 GitHub 预览域名(不带 https://)
~~~~~~
________________________________________
