# debain11本地兼容编译教程（默认root用户）
## 一、环境搭建
### 1. net版本：要求10.0.0或更高。 输入dotnet --info查看版本
若版本错误，安装10.0.0版本可使用使用微软官方安装脚本

wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh

chmod +x dotnet-install.sh

./dotnet-install.sh --channel 10.0

配置环境变量（.bashrc文件建议默认选择root目录下的）

echo 'export DOTNET_ROOT=$HOME/.dotnet' >> ~/.bashrc

echo 'export PATH=$PATH:$DOTNET_ROOT:$DOTNET_ROOT/tools' >> ~/.bashrc

source ~/.bashrc

### 2. node版本和npm版本：分别要求20.19.0和10.0.0或更高。分别输入node --version和npm --version查看版本
若版本错误，彻底卸载当前的Node.js和npm，安装适合的版本

通过 apt 移除 nodejs 和 npm 包及其配置文件

apt-get remove --purge nodejs npm -y

移除不再需要的依赖包

apt-get autoremove -y

清理 apt 缓存

apt-get autoclean

手动删除可能残留的全局目录和文件（重要）

rm -rf /usr/local/bin/node

rm -rf /usr/local/bin/npm

rm -rf /usr/local/bin/npx

rm -rf /usr/local/lib/node_modules

rm -rf /usr/local/include/node

rm -rf /usr/local/share/doc/node

删除当前用户目录下的 npm 和 node 相关配置与缓存

rm -rf ~/.npm

rm -rf ~/.npmrc

rm -rf ~/.node-gyp

rm -rf ~/.node_repl_history

安装 Node.js 20.x

更新包索引并安装依赖工具

apt update

apt install -y curl gnupg2 ca-certificates

下载并运行 NodeSource 针对 20.x 版本的安装脚本

这个脚本会自动添加正确的软件源并更新包列表

curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -

安装 Node.js 和 npm

apt install -y nodejs

将 npm 升级到最新稳定版

npm install -g npm@latest

### 3. libstdc++：要求是libstdc++.so.6版本。
重新安装前端依赖，进入前端目录，删除 node_modules 和 package-lock.json，然后重新安装

cd /opt/Kavita_oldcpu-oldcpu/UI/Web

rm -rf node_modules package-lock.json

npm cache clean --force

npm install --legacy-peer-deps
