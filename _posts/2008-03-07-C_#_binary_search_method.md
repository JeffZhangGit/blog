---
author: jeffzhang
comments: true
date: 2008-03-07 03:30:52+00:00
layout: post
title: C# 二分查找法
wordpress_id: 119
categories:
- 挨踢
tags:
- 杂谈
---

using System;
 /// <summary>
 /// 二分查找法
 /// </summary>

public class Search
 {
  static int search(int[] array)
  {
  int low = 0;
  int high = array.Length - 1;
  Console.WriteLine("Please input a number:");
  int i = int.Parse(Console.ReadLine());
  while (low <= high)
  {
  int middle = (low + high) / 2;
  if (i == array[middle])
  {
  return i;
  }
  else if (i < array[middle])
  {
  high = middle - 1;
  }
  else
  {
  low = middle + 1;
  }
  }
  throw new Exception();
  }
  static void sort(int[] array)
  {
  bool exchange;
  for (int i = 0; i < array.Length - 1; i++)
  {
  exchange = false;
  for (int j = array.Length - 1; j > i; j--)
  {
  if (array[j - 1] > array[j])
  {
  int tem;
  tem = array[j - 1];
  array[j - 1] = array[j];
  array[j] = tem;
  exchange = true;
  }
  }
  if (!exchange) { break; }
  }
  }

static void Main()
  {
  int[] iarray = new int[] { 2, 6, 4, 98, 5, 16, 9, 8, 7, 44 };
  sort(iarray);
  try
  {
  Console.WriteLine(search(iarray));
  }
  catch
  {
  Console.WriteLine("This num is not in this Array or you enter an invalid num!");
  }
  }
 }

