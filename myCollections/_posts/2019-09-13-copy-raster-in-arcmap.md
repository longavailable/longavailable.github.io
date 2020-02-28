---
layout: post
title:  神奇的Copy Raster
subtitle: 
author: Bruce Liu
# last update date
date:   2019-09-13 00:50:03 +0200 
# first published date
published: 2019-09-13 00:50:03 +0200 
categories: [post]
tags: [ArcGIS, GIS, tools]
header-image: 
permalink: 
---
Copy Raster不仅仅是copy工具，更是一个独特的转换工具
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

<!-- This post was copied from my Wordpress website -->
<!-- wp:paragraph -->
<p>工具位置：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Copy Raster &lt;- Raster Dataset &lt;- Raster &lt;- Data Management</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>功能如下：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>1. convert raster to other format /修改数据格式相同于coversion tools中raster to other format raster。在output raster dataset中除了name of output，同时指定要转换成的file&nbsp;extension。如下：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>.bil&nbsp;for&nbsp;Esri&nbsp;BIL</li><li>.bip&nbsp;for&nbsp;Esri&nbsp;BIP</li><li>.bmp&nbsp;for&nbsp;BMP</li><li>.bsq&nbsp;for&nbsp;Esri&nbsp;BSQ</li><li>.dat&nbsp;for&nbsp;ENVI&nbsp;DAT</li><li>.gif&nbsp;for&nbsp;GIF</li><li>.img&nbsp;for&nbsp;ERDAS&nbsp;IMAGINE</li><li>.jpg&nbsp;for&nbsp;JPEG</li><li>.jp2&nbsp;for&nbsp;JPEG&nbsp;2000</li><li>.png&nbsp;for&nbsp;PNG</li><li>.tif&nbsp;for&nbsp;TIFF</li><li>.mrf&nbsp;for&nbsp;MRF</li><li>.crf&nbsp;for&nbsp;CRF</li><li>No&nbsp;extension&nbsp;for&nbsp;Esri&nbsp;Grid</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>2. change “pixel type” /更改数据像素类型</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>1_BIT&nbsp;—A&nbsp;1-bit&nbsp;unsigned&nbsp;integer.&nbsp;The&nbsp;values&nbsp;can&nbsp;be&nbsp;0&nbsp;or&nbsp;1.</li><li>2_BIT&nbsp;—A&nbsp;2-bit&nbsp;unsigned&nbsp;integer.&nbsp;The&nbsp;values&nbsp;supported&nbsp;can&nbsp;be&nbsp;from&nbsp;0&nbsp;to&nbsp;3.</li><li>4_BIT&nbsp;—A&nbsp;4-bit&nbsp;unsigned&nbsp;integer.&nbsp;The&nbsp;values&nbsp;supported&nbsp;can&nbsp;be&nbsp;from&nbsp;0&nbsp;to&nbsp;15.</li><li>8_BIT_UNSIGNED&nbsp;—An&nbsp;unsigned&nbsp;8-bit&nbsp;data&nbsp;type.&nbsp;The&nbsp;values&nbsp;supported&nbsp;can&nbsp;be&nbsp;from&nbsp;0&nbsp;to&nbsp;255.</li><li>8_BIT_SIGNED&nbsp;—A&nbsp;signed&nbsp;8-bit&nbsp;data&nbsp;type.&nbsp;The&nbsp;values&nbsp;supported&nbsp;can&nbsp;be&nbsp;from&nbsp;-128&nbsp;to&nbsp;127.</li><li>16_BIT_UNSIGNED&nbsp;—A&nbsp;16-bit&nbsp;unsigned&nbsp;data&nbsp;type.&nbsp;The&nbsp;values&nbsp;can&nbsp;range&nbsp;from&nbsp;0&nbsp;to&nbsp;65,535.</li><li>16_BIT_SIGNED&nbsp;—A&nbsp;16-bit&nbsp;signed&nbsp;data&nbsp;type.&nbsp;The&nbsp;values&nbsp;can&nbsp;range&nbsp;from&nbsp;-32,768&nbsp;to&nbsp;32,767.</li><li>32_BIT_UNSIGNED&nbsp;—A&nbsp;32-bit&nbsp;unsigned&nbsp;data&nbsp;type.&nbsp;The&nbsp;values&nbsp;can&nbsp;range&nbsp;from&nbsp;0&nbsp;to&nbsp;4,294,967,295.</li><li>32_BIT_SIGNED&nbsp;—A&nbsp;32-bit&nbsp;signed&nbsp;data&nbsp;type.&nbsp;The&nbsp;values&nbsp;can&nbsp;range&nbsp;from&nbsp;-2,147,483,648&nbsp;to&nbsp;2,147,483,647.</li><li>32_BIT_FLOAT&nbsp;—A&nbsp;32-bit&nbsp;data&nbsp;type&nbsp;supporting&nbsp;decimals.</li><li>64_BIT&nbsp;—A&nbsp;64-bit&nbsp;data&nbsp;type&nbsp;supporting&nbsp;decimals.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>3. change "NoData Value" /修改NoData值！！更改的是NoData Value（NoData像素的标识值），而不是把NoData改为某个有效的Pixel value。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Reference:&nbsp;<a href="https://pro.arcgis.com/en/pro-app/tool-reference/data-management/copy-raster.htm">https://pro.arcgis.com/en/pro-app/tool-reference/data-management/copy-raster.htm</a></p>
<!-- /wp:paragraph -->




