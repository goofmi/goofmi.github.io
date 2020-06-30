---
title: Ubuntu20.04安裝baidu输入法
date: 2020-06-29 20:40:55
tags: ubuntu
---

## 下载安装包

[百度大胆说出： 我们来了 久等了](https://srf.baidu.com/site/guanwang_linux/index.html)

    mkdir /tmp/baidu_pinyin
    wget  https://imeres.baidu.com/imeres/ime-res/guanwang/img/Ubuntu_Deepin-fcitx-baidupinyin-64.zip -O /tmp/baidu_pinyin/Ubuntu_Deepin-fcitx-baidupinyin-64.zip
    upzip /tmp/baidu_pinyin/Ubuntu_Deepin-fcitx-baidupinyin-64.zip -d /tmp/baidu_pinyin

## 依赖包

    依赖包最大的问题。

    我先新增了一个ubuntu18.04(bionic)的apt源

    echo 'deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse' >> /etc/apt/sources.list.d/ubuntu1804.list

    sudo apt update  # 为了避免不必要的麻烦，我并没有进行 sudo apt upgrade 操作

    gdebi /tmp/baidu_pinyin/fcitx-baidupinyin.deb  # gdebi 会自动寻找依赖，如果没有安装，可以通过 sudo apt install gdebi 安装

    # 为保险起见，我把官方文档中给到的软件包又安装了一次，其实已经安装完了。

    # fcitx-config-gtk2  这个软件包有冲突，但是不安装也没发现有什么影响。

    sudo apt install fcitx-bin fcitx-table fcitx-config-gtk fcitx-frontend-all

    # 此时还需要安装一个依赖库，官方文档并没有提及。

    sudo apt install libqt5webkit5 libqt5webkit5-dev

## 修改默认语言

    将语言支持改为fcitx

    设置 - 区域与语言 - 管理已安装的语言 - 键盘输入法系统 - 选择 [fcitx]

    重启机器，你可能会出现ibus和fcitx两种输入法同在的情况，我的操作是直接删除了ibus

    sudo apt purge ibus
    
    然后再重启

## 清理工作

    rm -f /etc/apt/sources.list.d/ubuntu1804.list
