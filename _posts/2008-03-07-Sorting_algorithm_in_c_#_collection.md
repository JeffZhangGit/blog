---
author: jeffzhang
comments: true
date: 2008-03-07 03:21:58+00:00
layout: post
title: C# 排序算法合集
wordpress_id: 120
categories:
- 挨踢
tags:
- 杂谈
---

sort.cs

using System;
 using System.Collections.Generic;
 using System.Text;

namespace Sort
 {
  /// <summary>
  /// 冒泡排序
  /// </summary>
  public class BubbleSort
  {
  public void sort(int [] array)
  {
  bool exchange;
  for (int i = 0; i < array.Length; i++)
  {
  exchange = false;
  for (int j = array.Length-1; j > i; j--)
  {
  if(array[j]<array[j-1])
  {
  int tem;
  tem = array[j];
  array[j] = array[j - 1];
  array[j - 1] = tem;
  exchange = true;
  }
  }
  if (!exchange) { break;}
  }
  }
  }
  /// <summary>
  /// 快速排序，前置哨兵
  /// </summary>
  public class QuickSortI
  {
  public void swap(ref int l, ref int r)
  {
  int n;
  n = l; l = r; r = n;
  }
  public void sort(int[] array, int left, int right)
  {
  if (left < right)
  {
  int pivot = array[left];
  int i = left;
  int j = right + 1;
  while (true)
  {
  while (i < array.Length - 1 && array[++i] < pivot) ;
  while (j > 0 && array[--j] > pivot) ;
  if (i >= j)
  break;
  swap(ref array[i], ref array[j]);

}
  array[left] = array[j];
  array[j] = pivot;
  sort(array, left, j - 1);
  sort(array, right, j + 1);
  }
  }

}
  /// <summary>
  /// 快速排序，中置哨兵
  /// </summary>
  public class QuickSortII
  {
  private void swap(ref int i, ref int j)
  {
  int s;
  s = j; j = i; i = s;
  }
  public void sort(int[] array, int left, int right)
  {
  if (left < right)
  {
  int pivot = array[(left + right) / 2];
  int i = left - 1;
  int j = right + 1;
  while (true)
  {
  while (array[++i] < pivot) ;
  while (array[--j] > pivot) ;
  if (i >= j)
  break;
  
   swap(ref array[i], ref array[j]);
  } 
   sort(array, left, i - 1);
  sort(array, j + 1, right);
  }
  }
  }
  /// <summary>
  /// 快速排序，尾置哨兵
  /// </summary>
  public class QuickSortIII
  {
  public void swap(ref int l,ref int r)
  {
  int tem;
  tem = l; l = r; r = tem;
  }

public void sort(int[] array, int left, int right)
  {
  if(left < right)
  {
  int q = part(array, left, right);
  sort(array, left, q - 1);
  sort(array, q + 1, right);
  } 
   }

public int part(int[] array, int left, int right)
  {
  int pivot = array[right];
  int i = left - 1;
  for (int j = left; j < right; j++)
  {
  if (array[j] <= pivot)
  {
  i++;
  swap(ref array[i], ref array[j]);
  }
  
   }
  swap(ref array[i + 1], ref array[right]);
  return i+1;
  }

}

/// <summary>
  /// 选择排序
  /// </summary>
  public class ChooseSort
  {
  public void sort(int[] array)
  {
  int key,index;
  for (int i = 0; i < array.Length; i++)
  {
  key = array[i];
  index = i;
  for (int j = i+1; j < array.Length; j++)
  {
  if (array[j] < key)
  {
  key = array[j];
  index = j;
  }
  }
  array[index] = array[i];
  array[i] = key;
  }
  }
  }

/// <summary>
  /// 插入排序
  /// </summary>
  public class InsertionSort
  {
  public void sort(int[] array)
  {
  int temp;
  for (int i = 1; i < array.Length; i++)
  {
  temp = array[i];
  int j=i;
  while ((j > 0) && (array[j-1] > temp))
  {
  array[j] = array[j - 1];
  --j;
  }
  array[j] = temp;
  }
  }
  }
 }

