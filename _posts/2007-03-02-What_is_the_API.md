---
author: jeffzhang
comments: true
date: 2007-03-02 06:41:31+00:00
layout: post
title: 什么是API
wordpress_id: 197
categories:
- 挨踢
---

API 就是应用程序编程接口。它是能用来操作组件、应用程序或者操作系统的一组函数。典型的情况下，API 由一个或多个提供某种特殊功能的 DLL 组成。(java中有所不同，但大同小异）


DLL 是一个文件，其中包含了在 Microsoft Windows 下运行的任何应用程序都可调用的函数。运行时，DLL 中的函数动态地链接到调用它的应用程序中。无论有多少应用程序调用 DLL 中的某个函数，在磁盘上只有一个文件包含该函数，且只在它调入内存时才创建该 DLL。

您听到最多的 API 可能是 Windows API，它包括构成 Windows 操作系统的各种 DLL。每个 Windows 应用程序都直接或间接地与 Windows API 互动。Windows API 保证 Windows 下运行的所有应用程序的行为方式一致。

注意 随着 Windows 操作系统的发展，现已发布了几个版本的 Windows API。Windows 3.1 使用 Win16 API。Microsoft Windows NTindows 95 和 Windows 98 平台使用 Microsoft Win32 API。
  除 Windows API 外，其他一些 API 也已发布。例如，邮件应用程序编程接口 (MAPI) 是一组可用于编写电子邮件应用程序的 DLL。

API 传统上是为开发 Windows 应用程序的 C 和 C++ 程序员编写的，但其他的编程语言（包括VBA）也可以调用 DLL 中的函数。因为大部分 DLL 主要是为 C 和 C++ 程序员编写和整理说明的，所以调用 DLL 函数的方法与调用 VBA 函数会有所不同。在使用 API 时必须了解如何给 DLL 函数传递参数。

警告 调用 Windows API 和 其他 DLL 函数可能会给您的应用程序带来不良影响。从自己的代码中直接调用 DLL 函数时，您绕过了 VBA 通常提供的一些安全机制。如果在定义或调用 DLL 函数时出现错误（所有程序员都不可避免），可能会在应用程序中引起应用程序错误（也称为通用性保护错误，或 GPF）。最好的解决办法是在运行代码以前保存该项目，并确保了解 DLL 函数调用的原理。
