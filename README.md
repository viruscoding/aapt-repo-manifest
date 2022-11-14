# aapt-repo-manifest

编译最新版platform-tools

## for mac

创建大小写敏感磁盘

```
hdiutil create -volname "android" -type SPARSE -fs 'Case-sensitive Journaled HFS+' -size 10g android.dmg
```

挂载

```
hdiutil attach android.dmg.sparseimage -mountpoint /Volumes/android
```

卸载

```
hdiutil detach /Volumes/android
```

## for linux(Ubuntu 16.0.4)

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install openjdk-8-jdk
sudo apt-get install cmake
sudo apt-get install clang
sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip
```

## 构建

安装repo

```
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

初始化repo项目

```
#进入工作目录
cd /Volumes/aapt
#如果存在repo bundle下载不下来的情况，请使用下面的命令进行手动clone
#git clone http://mirrors.ustc.edu.cn/aosp/git-repo.git/ .repo/repo
#初始化并同步源码树，约3G
repo init -u https://github.com/viruscoding/aapt-repo-manifest.git -b platform-tools-33.0.3 --depth 1
repo sync -j8
```

## 补全依赖

> https://android.googlesource.com/platform/manifest/+/refs/heads/platform-tools-33.0.3/default.xml

- 添加build模块， 同步后执行`. source/envsetup.sh`
- 然后执行`mmm -h`命令， 缺依赖就在default.xml中补
- 添加aapt2相关依赖，参考`https://github.com/Lzhiyong/android-sdk-tools`


