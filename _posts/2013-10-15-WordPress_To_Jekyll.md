---
layout: post
title: Convert WordPress posts to Jekyll
categories:
- IT
tags:
- Git
- Markdown
- WordPress
---

If you only have one Wordpress backup file, and this backup file generate by one WP plugin "WP_DBManager". You want to create your github website and import the WP posts from the backup file, this post will help you on this.
<br/>



###Setup the WordPress environment###
1. Download XAMPP from [here][1].
2. Download the latest wordpress zip file from [here][2].
3. Configure the XAMPP by this guidance [WordPress本地环境搭建及安装图文教程][3]
4. If your backup file over 2M, you should update the PHP configure file to increase the max size of upload file.
5. Import the backup SQL file by PHPAdmin.
6. Configure the WP use this guidance [WordPress五分钟安装步骤][4]
<br/>
<br/>

###WordPress export XML file###
Convert all the wordpress to one XML file by the Export->All the content 
<br/>
<br/>

###Use exitwp convert WP XML file to markdown file###

 1. You can download the exitwp from [here][5]
 2. Setup the exitwp ruuning envionment
     -     Python 2.6, 2.7
     -     html2text : converts HTML to markdown (python)
     -     PyYAML : Reading configuration files and writing YAML headers (python)
     -     Beautiful soup : Parsing and downloading of post images/attachments (python)
 3. Execute the exitwp please follow this post  [WordPress转换至Jekyll][6]
<br/>
<br/>

###Final steps###
1.  The exitwp tool convert the WP XML file to files which extention is `.markdown`, we need rename the file extention to `.md` by the following script.
<br/> 
   ` ren  *.*  *.md`
2.  You may write other scripts to update the md files as you wish.
<br/>
<br/>


  [1]: http://www.apachefriends.org/zh_cn/xampp.html
  [2]: http://wordpress.org/download/
  [3]: http://jingyan.baidu.com/article/90bc8fc82098def653640c88.html
  [4]: http://xuui.net/wordpress/wordpress-install.html
  [5]: https://github.com/thomasf/exitwp
  [6]: http://aotee.com/wordpress-conversion-to-jekyll
