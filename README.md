# ohmytodolist 

本项目代码完全由cursor生成。

项目链接：https://ohmytodolist.netlify.app/


生成提示词：

使用 Vue3  创建一个 TODO List工具。

一，功能需求

1，可以添加 和 删除 TODO。

2，可以拖动TODO进行排序。

3，TODO可以打勾，打勾后灰度显示。

4，如果TODO数量超过3个，将第4个以及以后的TODO自动折叠，并显示折叠的TODO数量。

5，当有TODO折叠时，提供展开/折叠按钮，以便可以展开/折叠的TODO。

6，如果全部TODO都打勾完成，屏幕上显示一个大大的玫瑰花🌹鼓励一下用户。

二，实现方式

1，设计一个TodoItem组件来表示TODO，并管理TODO是否打勾的状态。

2，设计一个TodoList组件来管理TODO列表，并提供添加、删除、排序、打勾、折叠、展开等功能。 TodoList 组件是 TodoItem 组件的父组件。

3，设计一个Celebrate组件，当全部TODO都打勾完成时，显示一个大大的玫瑰花🌹鼓励一下用户。

4，设计一个App组件根组件，挂载到index.html页面的Div元素上。

5，请使用单文件组件SFC定义组件，请使用组合式API风格。
