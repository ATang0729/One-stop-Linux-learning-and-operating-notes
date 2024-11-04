---
description: 'Reference: https://www.bilibili.com/video/BV1j2421o77K/'
icon: apple
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Install a macOS VM in a WSL-based Docker

This is an ultimate matryoshka Mac system, which I installed into a Linux subsystem running on Windows inside a Docker container. It's a combination of three major operating systems all at once. We can use this system to try out some Mac-specific software, develop cross-platform software, test compatibility, and more.

In this page, let's take a look at how to set up this interesting system. For this project, I'm using [Docker OSX](https://github.com/sickcodes/Docker-OSX), whichc cows you to quickly start a MacOS environment using Docker. However, this project has fairly high hardware requirements, and a Linux mini-computer's performance may not be sufficient. So this time, I'm going to run Docker on my Windows computer.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Architecture Diagram (From: <a href="https://www.bilibili.com/video/BV1j2421o77K/">https://www.bilibili.com/video/BV1j2421o77K/</a>)</p></figcaption></figure>

## First, initial setup for Docker-OSX to run on Windows

Go to `C:/Users/<Your_Name>/.wslconfig` and add `nestedVirtualization=true` to the end of the file (If the file doesn't exist, create it). For more information about the `.wslconfig` file check [this link](https://docs.microsoft.com/en-us/windows/wsl/wsl-config#wslconfig). Verify that you have selected "Show Hidden Files" and "Show File Extensions" in File Explorer options. The result should be like this:

```
[wsl2]
nestedVirtualization=true
```

This step is to allow nesting of virtual machines.

:warning:If you are running your WSL, don't forget to run `wsl --shutdown` to activate the above config.

## Second, install a Docker desktop

:link:Downloading links:

* :flag\_gb: [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
* :flag\_cn: [https://github.com/tech-shrimp/docker\_installer/releases](https://github.com/tech-shrimp/docker\_installer/releases)

## Third, modify configuration

### Modification

Insure that the options, framed in the figures below, are selected.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>select "Use the WSL 2 based engine"</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>select "Enable integration with my default WSL distro" and your default WSL, then check "Apply &#x26; restart"</p></figcaption></figure>

### Verification

Enter `docker ps` in your WSL to check whether you can use docker in your WSL.

You success if you get the following return:

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

check if KVM is enabled by using the `kvm-ok` command. The output should look like this:

```
INFO: /dev/kvm exists
KVM acceleration can be used
```

## Fourth, install mac OS in docker

> Choose the corresponding image of mac OS from here: [https://github.com/sickcodes/Docker-OSX?tab=readme-ov-file#technical-details](https://github.com/sickcodes/Docker-OSX?tab=readme-ov-file#technical-details)

For an example, I choose Ventura (2.36GB).

* _**Code for**_ :flag\_gb:**:**

<pre class="language-sh"><code class="lang-sh"><strong>docker run -it \
</strong>    --device /dev/kvm \
    -p 50922:10022 \
    -e "DISPLAY=${DISPLAY:-:0.0}" \
<strong>    -v /mnt/wslg/.X11-unix:/tmp/.X11-unix \
</strong>    -e GENERATE_UNIQUE=true \
    -e MASTER_PLIST_URL='https://raw.githubusercontent.com/sickcodes/osx-serial-generator/master/config-custom.plist' \
    -e SHORTNAME=ventura \
    sickcodes/docker-osx:latest

# docker build -t docker-osx .
</code></pre>

* _**Code for**_ :flag\_cn::

```sh
docker run -it \
    --name macos \
    --device /dev/kvm \
    -p 50922:10022 \
    -e "DISPLAY=${DISPLAY:-:0.0}" \
    -v /mnt/wslg/.X11-unix:/tmp/.X11-unix \
    -e GENERATE_UNIQUE=true \
    -e "MASTER_PLIST_URL=https://raw.githubusercontent.com/sickcodes/osx-serial-generator/master/config-custom.plist" \
    registry.cn-hangzhou.aliyuncs.com/shrimp-images/docker-osx:ventura

# docker build -t docker-osx .
```

> _<mark style="color:red;">**ERROR**</mark>_: wsl: 检测到 localhost 代理配置，但未镜像到 WSL。NAT 模式下的 WSL 不支持 localhost 代理
>
> _<mark style="color:green;">**SOLUTION**</mark>_: \[[_**Reference**_](https://blog.csdn.net/weixin\_50925658/article/details/135111897)]
>
>
>
> _<mark style="color:red;">**ERROR**</mark>_: curl: (7) Failed to connect to raw.githubusercontent.com port 443 after 16 ms: Couldn't connect to server
>
> _<mark style="color:green;">**SOLUTION1**</mark>_: add the following codes into the loacal _**host**_ file (`sudo vim /etc/hosts`)\[[_**Reference**_](https://stackoverflow.com/questions/59572626/curl-7-failed-to-connect-to-raw-githubusercontent-com-port-443-connection-re)]:
>
> ```
> 185.199.108.133 raw.githubusercontent.com
> 185.199.109.133 raw.githubusercontent.com
> 185.199.110.133 raw.githubusercontent.com
> 185.199.110.133 raw.githubusercontent.com
> ```
>
> <mark style="color:green;">**🌟**</mark>_<mark style="color:green;">**SOLUTION2**</mark>_: set proxy for wsl
>
> ```sh
> docker run -it \
>     --name macos \
>     --device /dev/kvm \
>     -p 50922:10022 \
>     -e "DISPLAY=${DISPLAY:-:0.0}" \
>     -v /mnt/wslg/.X11-unix:/tmp/.X11-unix \
>     -e GENERATE_UNIQUE=true \
>     -e "MASTER_PLIST_URL=https://raw.githubusercontent.com/sickcodes/osx-serial-generator/master/config-custom.plist" \
>     -e http_proxy=http://<your_proxy_server>:<your_port> \
>     -e https_proxy=http://<your_proxy_server>:<your_port> \
>     registry.cn-hangzhou.aliyuncs.com/shrimp-images/docker-osx:ventura
>
> # docker build -t docker-osx .
> ```
>
> :warning:_**NOTE**_: \<your\_proxy\_server> can be accessed after _**Enable LAN connection**_ on your proxy client (vEthernet (WSL (Hyper-V firewall))).
