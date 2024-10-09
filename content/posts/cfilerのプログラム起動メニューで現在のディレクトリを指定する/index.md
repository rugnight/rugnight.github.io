---
title: "Cfilerのプログラム起動メニューで現在のディレクトリを指定する"
date: 2024-10-02T23:47:48+09:00
categories: []
tags: ["cfiler"]
thumbnail: ""
---

```.py
def command_ProgramMenu(info):

# 現在開いているPaneをXnViewで開く
def launch_XnView():
    print(window.activePane().file_list.getLocation())
    shellExecute( None, r"C:\Program Files\XnViewMP\xnviewmp.exe", "%s" % window.activePane().file_list.getLocation(), "")

    items = [
        ( "XnView",    launch_XnView )
    ]
```
