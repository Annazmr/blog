[Anaconda下载地址](https://www.anaconda.com/products/individual#macos)

检查环境变量： sudo vi ~/.bash_profile

如果环境变量中没有conda那么要手动添加：export PATH="/Users/anaconda3/bin:$PATH"（这里填写自己的安装路径）

刷新环境变量：source ~/.bash_profile

再查看 conda list

## 常用的命令
- 查看conda版本：$ conda --version

- 更新conda版本：$ conda update conda

- 查看都安装了那些依赖库：$ conda list

- 创建新的python环境：$ conda create --name myenv

- 并且还可以指定python的版本：$ conda create -n myenv python=3.7

- 创建新环境并指定包含的库：$ conda create -n myenv scipy

- 并且还可以指定库的版本：$ conda create -n myenv scipy=0.15.0

- 复制环境：$ conda create --name myclone --clone myenv

- 查看是不是复制成功了：$ conda info --envs

- 激活、进入某个环境：$ source activate myenv

- 退出环境：$ source deactivate

- 删除环境：$ conda remove --name myenv --all

- 查看当前的环境列表：$ conda info --envs or $ conda env list

- 查看某个环境下安装的库：$ conda list -n myenv

- 查找包：$ conda search XXX

- 安装包：$ conda install XXX

- 更新包：$ conda update XXX

- 删除包：$ conda remove XXX

- 安装到指定环境：$ conda install -n myenv XXX