---
author: jeffzhang
comments: true
date: 2008-03-12 01:58:19+00:00
layout: post
title: C# 按照单词反转字符串
wordpress_id: 116
categories:
- 挨踢
tags:
- 杂谈
---

using System;
 public class reverse
 {
  public static void swap(string[] array, ref int istart, ref int iend)
  {
  string[] ch = new string[1] ;
  while (istart < iend)
  {
  ch[0] = array[istart];
  array[istart] = array[iend];
  array[iend] = ch[0];
  istart++;
  iend--;
  }
  }

public static string rever(string array)
  {
  int len=array.Length;
  string [] newstr=new string [len];
  for(int s=0;s<len;s++)
  {
  newstr[s]=array[len-1-s].ToString();
   }
  
  int istart=0,iend=0,i;
  for(i=0;i<len;i++)
  {
  if (newstr[i] == " ")
  {
  iend = i - 1;
  if (istart < iend)
  {
  swap(newstr,ref istart,ref iend);
  istart = i + 1;
  }
  }
  else if (newstr[i] == "!" | newstr[i] == "," | newstr[i] == ".")
  {
  istart=i+1;
   }
  }
  iend=len-1;
  if(istart<iend)
  {
  swap(newstr,ref istart,ref iend);
  }

array="";
  for(int s=0;s<len;s++)
  {
  array+=newstr[s];
   }
  return array;
  }
  public static void Main()
  {
  string iarray = "siemens like movie!! me too.";
  string reversestr = rever(iarray);
  Console.WriteLine(reversestr);
  }

}
