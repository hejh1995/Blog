1. 面板结构：
img
2. 添加断点 与 断点类型：
 - 普通断点：在 中间面板 的 代码行号的位置处点击 代码行号，就可以为 相应的行添加断点。
 - 条件断点：右键 行号， 可以为没用添加 断点的行 选择 ‘Add conditional breakpoint’ 添加条件断点。输入条件，在条件满足的时候，断点才会生效。（条件断点一般是黄色）
 - 行内断点：添加同上面，第一个断点处于激活状态，其他需要点击激活才能生效。（应该是因为这一行有多个执行吧）
 - 修改断点：
 - 删除断点：remove breakpoint
 - 忽略断点：disable breakpoint
 - 黑盒脚本：blockbox script。一个脚本文件标记为 "Blackbox Script"，那么我们就永远不可能进入这个文件内部，这个文件对我们来讲就是一个黑盒子。为什么要强调“永远”呢？因为不仅普通的断点不能访问这个被标记了的脚本，其他的，比如说 DOM 断点、事件断点等等都无法访问那个脚本文件内部。
3. 面板介绍：
- watch：
- call stack：
- scope：
- break points：
  - 会显示 所有通过行号 留下的断点，可以右键管理某个或者全部断点：
  - Remove Breakpoints：删除选中的断点
  - Deactivate Breakpoints：暂时忽略所有断点
  - Disable all Breakpoints：功能同上（与上一功能有细微差别，但表现类似）
  - Remove all Breakpoints：删除所有断点
- XHR Breakpoints：
  - XHR 断点，ajax 调用的触发点和调用堆栈。最新的 Chrome DevTools 中要么为所有 ajax 调用添加断点，要么都不添加断点。
- DOM Breakpoints：
  - DOM 断点。
- GlobalBreakpoints：
  - 
- Event ListenerBreakpoints：
  - 展开 Event Listener Breakpoints 可以看到一组事件类型，展开一个事件类型可以看到具体的事件名称。
  - 每个事件名称和事件类型前面都有个复选框，选中即指  当页面中触发了所选的事件的话，就会触发中断。
- 异常中断：
  - 选中 "Pause on exceptions --- pause on caught exceptions" 按钮，当执行的脚本出现异常时会触发中断。
