# How-to-Chisel-DLCO-Lab
Trouble shooting of using Chisel in Nanjing University DLCO Lab Course.


- Chisel环境安装中出现各种奇怪的问题（Connection Refuse）   
挂梯子。同时，建议使用模板仓库+sbt构建(网上有教程)，而不是用scala-cli  
- 如何通过OJ？Chisel可以生成Verilog吗？  
目前版本的Chisel无法生成Verilog代码，只能输出SystemVerilog。（已经在开发者论坛上向项目维护者确认过）  
可以采用一个开源工具 [sv2v](https://github.com/zachjs/sv2v)  来展开automatic等语法，获得用于通过OJ的Verilog的代码。（目前整个方法还没出现问题）  
- Chiseltest会出现无法引入的问题  
  1. 可以使用自带的Scalatest
  2. 使用ChiselTest https://github.com/ucb-bar/chiseltest  
    但是ChiselTest 官方`README`上面的仓库链接是无效的，  
    经过反复尝试，需要将`README`中的 Dependency  
    `libraryDependencies += "edu.berkeley.cs" %% "chiseltest" % "5.0-SNAPSHOT”`  
    替换为  
    `"edu.berkeley.cs" %% "chiseltest" % "6.0.0”`  
    引入方式为  
    ```scala
    import chiseltest._
    import org.scalatest.flatspec.AnyFlatSpec
    ```  
    使用方法可以参考[CSDN Blog](https://blog.csdn.net/weixin_43681766/article/details/125590735) 或者官方Repo上面的例子。

- 报错“实例化时未初始化为Module”的问题?  
    模块实例化的时候必须初始化为`Module`(即使是组合电路继承自`RawModule`)  
- 增加test object后，出现sbt test无法找到的问题？  
    test的.scala文件必须在template的test文件夹里
- 明明把BlackBox的原文件放进resources文件夹了，为什么还显示找不到？
  sbt clean 以下
- 注意不能使用 `Y = (X.asSInt).asUInt`进行符号拓展，注意自动拓展发生的位置。
