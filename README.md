## Q:我希望在Obsibian中，每次打开这篇笔记时，使用Dataview插件自动计算并显示从指定日期到当前日期的天数差，入职时间格式“入职时间：xxxx/xx/x” 或者“xxxx-xx-xx”，并且当搜索到离职时间时，截止时间计算到离职时。请编写代码，谢谢！

## ChatGPT:
### 在Obsidian中，每次打开文档时自动计算日期差并以天为单位显示，可以使用Dataview插件和DataviewJS的结合。以下是具体的实现步骤：

### 安装与配置Dataview插件

1. **安装Dataview插件**：
   - 打开Obsidian应用程序，点击左侧的设置按钮（齿轮图标）。
   - 在“社区插件”中，点击“浏览”。
   - 搜索“Dataview”插件，然后点击“安装”。
   - 安装完成后，点击“启用”来启用插件。
2. **配置Dataview插件**：
   - 在“设置”中，找到“Dataview”插件并点击进入其配置页面。
   - 确保 Dataview 插件已启。
   - 在 Dataview 设置中启用“Enable JavaScript Queries”。

### 创建自动计算时间差的笔记

1. **创建笔记**：
   - 打开Obsidian，创建一个新的笔记文件，例如“TimeDifference.md”。
2. **编辑笔记内容**：
   - 在笔记中使用Dataview的 `dataviewjs` 功能来动态计算时间差。以下是一个示例：

1. - 在笔记中使用Dataview的 `dataviewjs` 功能来动态计算时间差。以下是一个示例：


### 时间差计算

从某个日期到今天已经过去了：

```dataviewjs
const targetDate = dv.date("2023-05-01"); // 输入目标日期
const currentDate = dv.date("today");
const differenceInDays = currentDate.diff(targetDate, "days").days;
dv.span(`从 ${targetDate.toISODate()} 到今天已经过去了 ${Math.floor(differenceInDays)} 天。`);
```

### 解释代码

- **目标日期设置**：
  const targetDate = dv.date("2023-05-01"); // 输入目标日期
  

将 `"2023-05-01"` 替换为您要计算的日期。

- **当前日期和时间差计算**：

  ```
  const currentDate = dv.date("today");
  const differenceInDays = currentDate.diff(targetDate, "days").days;
  ```

- **显示结果**：

  ```
  dv.span(`从 ${targetDate.toISODate()} 到今天已经过去了 ${Math.floor(differenceInDays)} 天。`);
  ```

### 使用笔记

1. 保存并查看笔记
   - 保存笔记文件后，每次打开这篇笔记时，Dataview插件会自动计算并显示从指定日期到当前日期的天数差。
  

## Demo.md 中是一个实际可用的例子，可下载后根据需要修改
