---
author: jeffzhang
comments: true
date: 2009-04-22 10:10:46+00:00
layout: post
title: 反转字符串 II （Reverse string II）
wordpress_id: 76
categories:
- 挨踢
tags:
- 杂谈
---

更新后的算法，

非常简单的逻辑，

class Program
  {
  static void Main(string[] args)
  {
  while (true)
  {
  Console.WriteLine("Input:");
  string input = Console.ReadLine();
  StringBuilder output = new StringBuilder(new string(' ', input.Length), input.Length);
  StringBuilder temp = new StringBuilder();
  bool dataExist = false;
  for (int counter = 0; counter < input.Length; counter++)
  {
  if (IsSplitor(input[counter]))
  {
  output[input.Length - counter - 1] = input[counter];
  if (dataExist)
  {
  for (int counterII = 0; counterII < temp.Length; counterII++)
  {
  output[input.Length - counter + counterII] = temp[counterII];
  }
  temp = new StringBuilder();
  }
  }
  else
  {
  temp.Append(input[counter]);
  dataExist = true;
  if (counter == input.Length - 1)
  {
  for (int counterII = 0; counterII < temp.Length; counterII++)
  {
  output[counterII] = temp[counterII];
  }
  }
  }
  }
  Console.WriteLine("Outut:");
  Console.WriteLine(output);
  }
  }

static bool IsSplitor(char value)
  {
  return (value == ',' || value == ' ' || value == '!' || value == '.');
  }
  }
