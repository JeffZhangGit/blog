---
author: jeffzhang
comments: true
date: 2008-10-14 07:04:52+00:00
layout: post
title: 事件的传递与分层初探
wordpress_id: 87
categories:
- 挨踢
tags:
- 杂谈
---

程序为什么要分层

分层之后层与层之间靠什么通信

参见[http://msdn.microsoft.com/en-au/library/ms978678(zh-cn).aspx](http://msdn.microsoft.com/en-au/library/ms978678(zh-cn).aspx)

下例是一个简单的例子

使用事件进行信息传递

当baselayer收到信息之后，传递到middlelayer然后再传递到toplayer.

using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;

namespace Prac
 {

//传递的信息类
  public class ReceiveMSGEventArgs
  {
  public readonly string _MSG;
  public ReceiveMSGEventArgs(string value)
  {
  this._MSG = value;
  }
  }

//收到信息的委托
  public delegate void ReceiveMSGHandler(object sender, ReceiveMSGEventArgs args);

//底层类

public class BaseLayer
  {
  ReceiveMSGEventArgs _args = null;
  public event ReceiveMSGHandler ReceivedMSG;
  public BaseLayer()
  {
  _args = new ReceiveMSGEventArgs("BaseLayer received MSG");
  }

//正在接收信息
  public void ReceivingMSG()
  {
  //TODO receiving msg
  OnReceiveMSG(_args);
  }

//当收到信息之后触发ReceivedMSG事件
  public void OnReceiveMSG(ReceiveMSGEventArgs args)
  {
  if (ReceivedMSG != null)
  {
  ReceivedMSG(this, args);
  }
  }
  }

//中层类
  public class MiddleLayer
  {
  public event ReceiveMSGHandler ReceivedMSG;
  ReceiveMSGEventArgs _args;
  public BaseLayer _blayer = null;
  public MiddleLayer()
  {
  _blayer = new BaseLayer();
  }
  public void Initialize()
  {

//注册事件
  _blayer.ReceivedMSG += new ReceiveMSGHandler(_blayer_ReceivedMSG);
  }

//当收到底层的信息后进行包装并向上层传递事件
  private void _blayer_ReceivedMSG(object sender, ReceiveMSGEventArgs args)
  {
  Console.WriteLine("MiddleLayer receive: {0}", args._MSG);
  _args = new ReceiveMSGEventArgs(args._MSG + " and SecondLayer received MSG");
  ReceivedMSG(this, _args);
  }
  }

//上层类
  public class TopLayer
  {
  public MiddleLayer _mlayer = null;
  public TopLayer()
  {
  _mlayer = new MiddleLayer();
  }
  public void Initialize()
  {
 //注册事件
  _mlayer.ReceivedMSG += new ReceiveMSGHandler(_mlayer_ReceivedMSG);
  }

//接收中层传递的信息
  private void _mlayer_ReceivedMSG(object sender, ReceiveMSGEventArgs args)
  {
  Console.WriteLine("TopLayer receive: {0}", args._MSG);
  }
  }

//测试程序
  public class App
  {
  static void Main()
  {

TopLayer tlayer = new TopLayer();
  tlayer.Initialize();
  tlayer._mlayer.Initialize();
  tlayer._mlayer._blayer.ReceivingMSG();

}
  }
 }

