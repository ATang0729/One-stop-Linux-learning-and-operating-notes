# 🌐 Network Problems

## How to clone a github repository

:flag\_cn:Similar to [the network problems when visit websites like Google in VM](../../oracle-vm-virtualbox/network-problems.md), Chinese user couldn't successfully connect with Github so as to clone a repository. Here are some solutions:

1. through a proxy server
   * **(**_**Highly recommended this for everyone!**_**)** For others, refer to this: [How to use proxy in WSL? · issue #2122 · microsoft/WSL github.com](https://github.com/microsoft/WSL/issues/2122)
   * (❤️‍🩹_this doesn't work for me_) For Chinese, refer to this: [拉取github项目的时候，git clone https 失败，需要设置 wsl2 使用 windows 上的代理](https://blog.csdn.net/Desecrater/article/details/133581868)
     * _**NOTE**: If this solution doesn't work, maybe this will help you:_ [_WSL cannot use proxy with networkingMode=mirrored · issue #10794 · microsoft/WSL github.com_](https://github.com/microsoft/WSL/issues/10794)
2. through a mirror website
   * use `git clone https://mirror.ghproxy.com/<your target repository https url>`&#x20;
   * For ways of cloning a private repo or use wget & curl to download file, please refer to the reference: [github proxy 代理加速](https://mirror.ghproxy.com/) _(I promise it's quite esay)_
