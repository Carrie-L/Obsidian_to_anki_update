# Obsidian_to_anki_update
修改插件[Obsidian_to_Anki](https://github.com/ObsidianToAnki/Obsidian_to_Anki)中的main.js源码，使其符合我的需求。为原插件更新了如下功能：
1. tag添加中文支持
2. 适配我的正则表达式，使添加卡片的操作更加顺滑
3. 添加对Cloze卡片的正则支持
4. 添加对输入答案卡片的正则支持

## 使用
### 替换插件main.js
1. 打开电脑中笔记存储路径下的插件文件夹, `.obsidian\plugins\obsidian-to-anki-plugin`, 例如我的路径为：
```
I:\B-1 笔记\DS & Algorithm\.obsidian\plugins\obsidian-to-anki-plugin
```
2. 点击此仓库中的`main.js`，下载，
替换插件里的 `main.js`
![image](https://github.com/user-attachments/assets/60aa2377-a3f3-4063-a652-7a63d5274423)

![image](https://github.com/user-attachments/assets/e31ffc4f-0d48-4618-a539-b6ddd919d087)

### 自定义正则表达式
1. Obsidian打开设置，在`Community plugins - Obsidian_to_Anki`里，点击 `Note Type Table`，选择一个笔记模板，在`Custom Regexp`下添加：
```
^#{2,}(.+)\n([\s\S]*?)\nEND
```

2. 将该笔记模板的`File Link Field` 改为正面问题，`Context Field` 改为反面回答。
3. 滑动到下面，打开 `Add Obsidian Tags`开关
![image](https://github.com/user-attachments/assets/24e7ab15-a788-47d5-b804-6cb5a20d1417)


###  添加笔记
笔记至少以`##`开头，`END`结尾。如果开头没有#，则不会添加成功。
插件会自动根据自定义正则表达式扫描笔记内容，如果添加到anki成功，会在笔记下方添加一个anki卡片ID。

### 添加Cloze笔记
#### 1. Anki操作
工具 —— 管理笔记模板，添加一个**填空题Cloze**模板，模板名称必须包含"Cloze"！否则无法添加卡片。
> [!IMPORTANT]
> 模板名称必须包含`Cloze`!

#### 2. Obsidian操作
##### 2.1 Regenerate 更新笔记模板 
打开设置，点击左侧`Community Plugins —— Obsidian_to_Anki`，找到右边页面的`Actions —— Regenerate Note Type Table`，点击`Regenerate`，更新笔记模板。

##### 2.2 Note Type Settings
点击`Note Type Table`，找到Cloze模板，输入:
```
^#{2,}\s*([\s\S]*?)\n()END
```

##### 2.3 添加Cloze笔记
Cloze笔记只有**正面内容**，将需要隐藏的内容修改为：`{{c1::这是你的笔记内容}}`。
请严格遵照这个格式，`{{}}`里只能为`c1`，不能为`c2`,不能为`cloze`，必须有两个冒号`::`，必须有两组大括号`{{}}`，只能创建一张卡片。
>[!TIP]
>{{c1::这是你的笔记内容}}

笔记参考示例：
```
#### Table
| 名字 | 姓氏 |
| ---- | ---- |
| 麦克斯 | {{c1::普朗克}} |
| {{c1::玛丽}} | 居里 |
END
```
然后点击同步。

### 添加问答题(输入答案)笔记
与添加Cloze笔记类似。

#### 1. Anki操作
工具 —— 管理笔记模板，添加一个 **问答题（输入答案）** 模板，模板名称必须包含"Type"！否则无法添加卡片。
> [!IMPORTANT]
> 模板名称必须包含`Type`!

#### 2. Obsidian操作
##### 2.1 Regenerate 更新笔记模板 
打开设置，点击左侧`Community Plugins —— Obsidian_to_Anki`，找到右边页面的`Actions —— Regenerate Note Type Table`，点击`Regenerate`，更新笔记模板。

##### 2.2 Note Type Settings
点击`Note Type Table`，找到Type答案模板，输入:
```
^#{2,}(.+)\n*([\s\S]*?)\nEND
```

##### 2.3 添加Type答案笔记
此模板为正反面问答题模板，背面内容为`答案`, 格式为: `{{type::你的答案}}`
>[!TIP]
>{{type::你的答案}}

参考示例：
```
#### 世界上最长的河流是什么？ 
{{type::尼罗河}}
END
```
显示效果为：

![Snipaste_2024-10-17_03-47-23](https://github.com/user-attachments/assets/40953f6e-045c-41c5-b072-56ddf75bc60f)
![Snipaste_2024-10-17_03-47-41](https://github.com/user-attachments/assets/93e65780-de8f-47a7-a41b-967892e8f492)



### 更新笔记
如果Obsidian笔记没有更新，插件则不会扫描该笔记。所以如果你需要更新笔记，你至少需要在笔记里做一点改动。
插件不会添加**问题和回答没有一点变化**的笔记。

**如何更新笔记？**
笔记下方的ID不需要改动，直接修改文本，并点击插件同步就好。

### 添加标签
打开Obsidian 
`#tags`
>[!TIP]
>`#`+`标签名`，**中间不要有空格**。
原插件只支持英文和数字标签，修改后的代码支持**中英文数字**标签。

### 删除笔记
删除笔记有两种方式：
#### 方法一
在**anki-浏览**中，选择笔记，右键删除。
然后删除该笔记下的ID。笔记ID与Anki卡片编号相对应。
![image](https://github.com/user-attachments/assets/759c2e23-bb93-4866-b106-6a6e8f7e26ba)
#### 方法二
在笔记`END`后面添加如下代码：
```
DELETE
ID: 1726985548909
```
> [!IMPORTANT]
> ID: 后面要有空格。
点击同步，同步完成后再删除该笔记下的ID。不要在还没同步之前就把ID删掉。

### 网络图片
支持网络图片和本地图片的同步，使用以下markdown格式显示图片,举例：
```
![](http://img.netbian.com/file/2024/0511/0048385zLvF.jpg)
```
[]里可以为空。



