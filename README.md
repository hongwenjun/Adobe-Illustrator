## ScriptPanel_2.jsx
```
ScriptPanel_2 脚本面板是 Adobe Illustrator 的浮动面板，它提供了一个界面来执行其他 .jsx 脚本。
它的工作原理是在与此脚本面板 .jsx 文件相同的文件夹中显示 .jsx 脚本，以及 1 级嵌套文件夹中的脚本。
与脚本面板 .jsx 和级别 1 嵌套文件夹脚本相关的脚本在面板中分组，位于各个组、面板或树视图节点内，具体取决于视图选项。
其他 .jsx 脚本被识别的方法是实际脚本面板 .jsx 文件的目录。
该目录可通过以下三种方式之一获得：
1）$.fileName，从ESTK执行脚本面板.jsx文件时使用，或者File>Scripts，File>Scripts>OtherScripts
2）变量“startupLocation”，它意味着从启动脚本中设置为全局变量，该脚本必须位于应用程序文件夹中的特殊“启动脚本”文件夹中，必须自定义添加。
（Mac 上的“/应用程序/Adobe Illustrator CC 2015/启动脚本”）
变量“startupLocation”应该有脚本面板 .jsx 文件的文件路径，并且在执行后应该设置为 null 或者所有脚本面板都将默认到这个位置。
3) 变量“btScript_MyLocation”，它与从该脚本面板执行的每个脚本一起发送。这意味着为执行脚本提供一个目录来代替 $.fileName，因为当通过 BridgeTalk 对象执行脚本时 $.fileName 不可用，这是浮动面板可以在目标应用程序中执行任何内容的方式。
使用变量“btScript_MyLocation”，可以有一个完整的嵌套脚本面板工具集，每个工具集用于一组单独的 .jsx 脚本和 .jsx 脚本的 1 级文件夹。
注意：由于 $.fileName 的特性，脚本面板脚本无法通过双击文件系统中的图标来执行。 :(
```

## Illustrator JSDoc VSCode Types
```
该项目的目标是使非 TypeScript 用户能够通过使用 JSDoc 注释从 VSCode 的自动完成智能感知中获得一些好处。来自 Types for Adobe 的内容经过处理，将 TypeScript 类声明转换为模拟 javascript 类和类型定义。

要使用，只需在 VSCode 工作区中打开此文档，并在使用正确的注释时激活自动完成功能。

不要在代码中包含该文件，只需将其打开

VSCode 自动补全

现在，简单的 JSDoc 智能感知甚至可以在不创建 TS 项目及其配置的情况下启用临时丢弃的片段。

VSCode 自动补全

不再搜索网页或 PDF，对于 Adobe 脚本类、枚举和方法的类型中的大多数这些长期存在的最后记录。

笔记：

遗产
VSCode 不太支持 (02/2021) 类继承和 @extends/@augments 关键字。 （也是@returns 关键字。）因此，将扩展类的类变成一个以“JSDocType”为后缀的额外类，然后编写一个新的@typedef 语句，将此类与继承的类结合起来：

类继承类{
/** @type {string} - 示例基础属性 */
基础属性；
}

class InheritingClassJSDocType {
/** @type {string} - 示例子类属性 */
类属性；
}

/**
 * @typedef { InheritedClass & InheritingClassJSDocType } InheritingClass
 */
现在，当一个变量用 @type {InheritingClass} 注释时，它的自动完成应该识别 baseProperty。

文件类
由于 VSCode 会自动转到 HTML“文档”，因此将 Document 类重命名为 AiDocument 以区分它们。

创建方法
这是怎么做的？具有解析功能的节点可执行 javascript 文件通过操作字符串将 Adobe 文件的类型转换为 JSDoc 文件。它依赖于 Adobe .d.ts 文件类型中的通用结构约定，例如非常一致的注释、用空行分隔块以及每个地方的 TS 标签注释 - 甚至 :void 作为方法的返回标签.

类声明变成了真正的模拟javascript类，函数声明变成了真正的属性，以方便JSDoc自动完成。然而，方法主体不存在。这些类是真正的 JS 构造，但是它们不会在代码中使用，因为该文件不会在代码中使用。只需在 VSCode 中打开它即可创建自动完成功能！
```
