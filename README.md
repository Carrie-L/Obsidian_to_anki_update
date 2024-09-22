# Obsidian_to_anki_update
修改插件[Obsidian_to_Anki](https://github.com/ObsidianToAnki/Obsidian_to_Anki)中的main.js源码，使其符合我的需求。

## 使用
### 替换插件main.js
1. 打开电脑中笔记存储路径下的插件文件夹, `.obsidian\plugins\obsidian-to-anki-plugin`, 例如我的路径为：
```
I:\B-1 笔记\DS & Algorithm\.obsidian\plugins\obsidian-to-anki-plugin
```
2. 将此`main.js` 替换插件里的 `main.js`
![image](https://github.com/user-attachments/assets/e31ffc4f-0d48-4618-a539-b6ddd919d087)

### 自定义正则表达式
1. Obsidian打开设置，在`Community plugins - Obsidian_to_Anki`里，点击 `Note Type Table`，选择一个笔记模板，在`Custom Regexp`下添加：
```
^#{2,}(.+)\n([\s\S]*?)\nEND
```

2. 将该笔记模板的`File Link Field` 改为正面问题，`Context Field` 改为反面回答。

###  添加笔记
笔记需以`##`开头，`END`结尾。
插件会自动根据自定义正则表达式扫描笔记内容，如果添加到anki成功，会在笔记下方添加一个anki卡片ID。

### 更新笔记
如果Obsidian笔记没有更新，插件则不会扫描该笔记。所以如果你需要更新笔记，你至少需要在笔记里做一点改动。
插件不会添加**问题和回答没有一点变化**的笔记。

**如何更新笔记？**
笔记下方的ID不需要改动，直接修改文本，并点击插件同步就好。

### 添加标签
>[!TIP]
>#tags
>`#`+标签名，**中间不要有空格**。
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



