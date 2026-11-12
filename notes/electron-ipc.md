---
layout: default
title: Electron IPC 笔记
---

# Electron IPC 笔记

IPC 是 Inter-Process Communication（进程间通信）的缩写。Electron 的渲染进程可以通过预加载脚本暴露的接口，调用主进程提供的桌面能力。

- `ipcRenderer.invoke` 和 `ipcMain.handle` 配对使用，适合需要返回结果的调用。
- 预加载脚本可以用 `contextBridge` 暴露业务接口，例如 `selectFile()`。

[返回目录](../)
