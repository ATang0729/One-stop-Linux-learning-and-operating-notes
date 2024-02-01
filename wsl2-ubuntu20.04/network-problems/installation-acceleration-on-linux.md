# 🌐 Installation Acceleration on Linux

## How to accelerate the installation by apt/apt-get

Recommended reference: [Ubuntu20.04更换国内镜像源（阿里、网易163、清华、中科大）](https://midoq.github.io/2022/05/30/Ubuntu20-04%E6%9B%B4%E6%8D%A2%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F%E6%BA%90/)

However, while some installation could be accelerated, some packages couldn't be found in Chinese mirror sources. SO it's recommended to backup the original setting file `source.list`.

## How to accelerate the installation by conda

Append the following code in `~/.condarc`

```
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
ssl_verify: true
```

For more Chinese mirror source, refer to: [conda换源](https://zhuanlan.zhihu.com/p/87123943)

## How to accelerate the installation by pip

Use the following code swith set mirror source in terminal:

```
# 清华源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

Use the following code swith back to default source in terminal:

```
pip config unset global.index-url
```

For more Chinese mirror source, refer to: [修改pip 源为国内源](https://juejin.cn/post/7141566114412101662)
