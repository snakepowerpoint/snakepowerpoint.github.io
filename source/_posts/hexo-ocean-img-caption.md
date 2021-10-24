---
title: 在 Hexo 插入圖片標題
date: 2021-10-24 22:12:57
tags: hexo, ocean
categories:
  - 程式
  - 前端
  - Hexo
---

最近在寫文章的時候，突然發現需要替圖片補上標題，上網查了一下，聽說 markdown 可以透過下面的語法，直接幫圖片插入標題：

```
![](path_to_image)
*image_caption*
```

不過我自己試了一下發現不行，由 Hexo 渲染的 markdown 文章並無法直接插入圖片標題。繼續爬文後，找到了另一個方法，而且做法相當簡單！


<!--more-->

### 步驟一

首先先安裝 hexo 套件，在 ```cmd``` 中輸入：

```
npm install --save hexo-image-caption
```

### 步驟二 

接著在 hexo 的 config 中加入以下資訊：

```
# add caption for iamges
image_caption:
  enable: true #false to disable
  class_name: #if you wanna customize the style for the caption,you can assign a class name, default is 'image-caption'
```

基本上這樣就大功告成了，往後只要在 markdown 文章中輸入：

```
![caption](img_file_name.jpg)
```

就能幫圖片插入標題啦！


### 補充

這個方法美中不足的地方是，標題沒辦法置中，爬文發現要另外在文章的 css 中加入一些設定，才能讓圖標置中。以我使用的 ocean 主題為例，在 ```ocean/source/css/_partial/articles.styl``` 中加入：

```
.article .image-caption {
    margin: auto;
    display: block;
    text-align: center;
    width: 80%
}
```

這樣就能讓圖片置中啦了，是不是很簡單！


### 參考資料

- hexo-image-caption https://github.com/wayou/hexo-image-caption

- https://stackoverflow.com/questions/19331362/using-an-image-caption-in-markdown-jekyll

- https://www.dazhuanlan.com/jokerissb/topics/1160083

