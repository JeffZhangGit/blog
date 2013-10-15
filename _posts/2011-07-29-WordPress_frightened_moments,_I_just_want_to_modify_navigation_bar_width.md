---
author: jeffzhang
comments: true
date: 2011-07-29 04:10:59+00:00
layout: post
title: WordPress惊魂一刻，我仅仅想要修改一下导航栏宽度
wordpress_id: 1751
categories:
- WordPress
- 愤青
tags:
- atahualpa
- wordpress
- 插件
- 铁盗部
---

昨天下午登录“姐夫张”，发现导航栏过于拥挤，想找个办法把导航栏栏目的宽度调整一下  
仅仅，仅仅是想修改一下导航栏宽度，没想到竟然制造了WordPress惊魂一刻  
下面表一下事情经过

我使用的是Atahualpa这个主题，我就在后台打开Atahualpa Theme Options，可是左找右找都没有发现调整导航栏栏目宽度的选项。

无意间（现在想想真是手贱)，发现了**Header Area->Style & edit HEADER AREA ->Configure Header Area **这里有关于导航栏控件的定义。 
  * `%pages` - The horizontal drop down menu bar for "Page" pages 


  * `%page-center` - Like above but centered. Note: There's no S in this tag. It's **not** %page**S**-center 


  * `%page-right` - Like above but right-aligned. Note: There's no S in this tag. It's **not** %page**S**-right 


  * `%cats` - The horizontal drop down menu bar for categories 


  * `%cat-center` - Like above but centered. Note: There's no S in this tag. It's **not** %cat**S**-center 


  * `%cat-right` - Like above but right-aligned. Note: There's no S in this tag. It's **not** %cat**S**-right 


  * `%logo` - The logo area, including the logo icon, the blog title & description, the search box and the RSS/Email icons 


  * `%image` - The rotating (or static) header image with the (optional) opacity overlay left & right and an (optional) overlayed blog title & blog tagline 


  * `%bar1` - A horizontal bar, to be used as decoration on top, bottom of between header items. Can be used multiple times. 


  * `%bar2` - A second horizontal bar, that can be styled differently. Can be used multiple times.

我没有使用过%page-center 这一项，便抱着试试看的想法把导航栏布局中的%pages换成了前者。预览了一下，导航栏位置居中，视觉效果不是很好，我就想把刚才的修改还原回去。可是没成想，Atahualpa竟然无法保存配置更新，试了好几次都是页面无响应。心中暗想，不妙。下面开始了弥补过错的尝试。
  * 开始疯狂的baidu google “Atahualpa 不能保存配置”，搜出来的信息都是低版本的。无解。


  * 使用Import 配置文件方法，首先把当前配置文件导出，然后手动找到需要修改的地方进行修改，然后使用Import方法上传，可是上传之后的配置文件依然没有生效，无解。


  * 使用Reset配置文件方法，希望重置了配置文件之后就可以保存配置信息，结果事与愿违，导航栏配置重置之后惨不忍睹，并无法更新，无解。


  * 在Atahualpa目录中搜索主题的配置文件，可是翻遍所有的文件都没有找到，无解。

在尝试了如此方法都没有任何进展的前提下，怒从心头起恶向胆边生，小样的，还治不了你了。

**老子要改你的数据表！！！**

 

在网上搜到Atahualpa把配置文件存在wp_options数据表中，搜了一下，这个表中竟然有800多条记录，心想，什么主题这么NB，竟然有这么多的配置信息，我还专门Query了一遍，看的眼花缭乱的。当机立断，做出来愚蠢错误的决定，删掉数据表。  
反思一下这个决定：
  * 不知道wp_options是系统数据表，不仅存着主题配置信息，还存着所有插件的配置信息和系统配置信息。


  * 天真的认为删了wp_options数据表就可以把Atahualpa配置文件进行恢复。


  * 认为wp_options中Atahualpa配置信息太多，所以想清空（有系统洁癖的通病）。


  * 被愤怒冲昏头脑，只想快速把系统恢复原样。

结果是系统彻底的Down了。系统提示遇到致命错误，需要恢复数据库，点击回复数据库的按钮也与事无补。

** **

**咔嚓！系统崩溃！如同晴天霹雳！**

我的心在流泪，仅仅，我仅仅想修改一下导航栏栏目的宽带，竟然落到系统崩溃的可悲的下场。可恶的蝴蝶效应在我身上得到了完美的体现。  
叹了口气，眼泪是留给懦弱者的。我要把系统回复过来。  
还好老子有备份系统的好习惯，找到最新的备份文件，是7月13号，当时有两个方案：
  1. 完整恢复数据库，这样可以保证系统完美恢复，不过缺点是最近几天的数据将丢失。


  2. 恢复被删除的数据表，这个方案不是完美恢复方案，但是不会丢失最近今天的文章评论等信息。

在一番深思熟虑之后，选择了方案2. 具体实现方法如下：
  * 创建一个新的数据库，然后还原 


    * create database temp;


    * use temp;


    * source TheBackUpFileFullPath


  * 在将新库中的表导入原来的数据库 


    * drop table DatabaseName.wp_options


    * create table DatabaseName.wp_options as select * from temp.wp_options;

终于，熟悉的界面出现了。一场系统浩劫过去，留给我们反思的地方很多：
  * 做决定之前要先把事情理清楚，不能想当然，更不能冒失。


  * 发现问题，不需要惊慌，冷静的面对困难，解决问题。


  * 一定要养成及时备份的好习惯。

 

PS：铁盗部，出了事故之后否认这个否认那个，根本没有自省，否认掩埋事故列车车头销毁证据，那么多记者，现场照片，视频证明你们挖了个坑埋列车车头，你他妈的还能说否认就否认。这是什么天理？

铁盗部非横跋扈，你们这些P民折腾有什么用，能有什么用，我说死了多少人就是死了多少人，我说事故是他妈的雷劈的就是雷劈的，死几十个人算什么，一条命不过区区五十万么。

要想使其灭亡，必先使其疯狂。

他们终究迟早要灭亡，至于你信不信，由你，我反正是信了。
