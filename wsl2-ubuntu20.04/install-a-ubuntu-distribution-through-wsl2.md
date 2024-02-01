# 🛠 Install a Ubuntu Distribution through WSL2

wsl:star\_struck:In this note, we are going to learn how to install WSL2. If you want to learn about the differences between WSL2 and WSL1, please refer to [this official docs](https://learn.microsoft.com/zh-cn/windows/wsl/compare-versions?source=recommendations). For more information, please refer to [references](install-a-ubuntu-distribution-through-wsl2.md#references).

## Instructions

### Installation

1.  use `wsl --list --online` to view available Linux distributions that can be downloaded through the online store

    <figure><img src="../.gitbook/assets/wsl-list.png" alt=""><figcaption><p>wsl --list --online</p></figcaption></figure>
2.  use `wsl --install -d <distribution name>` to install the certain distribution and this well a few minutes for the first time. For example, in this note, Harry installed Ubuntu-20.04, for which he used `wsl --install -d Ubuntu-20.04`. If you counter some errors, please refer to [Additions](install-a-ubuntu-distribution-through-wsl2.md#additions)

    <figure><img src="../.gitbook/assets/install wsl.png" alt=""><figcaption><p>Successful installation</p></figcaption></figure>

### Verification

1.  use `wsl -l -v` to view the installed distributions' name, state and version.

    <figure><img src="../.gitbook/assets/wsl -l -v.png" alt=""><figcaption></figcaption></figure>
2. Once installed, there are several ways to run a Linux distribution. Here are some recommend ways:
   1.  Typing the name of the installed distribution in the _Windows Start menu_. For example, "Ubuntu".  This opens Ubuntu in its own console window.

       <figure><img src="../.gitbook/assets/start menu.png" alt=""><figcaption><p>search "Ubuntu" in the Windows Start menu</p></figcaption></figure>
   2.  Typing the name of the installed distribution in _cmd_ or _Windows Powershell_. Type `wsl` or `wsl.exe` will open the default distribution. To change default setting, refer to [this](https://learn.microsoft.com/zh-cn/windows/wsl/install#check-which-version-of-wsl-you-are-running).



       _**NOTE**: If you have installed visual studio code, you can type `code .` in the cli of Ubuntu to connect Linux server with VS Code server._

       <figure><img src="../.gitbook/assets/vsc.png" alt=""><figcaption><p>connect VSC with linux server</p></figcaption></figure>
   3. For more information, refer to [this](https://learn.microsoft.com/zh-cn/windows/wsl/install#ways-to-run-multiple-linux-distributions-with-wsl).

### Migration

By default, WSL and Ubuntu will be installed on `C:\`. In this section, you will learn how to transfer these two parts to other disks.

1. **Deactivate**: use `wsl -l --all -v` to view the states of all distributions and use `wsl --shutdown` to stop the running ones&#x20;
2. **Backup**: use `wsl --export <name> <backup path>`
3. **Unregister**: use `wsl --unregister <name>`
4.  **Restore**: use `wsl --import <name> <restore dir> <backup path> [--version 2]` and you can see the VHDX file of Ubuntu present in your restore dir. (see the below figure)

    <figure><img src="../.gitbook/assets/restore.jpg" alt=""><figcaption><p>Successfully migrated</p></figcaption></figure>
5.  **Set default user**: after importing and starting the Ubuntu backup, you may find the default user is root. Although you can change the default user of a distribution by `<distribution name> config --default-user <user name>` in cmd, _it doesn't work for imported distributions_. But you can do that by modifying `/etc/wsl.conf` in Ubuntu (see the figure below) \[[Reference](https://learn.microsoft.com/zh-cn/windows/wsl/wsl-config#wslconf)]. Besides, you can cahnge user temporarily by using `su <user name>` in Ubuntu or `wsl --user <user name>` in cmd

    <figure><img src="../.gitbook/assets/set default user.png" alt="" width="530"><figcaption></figcaption></figure>

## Additions

1.  If you counter error 0x800701bc, the tutorials below are recommended for your&#x20;

    <figure><img src="../.gitbook/assets/Error 0x800701bc.png" alt=""><figcaption><p>Error: 0x800701bc</p></figcaption></figure>

    1. In Chinese: [win10 WSL2问题解决WslRegisterDistribution failed with error: 0x800701bc](https://blog.csdn.net/qq\_18625805/article/details/109732122)
    2. In English: [\[Solved\] WslRegisterDistribution Failed with Error: 0x800701bc](https://www.partitionwizard.com/partitionmagic/wslregisterdistribution-failed-with-error-0x800701bc.html)
2.  If you counter error 0x80370102, the tutorials below are recommended for your&#x20;

    <figure><img src="../.gitbook/assets/Error 0x80370102.png" alt=""><figcaption><p>Error: 0x80370102</p></figcaption></figure>

    1. In Chinese: [wsl2的Error 0x80370102 解决方案](https://zhuanlan.zhihu.com/p/147233604)
    2. In English: [Fix: WSL Register Distribution Error 0x80370102 Windows ...](https://www.partitionwizard.com/partitionmagic/wslregisterdistribution-failed-with-error-0x80370102.html)

## References

* In Chinese: [如何使用 WSL 在 Windows 上安装 Linux | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/install)
* In English: [How to install Linux on Windows with WSL | Microsoft Learn](https://learn.microsoft.com/en-gb/windows/wsl/install)
