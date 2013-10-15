---
author: jeffzhang
comments: true
date: 2008-03-07 05:06:24+00:00
layout: post
title: C# 逆序字符串
wordpress_id: 118
categories:
- 挨踢
tags:
- 杂谈
---

using System;

class Output
 {
  public static void Main(string[] args)
  {
  //*********************String reverse******************
  Console.WriteLine("Please input a sentence:");
  string str = Console.ReadLine();
  string[] s = str.Split(' ');
  for (int i =0 ; i < s.Length/2 ; i++)
  {
  string tem;
  tem = s[i];
  s[i] = s[s.Length - i-1];
  s[s.Length-i-1] = tem;
  }
  foreach (string a in s)
  {
  Console.Write(a+" ");
  }

}
 }
