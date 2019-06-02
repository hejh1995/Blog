1. 面板结构：
![image](https://github.com/hejh1995/project-img/blob/master/blog/devtool-source-1.png)

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
  - 可以通过 "+" 来添加变量，当添加的变量存在时会显示对应的值，不存在的话则会显示 "not availble"。   - 需要注意的是，这里的变量不会随着代码的执行而发生改变，所以到了下一个状态时，你需要点击刷新按钮来获得关注的变量的新的值。
- call stack：
  - 中断后，显示代码的执行路径。比如在 a() 中调用了 b()，b() 中调用了 c()，那么中断如果在 c() 内部的话，那么 Call Stack 面板会依次显示 c、b、a。
  - 即使在查看调用栈时 也没法看到黑盒脚本里的内容。
- scope：
  - 显示 当前定义的所有属性的值。
  - 还可以在 左侧的代码区域，中断的旁边看到语句中包含的变量的值。
  - 还可以 把鼠标放在变量上面，也显示对应变量的值。
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
  ![image](https://github.com/hejh1995/project-img/blob/master/blog/devtool-source-2.png)
4. 查看和修改值：
- 在中断状态，还可以动态修改变量的值。在按恢复执行之前，在 console 面板里面 改变变量的值，下一次值就被改变了。
- 当程序 中断时，可以在 sources 面板里修改你的代码。
5. 源码调试：
- 现在的项目几乎都是经过编译过的，所以当我们调试时会与编译后的代码打交道，但那并不是我们想要的。不要急，Chrome DevTools 提供了预处理过的代码与源码的映射，主要表现在两点：
  - 在 console 上，源链接指向的是源码，而不是编译后的文件
  - 在 debug 时，在 Call Stack 面板上的源链接指向的也是源码，不是编译后的文件
- 不过需要注意的是，上面所讲的能查看源码的前提是 Chrome DevTools 在设置中提供了相应权限，具体是：Settings - Sources - Enable Javascript source maps / Enable CSS source maps，勾选这两项即可。不过，默认情况下就是勾选。
