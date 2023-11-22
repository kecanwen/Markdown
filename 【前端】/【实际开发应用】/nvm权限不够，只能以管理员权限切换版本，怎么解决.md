如果您在使用 nvm 切换版本的时候遇到权限问题，可以考虑以下两种方法解决：

1. 修改 nvm 的默认安装路径

nvm 会将所有的 Node.js 版本安装到默认的路径 `~/.nvm/versions/node` 下，如果这个目录没有写权限，则可能会导致权限问题，此时可以考虑将 nvm 的默认安装路径修改成有写权限的目录。

具体操作步骤：

1. 打开终端，切换到您想要安装 nvm 的目录。
2. 使用 git 克隆 nvm 仓库：`git clone https://github.com/nvm-sh/nvm.git`
3. 将 nvm 目录的所有者改为当前用户：`sudo chown -R $USER:$USER nvm`
4. 在当前用户的 home 目录中添加一个 `.nvm` 目录：`mkdir ~/.nvm`
5. 修改 nvm 的安装路径：`export NVM_DIR="/home/<user_name>/.nvm"`
6. 将上一步中的 `<user_name>` 改为当前用户的用户名。
7. 在当前终端窗口中执行 `source nvm/nvm.sh` 命令，使 nvm 环境生效。
8. 修改 nvm 安装目录的权限

如果您已经安装了 nvm，并且遇到了权限问题，可以考虑修改 nvm 安装目录的权限。具体操作步骤：

1. 找到您的 nvm 目录。默认情况下，nvm 的目录为 `~/.nvm/`。
2. 使用以下命令将 nvm 目录的权限修改为当前用户：`sudo chown -R $USER:$USER ~/.nvm/`
3. 使用以下命令将 nvm 目录的权限修改为当前用户和其他人可读写：`sudo chmod -R 755 ~/.nvm/`
4. 在当前终端窗口中执行 `source ~/.bashrc` 命令，使修改后的权限生效。

总之，以上两种方法都可以解决 nvm 权限不够的问题，您可以根据自己的实际情况进行选择。