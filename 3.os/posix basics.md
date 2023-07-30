# stdin stdout stderr pipes

当在Unix-like操作系统中运行程序时，有三个标准流（stdin、stdout和stderr）以及管道（pipes）起着重要的作用：

- 标准输入（stdin）：stdin是标准输入流，用于从程序中读取输入数据。默认情况下，stdin与键盘相连，允许程序从用户那里读取输入。但是，您可以通过shell重定向（`<`）或管道（`|`）将stdin重定向为从文件或其他命令读取输入。

- 标准输出（stdout）：stdout是标准输出流，用于将程序的常规输出或结果数据写入。默认情况下，stdout与终端相连，程序的输出会显示在屏幕上。与stdin类似，您也可以通过shell重定向（`>`）或管道（`|`）将stdout重定向为写入到文件或其他命令。

- 标准错误（stderr）：stderr是标准错误流，用于从程序写入错误消息或诊断信息。与stdout不同，stderr不受shell重定向影响。默认情况下，它也与终端相连，因此错误消息会与常规输出一起显示在屏幕上。但是，您可以使用`2>`来单独重定向stderr，或使用`2>&1`一起重定向stdout和stderr。

- 管道（pipes）：管道（`|`）用于连接一个命令的输出到另一个命令的输入，使它们在一个链条中协同工作。例如，您可以使用以下命令在文件中搜索特定模式并计算出现次数：
  ```
  cat file.txt | grep "pattern" | wc -l
  ```
  在这个命令中，`cat file.txt`的输出被管道传递给`grep "pattern"`，而`grep "pattern"`的输出又被管道传递给`wc -l`。这样，这些命令组合在一起实现所需的功能。

管道是Unix-like系统中的一个强大特性，允许您将多个命令链接在一起，轻松处理和操作数据。它体现了Unix的设计哲学：“小而简单的工具做好一件事，并且可以组合在一起完成更复杂的任务。”



- stdin is represented by file descriptor 0
- stdout is represented by file descriptor 1
- stderr is represented by file descriptor 2