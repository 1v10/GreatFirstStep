## COBOL

#### 背景

- [Cobol Basics | Cobol | Free Cobol | Learn Cobol | Cobol Tutorial | Cobol Books | Cobol Interview Questions | Cobol FAQ | Cobol Preparation (academictutorials.com)](http://www.academictutorials.com/cobol/cobol-basics.asp)
- [COBOL - 快速指南_学习COBOL|WIKI教程 (iowiki.com)](https://iowiki.com/cobol/cobol_quick_guide.html)
- [COBOL数据类型 - COBOL教程 (yiibai.com)](https://www.yiibai.com/cobol/cobol_data_types.html)
- 为国防领域和金融领域而设计 因为其先进的文件处理 所以其可以处理文件和大量数据  也可以处理数据库
- COBOL在线执行网站:
  - [Home - Replit](https://replit.com/~)  支持工程化 支持读取PS文件
  - https://www.jdoodle.com/ 支持工程化 支持读取文件
  - [GDB online Debugger | Compiler - Code, Compile, Run, Debug online C, C++ (onlinegdb.com)](https://www.onlinegdb.com/) 简单执行
  - [Online Cobol Compiler (tutorialspoint.com)](https://www.tutorialspoint.com/compile_cobol_online.php) 简单语句执行

### Cobol VScode环境配置

- 显示代码内部执行过程
  - 按照该拓展 COOBL代码内右键选择Generate Cobol Control Flow
  - ![image-20240404112112068](https://raw.githubusercontent.com/1v10/Photo/main/photo/202404041123743.png)
- 编写好COBOL代码,会有对应的JCL(与MainFrame交互的命令)
- 代码在CBL文件夹,以CBL结尾,执行文件在JCL文件夹,以JCL结尾
- 右键想运行的CBL对应的JCL:点击Submit JOB即可

![image-20230611182419693](https://raw.githubusercontent.com/1v10/Photo/main/photo/202306111824734.png)

- 此时在VSCODE JOS视图可以看到相对应的运行结果 会以文件形式出现,查看各个文件内容即可,如DISPLAY语法显示如下

- ![image-20230611182439246](https://raw.githubusercontent.com/1v10/Photo/main/photo/202306111824288.png)

- 使用命令行执行:Zowe CLI

  - 环境配置文件确认判断

  ```cobol
  	zowe config list --locations
  ```

  - 一下命令可以确认是否连接到Z/OS 

  ```
  zowe zosmf check status
  ```

  - 列出相关文件

    ```cobol
    zowe files list ds "文件名.*"
    ```

  - 下载文件到本地

    ```
    zowe fukes downliad am "Z95526.JCL" -e "JCL"
    ```

  - 提交JCL:可以直接看到输出结果

    ```
    zowe jobs submit ds "Z95526.JCL(HELLO)" --vasc
    ```

  - 提交并下载文件

    ```
    zowe jobs submit ds "Z99998.JCL(HELLO)" -d.
    ```

  - 逐步提交以查看各个执行文件

    ```
    	zowe jobs submit ds "Z99998.JCL(HELLO)" --wfo
    ```

    - 以上命令执行完会得到一个JOBID

    ```
    	zowe jobs view sfbi JSBID 
    ```

    - 上一步返回具体的各个运行文件 通过以下命令可以具体查看

      ```
      zowe jobs view sfbi JOBID 具体文件
      ```

  - 使用node.js自动化编译、提交、运行

    - 在当前文件夹输入

      ```javascript
      npm init
      ```

    - 返回到VS的正常打开文件视图,可以看到有一个PACKAGE.json文件, 在scripts中即可配置我们对应命令所执行的简略命令

      ![image-20230611184955410](https://raw.githubusercontent.com/1v10/Photo/main/photo/202306111849447.png)

    - 回到ZOWE EXPLODRE 此时修改HELLO.cbl的display文字,然后可以直接使用NPM命令,提交编译

  
  
- 关联文件

  - .COBOL
  - .CBL
  - .COB
  - .COBCOPY
  - .COPYBOOK
- .COPY

- VSCO相关技巧

  - CTRL+G 输入行号 可导航至该行代码

  - CTRL+鼠标左键变量到定义处

  - 鼠标悬停在变量上,将显示该变量的声明

    <img src="C:%5CUsers%5CPhelop%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20230528164709321.png" alt="image-20230528164709321" style="zoom: 80%;" />

  - 按住CTRL鼠标悬停在变量上可查看更多信息

  - 左侧大纲视图(outline)可以展示程序结构和变量,可以很方便转到特定部分

    ![image-20230528165448584](https://raw.githubusercontent.com/1v10/Photo/main/photo/202305281654641.png)

- 顶部面包屑导航会显示当前的所在结构

  ![image-20230528165836513](https://raw.githubusercontent.com/1v10/Photo/main/photo/202305281658548.png)

- 点击面包屑导航会高亮显示该区域并显示该区域大纲视图

  <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202305281659697.png" alt="image-20230528165955594" style="zoom:67%;" />

- 如果要查看处理过程具体内容而不跳转过去,会弹出一个悬浮框,显示具体内容,如果是变量还是会跳转

  - 右键→go to References

    ![image-20230528170652463](https://raw.githubusercontent.com/1v10/Photo/main/photo/202305281706504.png)

  - go to de definition 则会跳转声明处处

- 批量变量更名:右键→查看所有引用 F2输入新名称即可

### COBOL语法

- 范围终止语句:END-或者.

  - 条件语句或者具有条件子句都将有终止语句

- 结构构成

  ![image-20230528202112799](https://raw.githubusercontent.com/1v10/Photo/main/photo/202305282021838.png)

  - statements:短语:以Cobol保留字开头的逻辑
  - sentences:语句:包含多个短语
    - 一系列以 .结尾多个COBOL语句
  - paragraph:段落,包含多个语句,是节或者部的细分
    - 陈述的主题
  - section:节,包含多个段落
    - 处理逻辑的细分
  - division:部,包含多个节
  - program:程序自身
  - <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202403031555890.png" alt="image-20240303155459726" style="zoom:50%;" />

- 四个部

  - Identification Divesion 标识部:程序标识 用来程序相互识别 其实类似于类名
    - 比如程序ID(必须项) 作者之类
    - <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202403031952906.png" alt="image-20240303195232862" style="zoom:50%;" />
  - Environment Division 环境部:程序环境配置 
    - Input-Output Section:指定环境 的输入输出文件 以及文件类型等等
      - 当前程序中文文件名为FILTEN 然后与物理文件DDNAME关联 该句用来告诉JCL当前 逻辑文件名与那个物理文件关联
        - JCL:IBM大型机系统级别语言 作业控制语言 用来管理和调度大型机上的作业
      - 下面一行SEQUENTIAL表示文件中的记录是连续的  文件的组织方式
        - 文件的组织方式指的是文件中记录的排列方式和组织结构。在计算机中，常见的文件组织方式包括：
          - 顺序组织（Sequential Organization）：文件中的记录按照它们在文件中出现的顺序依次排列，记录之间没有直接的逻辑链接关系。顺序组织的文件通常用于顺序访问，即从文件的开始处逐条读取记录。
          - 索引组织（Indexed Organization）：文件中的记录按照某种顺序排列，并且每个记录都有一个对应的索引项，索引项存储了记录在文件中的位置信息。通过索引项，可以快速地定位和访问文件中的记录，而不需要顺序地扫描整个文件。
          - 随机组织（Random Organization）：文件中的记录存储在按照记录键值（Key）排序的区域中，每个记录都有一个唯一的键值。随机组织的文件允许根据记录的键值直接访问和检索记录，而不需要进行顺序查找。
      - <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202403031958355.png" alt="image-20240303195858314" style="zoom:50%;" />
    - Configuration Section:提供有关编写和执行的系统信息
      - 比如以下SOURCE指的是 编写和指定源代码的计算机 OBJECT指的是执行的计算机
      - <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202403031955949.png" alt="image-20240303195504907" style="zoom:50%;" />
  - Data division 数据部:程序变量,文件内容
    - File Section 文件节 定义文件的记录结构
      - 如下图针对上边定义的文件 进行了PIC内容的定义 定义文件的内容为一个A(字母字符 A-Z,a-z) 长度为25
      - <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202403032008091.png" alt="image-20240303200838038" style="zoom:50%;" />
    - 以下三个节 分别定义了三个区域的变量 定义方式没有太大区别 主要是用法和生命周期
    - <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202403032024623.png" alt="image-20240303202405564" style="zoom:50%;" />
    - Working-Storage section 工作存储节 定义程序中内部使用的变量  程序启动时分配内容 
    - Local-Storage section:定义的是某个特定部分的变量  局部变量 程序每次调用时都会分配内存和初始化变量 
    - Linkage section:用于定义程序与程序之间传递数据的变量 生命周期由另一个程序控制  link区 容许一个程序访问另一个程序的数据区 或者接受从调用程序传递过来的参数 
      - 数据交换不一定适用该途径
      - copy命令可以引入外部文件定义的代码段  这些外部 文件通常包含数据结构定义 常量生命等 被存放在单独的文件中以便多个程序共用 
      - 虽然 copy文件本身不负责数据的直接传递 但他保证了 数据交换双方使用一致的数据结构  实际的数据可以通过数据库或者外部存储完成  一个程序可以将数据写入一个共享文件 另一个程序读取 
      - copy文件 .cpy  本身就是定义数据布局或者常量  可以在多个程序之间共享代码和数据布局 里面的定义会被插入到该语句所在位置 类似于其他语言的import或者suing避免了代码重复, 使用`COPY`语句引入的代码就好像是直接写在主程序文件中一样
      - 插入布局的操作是由编译阶段 编译器完成的
  - Procedure division 过程部:操作指令  
    - 是程序完成工作的地方,statements便在此处
    - 包含程序的逻辑 使用由数据区定义的变量的可执行语句组成
    - 段落和节名由用户自定义 
    - 例如以下  我们在过程部编写 逻辑区域 打印Hello World!
    - <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202403032040376.png" alt="image-20240303204044327" style="zoom:50%;" />

- JCL:负责与z/OS交互,包括让编译代码, 让z/OS执行

- zome CLI:如果npm安装后 --version报错,再安装一个安全模块即可

  ```java
  zowe plugins install @zowe/secure-credential-store-for-zowe-cli
  ```

#### 基本语法

- 字符:一共有78个单字符 大小写字母 各种符号等

  - <img src="C:%5CUsers%5CPhelop%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240304215817097.png" alt="image-20240304215817097" style="zoom:50%;" />

- 格式：cobol的字符必须以某种格式书写 cobol的列都具体特定的含义

  - ![image-20240310190006009](C:%5CUsers%5CPhelop%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240310190006009.png)
  - 1-6列:行号列
  - 7列:注释列 如果该列有*号 代表该行是注释行
  - 8-11列:Cobol的 division section paragraphs和一些特殊的条目必须在该列开始！
  - 12-72列：所有的COBOL语句必须在B区开始
  - 73-80列：标识区域　根据程序员需要使用

- 字符串

  - 字符串由单个字符组成
  - 所有字符串必须有分隔符
  - 分隔符用于分割字符串
  - 常用分隔符：空格，逗号，句号，撇号，左右括号，引号
  - 一个字符串可以是注释　也可也是关键词　也可以是文字

- 程序中有一些名称是保留字　不能当作名称！

- 变量定义：

  - 级别编号　数据名称　Picutre-Clause Value-Clause

    - CLAUSE:子句 代表PIC定义的子句 指定特定属性和行为 定义数据项的格式 告知编译器数据应该是什么样子的 例如X代表一个字母 9代表一个数字

  - 级别编号:用于指定记录中的数据级别,用于区分基本项目和组项目,因此会有两种类型的项目

    - 简单理解就是单个变量 和集合变量

    - 01:记录描述级别

      - 定义数据,文件,表结构 可以决定是一个组项目还是基本项目  是数据的最外层结构

    - 02~49:组和基本项目

      - 数据使用之前必须定义 给出数据名称 数据名称给出了实际内存的引用

      - 不能使用COBOL保留字 

      - 以下是组数据和基本数据

      - ```cobol
               WORKING-STORAGE SECTION.
               01 BASIC1 PIC 9(3) VALUE 100.
               01 GROUP1.
                       05 GROUP1-ITEM1 PIC X(20).
                       05 GROUP1-ITEM2 PIC X(20).
        ```

        

    - 66:重名名子句 可以用来重命名某些数据项

    - 77:用于定义顶层的数据项或组。它是最高级别的数据定义级别

    - 88:定义条件名 容许在程序中为 某些条件指定名称 并根据条件进行条件判断

      ```cobol
      88 IS-REGISTERED VALUE 'R'.
      88 IS-DROPPED    VALUE 'D'.
            
      IF STUDENT-STATUS IS REGISTERED
          DISPLAY 'This student is registered.'
      ELSE IF STUDENT-STATUS IS DROPPED
          DISPLAY 'This student has dropped the course.'
      END-IF.
      ```

      

- 基本项目(elementary item)/组项目(group item)

  - 9:Numberic(0-9)
  - A:Alphabetic(A-Z,a-z或者空格)
  - X:任意字符
  - V:隐式小数 指定小数点的位置  该符号会格式话数字 比如9(5)V9(2) 如果一个小数为"12.21"会在12前面加入3个空格 以保持小数点在第6位
  - S: 符号 标识该数字是带符号的 比如
    - PIC S9(3) VALUE -100
  - 定义时可以直接给初始值

- 命名格式

  - 关键词:PIC 决定变量长度和类型

    - PIC 9 长度为1的单个数值
    - PIC 9(4) 长度为4的四个数值
    - PIC X 单个字母数字
    - PIC X(4) 四个字母数字
    - PIC 9(2)V9 V代表小数点: 10.9

  - 除了X和9还有其他类型,比如A,仅仅只有字母

    - cs:货币符号

  - 变量/数据项的编码在DATA DIVISION中定义

    - Level Number:级别编号 记录数据的层次结构
    - Variable name/data-item name:变量名/数据项名称,为程序引用的字段指定一个名称

  - 保留字值

    - ZERO ZEROS
    - SPACE SPACES
    - NULL NULLS

  - 程序结构:通过级别指示符和级别编号系统进行定义

  - 赋值

    - MOVE 值 TO 变量名
    - COMPUTR 变量名 = 值;

    ## 操作语句

  - Accpet:接收JCL或者用户的输入

    - JCL:比如接受系统日期 用户名称 从操作系统获取数据 接受后可以显示或者使用
    - 用户输入:接收用户键盘的输入
    - 语法:ACCEPT DATE

  - Display:显示Cobol程序的输入

    - 类似于其他语言的Console语句
    - 语法:DISPLAY 变量名称或者字符串

  - Initialize:初始化语句 用来初始化组变量和基本变量

    - 如果时字符串 那么就放入空格 如果是数字 那么就放入0
    - 语法:INITIALIZE 变量名称
    - 如果你在COBOL中声明了一个变量，并立即使用`INITIALIZE`语句对其进行初始化，而该变量在此之前没有被赋予任何其他值，那么使用`INITIALIZE`语句可能看起来没有产生任何可见的效果。这是因为新声明的变量已经有了默认的初始状态，而`INITIALIZE`语句仅仅是将变量重置为这些默认状态

  - Move:变量移动语句 将原数据移动到目标数据 需要指定变量名称

    - 语法:MOVE  变量名称1或者字面值 TO 目标变量名称

  - ADD:加法语法 将两个或两个以上数字相加 并将结果添加到目标变量

    - 语法:ADD A TO C GIVING B 将A加到C上并且将结果赋给B 
    - 如果不写GIVING B  默认赋给C

  - Subtract:减法操作 从一个变量中减去一个变量 

    - 语法 类似ADD :   SUBTRACT A FROM B GIVING C 从B中减去A

  - Multiply:乘法操作

    - MULTIPLY A BY B GICING E      E = A*B
    - 与之前语境不太一样 是by 是A*B 而不是之前以B为主了

  - Devide:除法操作

    - DEVIDE A BY B GIVING  C REMAINDER  R
      - 将A除以B 结果放到C中 余数放到R中

  - COMPUTE:通用操作符 可以执行各类复杂运算 直接使用+-*/符号即可

    - COMPUTE A = (B+C)*D  可以直接写符号当作复杂运算

    ```cobol
    PROCEDURE DIVISION.
        COMPUTE Sum = Num1 + Num2.
    ```

  - DEMO

    ```cobol
    
           IDENTIFICATION DIVISION.
           PROGRAM-ID. HELLO.
           DATA DIVISION.
           FILE SECTION.
           WORKING-STORAGE SECTION.
           01 WS-ACCEPT PIC A(15).
           01 WS-NAME PIC X(15).
           01 WS-NAME2 PIC 9(15).
           01 WS-NAME3 PIC 9(15).
           01 WS-NAME4 PIC 9(15).
           01 WS-NAME5 PIC 9(15).
           01 WS-NAME6 PIC 9(15).
           01 WS-NAME7 PIC 9(15).
           01 WS-NAME8 PIC 9(15).
           01 WS-NAME9 PIC 9(15).
           01 WS-NAME10 PIC 9(15).
           01 WS-NAME11 PIC X(15).
           01 GROUP1.
                   05 GROUP1-ITEM1 PIC X(20).
                   05 GROUP1-ITEM2 PIC X(20).
           PROCEDURE DIVISION.
           MAIN-PROCEDURE.
                ACCEPT WS-ACCEPT.
                MOVE WS-ACCEPT TO WS-NAME.
                DISPLAY 'WS-ACCEPT:' WS-ACCEPT.
                DISPLAY 'WS-NAME:' WS-NAME.
                
                DISPLAY 'WS-NAME2:' WS-NAME2.
                INITIALIZE WS-NAME2.
                DISPLAY 'WS-NAME2:' WS-NAME2.
                
                DISPLAY 'WS-NAME11:' WS-NAME11.
                INITIALIZE WS-NAME11.
                DISPLAY 'WS-NAME11:' WS-NAME11.
                
                DISPLAY 'WS-NAME3:' WS-NAME3.
                DISPLAY 'WS-NAME4:' WS-NAME4.
                DISPLAY 'WS-NAME5:' WS-NAME5.
                
                MOVE 3 TO WS-NAME3.
                ADD WS-NAME2 TO WS-NAME3.
                DISPLAY 'ADD WS-NAME2:' WS-NAME2.
                
                ADD WS-NAME2 TO WS-NAME3 GIVING WS-NAME4.
                DISPLAY 'ADD WS-NAME2:' WS-NAME4.
                
                MOVE 7 TO WS-NAME5.
                SUBTRACT WS-NAME4 FROM WS-NAME5 GIVING WS-NAME6.
                DISPLAY 'WS-NAME6 :' WS-NAME6.
                
                MULTIPLY WS-NAME6 BY WS-NAME5 GIVING  WS-NAME7.
                DISPLAY 'WS-NAME7:' WS-NAME7.
                
                DIVIDE WS-NAME7 BY WS-NAME5 GIVING WS-NAME8 
                REMAINDER WS-NAME10.
                
                DISPLAY 'WS-NAME8:' WS-NAME8.
                DISPLAY 'WS-NAME10:' WS-NAME10.
                
                
                DISPLAY 'WS-NAME2:' WS-NAME2.
                DISPLAY 'WS-NAME3:' WS-NAME3.
                DISPLAY 'WS-NAME4:' WS-NAME4.
                COMPUTE WS-NAME9 = (WS-NAME2 + WS-NAME3) * WS-NAME4. 
                DISPLAY 'WS-NAME9:' WS-NAME9.
                
                STOP RUN.
           END PROGRAM HELLO.
    
    ```

     运行结果:

    ```cobol
    hellow
    WS-ACCEPT:hellow         
    WS-NAME:hellow         
    WS-NAME2:000000000000000
    WS-NAME2:000000000000000
    WS-NAME11:               
    WS-NAME11:               
    WS-NAME3:000000000000000
    WS-NAME4:000000000000000
    WS-NAME5:000000000000000
    ADD WS-NAME2:000000000000000
    ADD WS-NAME2:000000000000003
    WS-NAME6 :000000000000004
    WS-NAME7:000000000000028
    WS-NAME8:000000000000004
    WS-NAME10:000000000000000
    WS-NAME2:000000000000000
    WS-NAME3:000000000000003
    WS-NAME4:000000000000003
    WS-NAME9:000000000000009
    ```

    ## Data Layout 

  - 数据布局将表达如何组织和标定数据

  - Redefines 重定义子句 

    - 容许以不同的方式解释同一片内存区域的数据 不需要占用额外的空间

    - 比如原来定义了两个变量a=a,b=b, 你可以重定义这块内存c=ab,而c不需要占用额外的内存,此时既可以单独访问a, 也可以访问ab

    - 该定义使得一个已经定义的数据项重定义为另一种结果或者类型 对相同的数据进行不同的解释

      ```cobol
             WORKING-STORAGE SECTION.
             01 EMPLOYEE-NAME.
                 05 FIRST-NAME PIC X(10) VALUE 'JANE'.
                 05 LAST-NAME PIC X(15) VALUE 'DOE'.
             01 FULL-NAME REDEFINES EMPLOYEE-NAME PIC X(25).
      ```

    - 以上语句 将名和姓变量合并为另一个变量姓名 姓名并不占内存 只是将原来的两个变量解释为一个变量,也不会影响原变量,与原变量占据了相同的存储区域  
    - 数据解释:重定义后的变量并没有修改原内存地址中的值 只是换了一种方式进行解释 共享内存区域
    - 数据共享性:此时修改重定义的之后的变量 也会影响原变量 因为是同一内存地址 本质上修改了原变量占据的内存区域
    - 数据有效性与长度:重定义长度不应该长于原始内存长度 如果改变数据类型 也要付和语法 否则会导致混乱错误  比如将字符串ABC改为数字类型 语法上容许 但是使用该数字类型计算时会报错

  - Renames 重命名子句

    - 用于给现有的数据项和数据结构赋予别名  可以给一组或单个数据起别名 操作别名即可操作这一组数据

    - 使用场景:需要组合不同位置的数据项时 可以将这些数据项视为一个整体 简化访问 物理储存没有变更

    - ```cobol
      01 EMPLOYEE-RECORD.
         05 EMPLOYEE-ID     PIC X(5).
         05 EMPLOYEE-NAME   PIC X(20).
         05 EMPLOYEE-ADDRESS.
             10 STREET      PIC X(15).
             10 CITY        PIC X(15).
             10 ZIP-CODE    PIC X(5).
         05 EMPLOYEE-STATUS PIC X(1).
      
      01 EMPLOYEE-CONTACT RENAMES EMPLOYEE-ADDRESS THRU EMPLOYEE-STATUS.
      ```

    - THRU  是指定该新名称重命名的数据范围 如上所属 新变量名称代指了从05-ADDRESS到STATUS的多个变量

    - 限制:

      - 必须使用级别号66 这是重命名专属级别
      - 重命名的数据必须是一个连续区域 不能跳过中间数据项 使用THRU来指定区域的起点的终点
      - 重命名的数据必须在同一组内 必须有共通的父项  
      - 不能使用88,77级别
      - 不影响数据结构 只是访问上简化

  - Usage:指定数据项的存储方式 指示该数据在内存中如何存储

    - DISPLAY :默认类型 以字符形式存储  最常用 适合读取和打印 但不是存储或计算的高效方式  以人类可读的文本形式存储
    - BUBARY,COMPUTATIONAL(COMP) 指示数据以二进制格式存储 COMP用于整数 根据计算机和编译器架构 可能占不同的个字节 二进制精度高 浮点数计算误差小 节省空间 
      - 数字直接转换为等价的二进制进行存储
      - 数据项必须是数字类型!
    - COMP-3:打包十进制 使用二进制存储十进制数字
      - 比如comp直接存储数字123的二进制形式 01111011 而comp3会使用4位存储一个十进制数字 即四位存储1 四位存储2 四位存储3 四位就是半个字节 默认存储整数符号 形成0001(1) 0010(2) 0011(3) 1100
    - COMP-1:数据以单精度浮点数格式存储
      - 类似于Float 以十六进制形式存储
    - COMP-2:数据以双精度浮点数个数存储
      - 类似于Double  以十六进制格式存储
    - 注意 无论什么类型 物理形式上 都是二进制上存储 这里说的是存储前的数据形式 以及逻辑表示和处理方式
      - 比如数字123 如果 我们不指定COMP 默认以DISPLA存储 其会按照相关编码(ASCII) 将数字转为特定编码比如 49 50 51 (二进制 00110001 00110010 00110011)然后进行存储
      - 而如果我们使用123 comp形式存储 将会直接存储123的二进制形式 01111011 二进制更加紧凑高效

  - Copybooks

    - Copybooks是用户定义数据结构 是一个独立的文本文件 里面描述了cobol程序复用的代码段 通常包含Data Layout 其他程序可以使用COPY 文件名来进行引用 COPY XXX.CPY

    - 如果一个特定的数据结构很多程序都在使用,那么我们将使用copybooks来进行定义

      ```cobol
        COPY 'CUSTOMER.CPY'.
      ```

  - Demo

    ```cobol
          ******************************************************************
          * Author:
          * Date:
          * Purpose:
          * Tectonics: cobc
          ******************************************************************
           IDENTIFICATION DIVISION.
           PROGRAM-ID. YOUR-PROGRAM-NAME.
           DATA DIVISION.
           FILE SECTION.
           WORKING-STORAGE SECTION.
           01 WS-NAME PIC A(15).
           01 WS-NAME-RED REDEFINES WS-NAME PIC X(10).
           01 WS-NUMBER.
               05 WS-NUM1 PIC 9(2).
               05 WS-NUM2 PIC 9(2).
               05 WS-NUM3 PIC 9(2).
               05 WS-NUM4 PIC 9(2).
           66 WS-RENAME RENAMES WS-NUM2 THRU WS-NUM4.
           
           COPY STRUC.
           PROCEDURE DIVISION.
           MAIN-PROCEDURE.
                DISPLAY "Hello world"
                DISPLAY 'WS-NAME:' WS-NAME.
                DISPLAY 'WS-NAME-RED:' WS-NAME-RED.
                
                MOVE 'TUTORIALSPOINT' TO WS-NAME.
                DISPLAY 'WS-NAME:' WS-NAME.
                DISPLAY 'WS-NAME-RED:' WS-NAME-RED.
                
                MOVE'DOTCOM' TO WS-NAME-RED
                DISPLAY 'WS-NAME:' WS-NAME.
                DISPLAY 'WS-NAME-RED:' WS-NAME-RED.
                
                MOVE 11223344 TO WS-NUMBER.
                
                DISPLAY 'WS-NUMBER:' WS-NUMBER.
                DISPLAY 'WS-NUM1:' WS-NUM1.
                DISPLAY 'WS-NUM2:' WS-NUM2.
                DISPLAY 'WS-NUM3:' WS-NUM3.
                DISPLAY 'WS-NUM4:' WS-NUM4.
                DISPLAY 'WS-RENAME:' WS-RENAME.
                DISPLAY 'WS-LAST-NAME:' WS-LAST-NAME.
                STOP RUN.
           END PROGRAM YOUR-PROGRAM-NAME.
    
    ```

    ```cobol
          * COPY: STRUC.cpy
    000100 01 WS-LAST-NAME PIC A(5) VALUE 'JIM'.  
    ```

    

    ```COBOL
    Hello world
    WS-NAME:               
    WS-NAME-RED:          
    WS-NAME:TUTORIALSPOINT 
    WS-NAME-RED:TUTORIALSP
    WS-NAME:DOTCOM    OINT 
    WS-NAME-RED:DOTCOM    
    WS-NUMBER:11223344
    WS-NUM1:11
    WS-NUM2:22
    WS-NUM3:33
    WS-NUM4:44
    WS-RENAME:223344
    WS-LAST-NAME:JIM  
    
    Process finished with exit code 0
    ```

  - 由于原数据WS-NAME长度为15,而重新定义的数据长度为10 所以将15个字符赋给原变量,重定义变量只显示了前十个字符 其指向了原变量内存区域的前十个变量

  - 当前将DOTCOM赋给重定义变量 发现重定义变量变成了'DOTCOM    '  而原始变量 直接编程课DOTCOM    OINT  也就是说重定义变量被改变 只会改变对应内存区域对应的部分 其余部分还是会保留

  - 然后将一串字符串赋给了一个组项目名称 然后输入各子项目 发现变量自动按照长度分别赋值  

  - 使用重名语句 命名 WS-NUM2~WS-NUM4 之后会输出这个范围的值

  - 最后使用  COPY STRUC. 引入了cpy文件 里面只定义了一个变量 引入后 即可以使用 显示

    ## Conditional 条件语句

    - IF-ELSE

      - 条件分支语句 如果条件为真 则执行IF语句 条件为假则执行ELSE语句

        ```cobol
        IF [condtion] THEN
        	[IF COBOL statements]
        ELSE
        	[ELSE COBOL statements]
        END-IF.
        ```

      - 这里可以不写ELSE分株

      - 也可以不写ENG-IF.显式结束 可以在语句后面加.来结束

          

        ```cobol
        IF [condtion] THEN
        	[IF COBOL statements]
        ELSE
        	[ELSE COBOL statements].
        ```

      - SIGN

        - 符号语句 可以使用符号来检查数值变量
        - POSTIVE:数据项为正数 条件为真
        - NEGATIVE:数据项为负数 条件为真
        - ZERO:数据项为0 条件为真
        - 使用IS/NOT 衔接
        - [DATA NAME]  [IS/NOT] [POSITIVE/NEGATIVE/ZERO]

        ```cobol
               IDENTIFICATION DIVISION.
               PROGRAM-ID. YOUR-PROGRAM-NAME.
               DATA DIVISION.
               FILE SECTION.
               WORKING-STORAGE SECTION.
               01 WS-NAME PIC X(2) VALUE '01'.
               01 WS-SIGNNAME PIC 9(2) VALUE 12.
               PROCEDURE DIVISION.
               MAIN-PROCEDURE.
                    DISPLAY 'WS-NAME :' WS-NAME.
                    IF WS-NAME = '01' THEN
                        DISPLAY 'TRUE'
                    END-IF.
                        
                    IF WS-SIGNNAME IS POSITIVE
                        DISPLAY 'POSITIVE'
                    END-IF.
                        
                    IF WS-SIGNNAME NOT NEGATIVE
                        DISPLAY 'NOT NEGATIVE'
                    END-IF.    
                    
                    STOP RUN.
               END PROGRAM YOUR-PROGRAM-NAME.
        ```

        

      - Class

        - 类别条件 可以检查数据是什么类型 大写,小写,是否是字母等
        - SPCES/SPACES:是否为空格
        - ALPHABETIC:是否为字母
        - ALPHABETIC-LOWER:小写字母
        - ALPHABETIC-UPPER:大写字母

      - 88 Level

        - 用户定义条件:可以定义布尔条件  自定义条件名
        - 88 [CONDITION-NAME] VALUES [IS,ARE] [LITERAL(字面值)]
        - 基于其他数据项的值 可以给特定的条件值赋予名字  与PIC的数据相关联 在程序中就不必写条件 直接使用此处定义的条件名名即可 该条件不占用空间 作为已知数据项的一种视图标识  用户指定的值
        - 该值可以设定具体的值 也可以设定范围值  :VALUES ARE 0 THRU 100
        - 就比如你需要判断程序中某个值 你可能每次都要写 >0或＜100这样的条件　而可以将这个范围定义为一个条件名　直接拿来用

        ```cobol
        01 STATUS PIC X(2)
              * 当STATUS是A时 这种条件命名为 A-STATUS
        	88 A-STATUS VALUE 'A' 
              * 当STATUS是B时 这种条件命名为 B-STATUS
        	88 B-STATUS VALUE 'B' 
        ```

          

        ```cobol
        IF A-STATUS 
           PERFORM A-PRRGRAM
        ELSE IF B-STATUS
           		PERFORM B-PROGRAM
             END-IF.
        END-IF.
        ```

      - Negate

        - 否定条件
        - NOT

      - Evaluate

        - 评估条件 分支选择 类似Switch 可以选择多个条件 IF-ELSE的替代

        - 此处可以使用88条件语句

        - WHEN OTHER　：类似于default  

        - EVALUATE [CONDITION]

          - WHEN [VALUE1]

            - [COBOL STATEMENTS]

          - WHEN [VALUE2]

            ​     [COBOL STATEMENTS]

          ....

          - WHEN OTHER　

            ​    [COBOL DEFAULT STATEMENTS]

    - 示例程序

      ```cobol
            ******************************************************************
            * Author:
            * Date:
            * Purpose:
            * Tectonics: cobc
            ******************************************************************
             IDENTIFICATION DIVISION.
             PROGRAM-ID. YOUR-PROGRAM-NAME.
             DATA DIVISION.
             FILE SECTION.
             WORKING-STORAGE SECTION.
             01 WS-NUM1 PIC 9(2) VALUE 99.
             01 WS-NUM2 PIC 9(2) VALUE 72.
             01 WS-NUM3 PIC 9(2) VALUE 35.
             01 WS-NUM4 PIC 9(2) VALUE 35.
             01 WS-NUM5 PIC S9(2) VALUE -25.
             01 WS-NAME PIC A(15) VALUE 'abcdef'.
             01 WS-MARKS PIC 9(3).
                 88 PASS VALUES ARE 041 THRU 100.
                 88 FAIL VALUES ARE 000 THRU 040.
             PROCEDURE DIVISION.
             MAIN-PROCEDURE.
                  DISPLAY 'WS-NUM1 :' WS-NUM1.
                  DISPLAY 'WS-NUM2 :' WS-NUM2.
                  DISPLAY 'WS-NUM3 :' WS-NUM3.
                  DISPLAY 'WS-NUM4 :' WS-NUM4.
                  DISPLAY 'WS-NUM5 :' WS-NUM5.
                  
                  IF WS-NUM1 > WS-NUM2 THEN
                      DISPLAY 'WS-NUM1 IS GREATER'
                      IF WS-NUM3 = WS-NUM4 THEN
                         DISPLAY 'WS-NUM3 AND WS-NUM4 ARE EQUAL'
                      END-IF
                  ELSE
                      DISPLAY 'WS-NUM2 IS GREATER'
                  END-IF.
                      
                  IF WS-NUM5 IS NEGATIVE THEN
                      DISPLAY 'WS-NUM5 IS NEGATIVE'
                  END-IF.
                      
                  IF WS-NAME IS ALPHABETIC THEN
                      DISPLAY 'WS-NAME IS  ALPHABETIC'
                  END-IF.    
                  
                  IF WS-NUM1 IS NUMERIC THEN 
                      DISPLAY 'WS-NUM1 IS NUMERIC' 
                  END-IF.
                  
                  MOVE 75 TO WS-MARKS.
                  
                  IF PASS
                      DISPLAY 'WS-MARKS:' WS-MARKS 'PASS'  
                  END-IF.
                      
                  IF NOT FAIL
                      DISPLAY 'WS-MARKS:' WS-MARKS 'NEGATED PASS'  
                  END-IF.
                      
                  EVALUATE   TRUE
                     WHEN WS-NUM4 > 10
                         DISPLAY 'WS-NUM4 VALUE IS' WS-NUM4 'GREATER THAN 10'
                     WHEN WS-NUM4 < 10
                         DISPLAY 'WS-NUM4' WS-NUM4 'LESS THAN 10'
                     WHEN OTHER
                         DISPLAY 'OTHER CONDITION'
                  END-EVALUATE
                  STOP RUN.
             END PROGRAM YOUR-PROGRAM-NAME.
      
      
      ```

      ```cobol
      WS-NUM1 :99
      WS-NUM2 :72
      WS-NUM3 :35
      WS-NUM4 :35
      WS-NUM5 :-25
      WS-NUM1 IS GREATER
      WS-NUM3 AND WS-NUM4 ARE EQUAL
      WS-NUM5 IS NEGATIVE
      WS-NAME IS  ALPHABETIC
      WS-NUM1 IS NUMERIC
      WS-MARKS:075PASS
      WS-MARKS:075NEGATED PASS
      WS-NUM4 VALUE IS35GREATER THAN 10
      ```

      

  ## 循环

  - PERFORM THRU

    - 程序中可以在过程部(PROCEDURE DIVISION) 中定义段落名

      ```cobol
      PROCEDURE DIVISION.
      段落1.
          DISPLAY "This is Paragraph 1".
      段落2.
          DISPLAY "This is Paragraph 2".
      段落3.
          DISPLAY "This is Paragraph 3".
      ```

    - 段落名本质上是给一小段逻辑起了名称 其他地方可以通过PROFORM调用该段落 但是其不接收参数 也不返回值!

    - PERFORM 段落1 THRU 段落3  会按照顺序从段落1执行到段落3  包含两个段落之间的段落也会执行

  - PERFORM UNTIL

    - 重复执行一个段落 直到给定条件为真  类似于 do-while 执行过一次 检查是否继续执行

      ```
      PREFORM [段落名] UNTIL 条件
      	[COBOL语句]
      END PREFORM
      ```

    - 需要重复执行某些段落时  使逻辑更简洁

    - WITH TEST AFTER UNTIL 表示条件检查在执行之后 

  - PERFORM TIMES

    - 重复执行段落 重复次数为给定次数

      ```cobol
      PERFORM 段落名 次数 TIMES
      ```

  - PERFORM VARYING

    - 与PREFORM UNTIL 类似  但是VARYING每次循环时 可以自动修改一个或多个变量的值 可以控制循环次数和条件 类似for循环  提供一种简单的方式控制循环次数和条件

      ```cobol
      PERFORM VARYING 变量1 FROM 初始值1 BY 增量1 UNTIL 条件
          [COBOL 语句]
      END-PERFORM
      
      for(int i = 0; i>10; i++)
      变量1 = i, 初始值1 = 0,增量=i++,条件=i>10      
      ```

  - GO TO

    - 无条件跳转:

      - GO TO 段落名 将当前执行执行流跳转到执行段落名 不再返回当前执行的段落 也不会去执行之间的段落 而是直接继续执行指定段落

    - 有条件跳转:根据变量值选择跳转的段落

      - GO TO  段落1,段落2, DEPENDING ON 变量名1

      - 值是1则执行段落1,值是2则执行段落2

  - 示例程序

    - PERFORM   COBOL语句             END-PERFORM 内联语句  和直接写没太大区别  为了提供一种明确的表达意图 和结构清晰 明确表达代码是为一个逻辑单元执行的
    - PERFORM 段落名 无条件执行指定段落一次 完成后返回当前继续执行

     

    ```cobol
          ******************************************************************
          * Author:
          * Date:
          * Purpose:
          * Tectonics: cobc
          ******************************************************************
           IDENTIFICATION DIVISION.
           PROGRAM-ID. YOUR-PROGRAM-NAME.
           DATA DIVISION.
           FILE SECTION.
           WORKING-STORAGE SECTION.
           01 WS-CNT   PIC 9(1) VALUE 0.
           PROCEDURE DIVISION.
               A000-PARA.
                PERFORM 
                   DISPLAY 'A000 INLINE PERFORM PARA'
                END-PERFORM.
                 
                PERFORM C000-PARA THRU E000-PARA.
                PERFORM B000-PARA.
                PERFORM F000-PARA WITH TEST AFTER UNTIL WS-CNT = 3.
                PERFORM G000-PARA 3 TIMES.
                PERFORM H000-PARA VARYING WS-CNT FROM 1 BY 1 UNTIL WS-CNT 
                = 7.
                STOP RUN.
               B000-PARA.
                   DISPLAY 'B000 PERFORM PARA'.
               C000-PARA.
                   DISPLAY 'C000 PERFORM PARA'.
               D000-PARA.
                   DISPLAY 'D000 PERFORM PARA'.
               E000-PARA.
                   DISPLAY 'E000 PERFORM PARA'.
               F000-PARA.
                   DISPLAY 'F000 PERFORM PARA'.
                   ADD 1 TO WS-CNT.
               G000-PARA.
                   DISPLAY 'G000 PERFORM PARA'.
               H000-PARA.
                   DISPLAY  WS-CNT 'H000 PERFORM PARA'.
           END PROGRAM YOUR-PROGRAM-NAME.
    
    
    ```

    ```cobol
    A000 INLINE PERFORM PARA
    C000 PERFORM PARA
    D000 PERFORM PARA
    E000 PERFORM PARA
    B000 PERFORM PARA
    F000 PERFORM PARA
    F000 PERFORM PARA
    F000 PERFORM PARA
    G000 PERFORM PARA
    G000 PERFORM PARA
    G000 PERFORM PARA
    1H000 PERFORM PARA
    2H000 PERFORM PARA
    3H000 PERFORM PARA
    4H000 PERFORM PARA
    5H000 PERFORM PARA
    6H000 PERFORM PARA
    ```

    

  ## 表

  - 表声明

    - 相同数据项的集合,COBOL中的数组被称为表(tables)

    - 表是线性集合 相同类型数据项的集合

    - 表的数据项内部排序 

    - 表在Data Division中声明

    - OCCURS 子句用于定于表

    - 只能在02~49级别使用

    - 不要再重定义(Redefines)中使用OCCURS

    - TIMES有时候可以省略MOVE

    - 01  table-name

      - 05 sub-item OCCURS N TIMES.
        - 10 ELEMENTS1 PIC X(2)
        - 10 ELEMENTS2 PIC 9(2)

      > table-name是数组名称,sub-item是子项,该子项包含两个元素,ELEMENTS1和ELEMENTS2
      >
      > n代表重复N个子项
      > OCCURS不能出现在01!
      >
      > 

  - One-Dimensional Table 一维表

    - OCCURS子句只出现一次

    - 01 WS-TABLE.

      - 05 WS-A PIC A(10) OCCURS 10 TIME.
      - WS-A的值被定义出现10次 于是该变量存储了10次 组成一个数组
      - WS-A是为出现10次的元素进行了统一命名
      - WS-TABLE是包含表的组项目

    - 另一种定义方式

      ```cobol
      01 WS-A OCCURS 10.
      
      - 05 WS-A-ITEM PIC A(10)
      ```

      

  - Two-Dimensional Table 二维表

    - 一个表项目其下级还可以声明表项目 称为二维表

      - 本质是两个数组进行嵌套,一个数组是另一个数组的元素 

      ```cobol
      01 WS-TABLE
      
      - 05 WS-A OCCURS 10 TIMES
        - 10 WS-B PIC A(10).
        - 10 WS-C OCCURS 5 TIMES.
          - 15 WS-D PIC X(6).
      ```

      

    - 以上是一个表结构 WS-A可以出现1~10次 每次都包含一个WS-B和一整个WS-C表,WS可以出现1~5次,每次都包含一个长度为6的字符

    - 上级表WS-A每出现一次 下级表每次都出现5次

  - 下标(subscript)

    - 用来访问表 是一个固定数字

    - 不需要声明 OCCURS子句会自动处理

    - 使用方式为表名(任意数字 小于出现次数即可) 

      - ```cobol
        01 WS-TABLE
        
        - 05 WS-A OCCURS 10 TIMES
          - 10 WS-B PIC A(10).
          - 10 WS-C OCCURS 5 TIMES.
            - 15 WS-D PIC X(6).
            - 15 WS-E PIC X(6).
        ```

        

      - 一维表访问:WS-A(1) 如果此时输出 会输出WS-A第一次出现的值 如果WS-A下有多个元素 或者子表 也会全部输出字符串

      - 二维表访问:WS-C(1,1) 代表输出WS-A的第一个元素下的 WS-C的第一个元素 会输出WS-A(1)中的WS-C(1)的值 如果WS-C有子元素那么会输出其所有子元素的值

        - 也可以写成WS-C(1 1)中间可以不带逗号

      - 那么如何输出特定下标的子项目值呢  而不是所有元素值 比如我 我想单独输出WS-C(1,1)中 WS-E的值 而不想要WS-D的值

        - 使用特定的项目值加下标进行访问即可 不要使用表名进行访问
          - 一维表:WS-B(1) WS-B是WS-A下一个表元素 可以通过该方式单独访问
          - 二维表:WS-D(1 2) WS-D是WS-A下的WS-C下的表元素 可以通过双重索引访问特定二维表元素

      - JDOOLE平台示例

        ```cobol
        IDENTIFICATION DIVISION.
        PROGRAM-ID. HELLO-WORLD.
        DATA DIVISION.
            WORKING-STORAGE SECTION.
                   01 IX1 PIC 9(2).
                   01 IX2 PIC 9(2).
                   01 WW10 OCCURS 2 TIMES.
                       05 WW10-ITEM PIC X(1).
                       05 WW10-SUB OCCURS 2.
                           10 WW10-SUB-ITEM PIC X(1).
                           10 WW10-SUB-ITEM2 PIC X(1).
        PROCEDURE DIVISION.
                    MOVE'ABCDE' TO WW10(1).
                    MOVE'HIJKN' TO WW10(2).
                    
                    DISPLAY 'WW10(1):'WW10(1)
                    DISPLAY 'WW10(2):'WW10(2)
                    
                    DISPLAY 'WW10-ITEM(1):'WW10-ITEM(1)
                    DISPLAY 'WW10-ITEM(2):'WW10-ITEM(2)
                    
                    DISPLAY 'WW10-SUB(1 1):'WW10-SUB(1 1)
                    DISPLAY 'WW10-SUB(1 2):'WW10-SUB(1 2)
                    
                    DISPLAY 'WW10-SUB(2 1):'WW10-SUB(2 1)
                    DISPLAY 'WW10-SUB(2 2):'WW10-SUB(2 2)
                    
                    DISPLAY 'WW10-SUB-ITEM(1 1):'WW10-SUB-ITEM(1 1)
                    DISPLAY 'WW10-SUB-ITEM(1 2):'WW10-SUB-ITEM(1 2)
                    
                    DISPLAY 'WW10-SUB-ITEM(2 1):'WW10-SUB-ITEM(2 1)
                    DISPLAY 'WW10-SUB-ITEM(2 2):'WW10-SUB-ITEM(2 2)
                    
                    DISPLAY 'WW10-SUB-ITEM2(1 1):'WW10-SUB-ITEM2(1 1)
                    DISPLAY 'WW10-SUB-ITEM2(1 2):'WW10-SUB-ITEM2(1 2)
                    
                    DISPLAY 'WW10-SUB-ITEM2(2 1):'WW10-SUB-ITEM2(2 1)
                    DISPLAY 'WW10-SUB-ITEM2(2 2):'WW10-SUB-ITEM2(2 2)
        STOP RUN.
        
        ```

         

        ```
        WW10(1):ABCDE
        WW10(2):HIJKN
        WW10-ITEM(1):A
        WW10-ITEM(2):H
        WW10-SUB(1 1):BC
        WW10-SUB(1 2):DE
        WW10-SUB(2 1):IJ
        WW10-SUB(2 2):KN
        WW10-SUB-ITEM(1 1):B
        WW10-SUB-ITEM(1 2):D
        WW10-SUB-ITEM(2 1):I
        WW10-SUB-ITEM(2 2):K
        WW10-SUB-ITEM2(1 1):C
        WW10-SUB-ITEM2(1 2):E
        WW10-SUB-ITEM2(2 1):J
        WW10-SUB-ITEM2(2 2):N
        ```

        

    - JDOOLE示例2

      ```cobol
            ******************************************************************
            * Author:
            * Date:
            * Purpose:
            * Tectonics: cobc
            ******************************************************************
             IDENTIFICATION DIVISION.
             PROGRAM-ID. YOUR-PROGRAM-NAME.
             DATA DIVISION.
             FILE SECTION.
             WORKING-STORAGE SECTION.
                 01 IX1 PIC 9(2).
                 01 IX2 PIC 9(2).
                 01 WW10 OCCURS 3.
                     05 WW10-ITEM PIC X(3).
                     05 WW10-SUB OCCURS 3.
                         10 WW10-SUB-ITEM PIC X(1).
             PROCEDURE DIVISION.
             MAIN-PROCEDURE.
                  DISPLAY IX1
                  MOVE '123' TO WW10(1).
                  MOVE '456' TO WW10(2).
                  MOVE '789' TO WW10(3).
      
                  MOVE '5' TO WW10-SUB(2 1).
      
                      
                  PERFORM VARYING IX1 FROM 1 BY 1 UNTIL IX1 > 10
                     DISPLAY WW10-SUB(2 1)
                  END-PERFORM.
                      
                  STOP RUN.
             END PROGRAM YOUR-PROGRAM-NAME.
      
      
      ```

      ```cobol
      00
      5
      5
      5
      5
      5
      5
      5
      5
      5
      5
      ```

      

  - 索引(index)

    - 由于下标是固定值 不会变化 所以有一些循环或者检索无法实现 此时需要用到索引 索引需要在声明时定义

    - 索引是表从开始位置的位移

    - 索引也可以用来访问表元素

    - 可以使用SET 语句变更索引值

      ```cobol
      01 WS-TABLE.
            05 WS-A PIC A(10) OCCURS 10 TIMES INDEXED BY I
      ```

    - 此时I就是一个索引 可以使用一些特定方式来通过索引操作表了 比如Search- - - 

    - 循环 PREFORM VARING

      ```cobol
            ******************************************************************
            * Author:
            * Date:
            * Purpose:
            * Tectonics: cobc
            ******************************************************************
             IDENTIFICATION DIVISION.
             PROGRAM-ID. YOUR-PROGRAM-NAME.
             DATA DIVISION.
             FILE SECTION.
             WORKING-STORAGE SECTION.
                 01 WW10.
                     05 WW10-ITEMS OCCURS 2 TIMES INDEXED BY I.
                         10 WW10-ITEM PIC X(1).
                         10 WW10-SUBS OCCURS 2 TIMES.
                             15 WW10-SUB PIC X(1).
                             15 WW10-SUB2 PIC X(1).
             PROCEDURE DIVISION.
             MAIN-PROCEDURE.
                 MOVE 'ABCDEFGHIJ' TO WW10.
      
                      
                  PERFORM VARYING I FROM 1 BY 1 UNTIL I > 2
                     DISPLAY WW10-ITEMS(I)
                     DISPLAY WW10-ITEM(I)
                     
                     DISPLAY WW10-SUBS(I 1)
                     DISPLAY WW10-SUBS(I 2)
      
                     DISPLAY WW10-SUB(I 1)
                     DISPLAY WW10-SUB(I 2)
      
      
                  END-PERFORM.
                      
                  STOP RUN.
             END PROGRAM YOUR-PROGRAM-NAME.
      
      
      ```

         

      ```cobol
      ABCDE
      A
      BC
      DE
      B
      D
      FGHIJ
      F
      GH
      IJ
      G
      I
      
      ```

      

  - 设值语句(set)

    - 可以更改索引值

    - 可以用来初始化 增加 减少索引值

    - 可以配合Search和Search All来检索表中元素

      ```cobol
      SET I TO 1  //索引设定为1
      SET I TO POSITIVE-NUMBER   //索引设定为正数
      ```

  - 关于给整个Layoutu赋值 必须是类似于结构定义才能赋值 不能直接给表赋值

    ```cobol
    IDENTIFICATION DIVISION.
    PROGRAM-ID. HELLO-WORLD.
    DATA DIVISION.
        WORKING-STORAGE SECTION.
               01 IX1 PIC 9(2).
               01 IX2 PIC 9(2).
               01 WW10.
                   05 WW10-FIRST OCCURS 2 TIMES.
                       10 WW10-ITEM PIC X(1).
                       10 WW10-SUB OCCURS 2.
                            13 WW10-SUB-ITEM PIC X(1).
                            13 WW10-SUB-ITEM2 PIC X(1).
    PROCEDURE DIVISION.
                MOVE'ABCDEHIJKL' TO WW10.
                DISPLAY WW10-SUB-ITEM(2,2)
    STOP RUN.
    
    ```

    - 如果是以下形式 就没办法给整个Layout赋值了 最外层必须是结构定义语句

      ```cobol
                 01 WW10 OCCURS 3.
                     05 WW10-ITEM PIC X(3).
                     05 WW10-SUB OCCURS 3.
                         10 WW10-SUB-ITEM PIC X(1).
                  
                 MOVE'ABCDEHIJKL' TO WW10. //会报错
      ```

    - DEMO3

      ```cobol
      IDENTIFICATION DIVISION.
      PROGRAM-ID. HELLO-WORLD.
      DATA DIVISION.
          WORKING-STORAGE SECTION.
                 01 WS-ONED.
                     05 WS-CHAR  PIC X(2) OCCURS 5 TIMES.
                 01 WS-TWOD.
                     05 WS-FIRST OCCURS 3 TIMES.
                          10 WS-A PIC A(1).
                          10 WS-SECOND OCCURS 2 TIMES.
                              15 WS-B PIC X.
      PROCEDURE DIVISION.
                  MOVE 'AABBCCDDEE' TO WS-ONED.
                  DISPLAY 'ONE DIMENSINAL TABLE'.
                  DISPLAY 'ONE IN WS-CHAR TABLE:' WS-CHAR(1).
                  DISPLAY 'TWO IN WS-CHAR TABLE:' WS-CHAR(2).
                  DISPLAY 'THREE IN WS-CHAR TABLE:' WS-CHAR(3).
                  DISPLAY 'FOUR IN WS-CHAR TABLE:' WS-CHAR(4).
                  DISPLAY 'FIVE IN WS-CHAR TABLE:' WS-CHAR(5).
                  
                  MOVE 'A12B34C56' TO WS-TWOD.
                  DISPLAY 'TWO DIMENSINAL TABLE'.
                  DISPLAY 'ONE IN WS-FIRST TABLE:' WS-FIRST(1).
                  DISPLAY '(1 1):' WS-SECOND(1 1).
                  DISPLAY '(1 2):' WS-SECOND(1 2).
                  
                  DISPLAY 'SECOND IN WS-FIRST TABLE:' WS-FIRST(2).
                  DISPLAY '(2 1):' WS-SECOND(2 1).
                  DISPLAY '(2 2):' WS-SECOND(2 2).
                  
                  DISPLAY 'THREE IN WS-FIRST TABLE:' WS-FIRST(3).
                  DISPLAY '(3 1):' WS-SECOND(3 1).
                  DISPLAY '(3 2):' WS-SECOND(3 2).
      STOP RUN.
      
      ```

      

  - 搜索语句(Search,Search All)

    ```cobol
    01 WS-TABLE.
          05 WS-A PIC A(10) OCCURS 10 TIMES INDEXED BY I
    ```

    

    - Search:线性搜索访问 可以搜素表内元素 从表开始逐一搜素 也是为什么其需要索引才能使用 表可以是排序的 也可以是无序的

      ```cobol
      SEARCH 表名
         AT END 
         //搜索结束未找到时 执行的逻辑
         WHEN 搜索条件
         //搜索到执行的逻辑
         END-SEARCH
      ```

      - 从索引的初始值开始,如果未找到搜索元素,索引会自动加1,会一直持续到表末尾,如果搜索到元素,会结束搜索,退出循环

        ```cobol
              ******************************************************************
              * Author:
              * Date:
              * Purpose:
              * Tectonics: cobc
              ******************************************************************
               IDENTIFICATION DIVISION.
               PROGRAM-ID. YOUR-PROGRAM-NAME1.
               DATA DIVISION.
               FILE SECTION.
               WORKING-STORAGE SECTION.
               01 WS-TWOD.
                   05 WS-FIRST OCCURS 3 TIMES INDEXED BY I.
                       10 WS-A PIC A(1).
                       10 WS-SECOND OCCURS 2 TIMES INDEXED BY J.
                           15 WS-B PIC X.
               01 WS-SRCH PIC X VALUE 'C'.
               PROCEDURE DIVISION.
               MAIN-PROCEDURE.
                    MOVE 'A12B34C56' TO WS-TWOD.
                    PERFORM A000-PARA VARYING I FROM 1 BY 1 UNTIL I > 3.
                    SET I J TO 1.
                    PERFORM C000-SEARCH-PARA.
                    STOP RUN.
               A000-PARA.
                    DISPLAY WS-FIRST(I).
                    PERFORM B000-PARA  VARYING J FROM 1 BY 1 UNTIL J > 2.
               B000-PARA.
                    DISPLAY WS-SECOND(I,J).
               C000-SEARCH-PARA.
                   SEARCH WS-FIRST
                       AT END DISPLAY 'NOT FOUND IN TABLE '
                       WHEN WS-A(I) = WS-SRCH
                       DISPLAY 'FOUNDED'
                   END-SEARCH.  
               END PROGRAM YOUR-PROGRAM-NAME1.
        
        
        ```

        ```cobol
        A12
        1
        2
        B34
        3
        4
        C56
        5
        6
        FOUNDED
        ```

        

    - Search All:搜索全部 二分查找 搜索表中元素 所以表必须是排序的

  ###　String Handling

- 概念

  - 与字符串相关的操作，包括计算字符个数，替换字符串，连接字符串，拆散字符串

- INSPECT　字符串处理语句

  - 统计,替换,统计字符串

  - 从左到右执行

  - INSPECT REPLACING:替换字符串

    - INSPECT input-string REPLACING ALL char1 BY char2.

    ​	

    ```COBOL
    INSPECT WS-STRING REPLACING ALL 'A' BY 'X'.
    ```

    - WS-STRING　操作目标字符　　REPLACING 　将前一个字符　全部替换为后一个字符
    - WS-STRING为输入字符串　WS-CNTA为输出　会将计数结果

  - INSPECT TALLYINBG:计算字符串个数

    - INSPECT input-string TALLYING output-count FOR ALL CHARACTERS

    ```cobol
    INSPECT WS-STRING TALLYING WS-CNTA FOR ALL 'A'.
    ```

    - WS-STRING为输入字符串　WS-CNTA为把保存结果项目　会将计数结果放到WS-CNTA
    - FOR ALL　后面为计数字符　统计＇A＇字符的数量

  - DEMO

    ```cobol
          ******************************************************************
          * Author:
          * Date:
          * Purpose:
          * Tectonics: cobc
          ******************************************************************
           IDENTIFICATION DIVISION.
           PROGRAM-ID. YOUR-PROGRAM-NAME.
           DATA DIVISION.
           FILE SECTION.
           WORKING-STORAGE SECTION.
           01 WS-STRING PIC A(15).
           01 WS-CNTA PIC 99.
           01 WS-CNTS PIC 99.
           PROCEDURE DIVISION.
               MOVE 'ABCDEASSDAERAAA' TO WS-STRING.
               INITIALIZE WS-CNTA.
               INSPECT WS-STRING TALLYING WS-CNTA FOR ALL 'A'.
               DISPLAY 'COUNT OF A IN STRING :' WS-CNTA.
               
               INSPECT WS-STRING REPLACING ALL 'A' BY 'X'.
               
               INITIALISE WS-CNTA.
               INSPECT WS-STRING TALLYING WS-CNTA FOR ALL 'A'.
               DISPLAY 'WS-STRING:' WS-STRING.
               DISPLAY 'COUNT OF A IN STRIN:' WS-CNTA.
               
               STOP RUN.
           MAIN-PROCEDURE.
                DISPLAY "Hello world"
                STOP RUN.
           END PROGRAM YOUR-PROGRAM-NAME.
    
    
    ```

    

- STRING

  - 字符串连接

  - STRING ws-string1 DELIMITED BY SPACE

    ws-string2 DELIMITED BY SIZE

    INTO WS-STRING

  - 可以拓展同时计算连接后的字符串长度INTO ws-string

  - 也可以显示溢出时显示消息 没有溢出时显示消息

    ```cobol
               STRING WS-STR1 DELIMITED BY SIZE
                      WS-STR2 DELIMITED BY SIZE
                      WS-STR3 DELIMITED BY SPACE
                      INTO WS-STRING
               END-STRING.
    ```

  - DELIMITED BY即分隔符 当将WS-STR1放入到WS-STRING的过程中 如果遇到分隔符停止放入,开始操作下一个字符串(不会吧分隔符放入),BY SIZE即将该字符所有字符放入

  - 连接之后的字符串会放在WS-STRING里面

- UNSTRING

  - 拆解字符串

  - UNSTRING ws-string DELIMITED BY SPACE

    INTO ws-str1,ws-str2

    ```cobol
               UNSTRING WS-STRING DELIMITED BY SPACE 
                   INTO WS-USTR1, WS-USTR2,WS-USTR3
               END-UNSTRING.
    ```

  - DELIMITED BY 分隔符 在操作时如果遇到指定分隔符 那么就停止放入当前字符串 继续放入下一个字符(不会把分隔符放入目标字符串)

- DEMO2

  ```cobol
        ******************************************************************
        * Author:
        * Date:
        * Purpose:
        * Tectonics: cobc
        ******************************************************************
         IDENTIFICATION DIVISION.
         PROGRAM-ID. YOUR-PROGRAM-NAME.
         DATA DIVISION.
         FILE SECTION.
         WORKING-STORAGE SECTION.
         01 WS-STRING PIC A(15).
         01 WS-CNTA PIC 99.
         01 WS-CNTS PIC 99.
         
         01 WS-STRING2 PIC A(40) VALUE SPACES.
         01 WS-STR1 PIC A(8) VALUE 'WELCOME '.
         01 WS-STR2 PIC A(3) VALUE 'TO '.
         01 WS-STR3 PIC A(16) VALUE 'TUTORIALSPOINT'.
         01 WS-USTR1 PIC A(8) VALUE SPACES.
         01 WS-USTR2 PIC A(8) VALUE SPACES.
         01 WS-USTR3 PIC A(8) VALUE SPACES.
  
         PROCEDURE DIVISION.
             MOVE 'ABCDEASSDAERAAA' TO WS-STRING.
             INITIALIZE WS-CNTA.
             INSPECT WS-STRING TALLYING WS-CNTA FOR ALL 'A'.
             DISPLAY 'COUNT OF A IN STRING :' WS-CNTA.
             
             INSPECT WS-STRING REPLACING ALL 'A' BY 'X'.
             
             INITIALISE WS-CNTA.
             INSPECT WS-STRING TALLYING WS-CNTA FOR ALL 'A'.
             DISPLAY 'WS-STRING:' WS-STRING.
             DISPLAY 'COUNT OF A IN STRIN:' WS-CNTA.
        * STRING, UNSTRING   
             DISPLAY 'STRING 1:' WS-STR1.
             DISPLAY 'STRING 2:' WS-STR2.
             DISPLAY 'STRING 3:' WS-STR3.
             STRING WS-STR1 DELIMITED BY SIZE
                    WS-STR2 DELIMITED BY SIZE
                    WS-STR3 DELIMITED BY SPACE
                    INTO WS-STRING
             END-STRING.
                 
             DISPLAY 'WS-STRING:' WS-STRING.
        *    GO TO A000-PARA.
             
             UNSTRING WS-STRING DELIMITED BY SPACE 
                 INTO WS-USTR1, WS-USTR2,WS-USTR3
             END-UNSTRING.
             
             DISPLAY 'UNSTRING 1 :' WS-USTR1.
             DISPLAY 'UNSTRING 2 :' WS-USTR2.
             DISPLAY 'UNSTRING 3 :' WS-USTR3.
  
             STOP RUN.
         MAIN-PROCEDURE.
              DISPLAY "Hello world"
              STOP RUN.
         END PROGRAM YOUR-PROGRAM-NAME.
  
  ```

  

- GO TO

  - GO TO语句用于把当前执行流跳转到指定地 中途的代码会跳过!

    ```cobol
               GO TO A000-PARA.
               
               UNSTRING WS-STRING DELIMITED BY SPACE 
                   INTO WS-USTR1, WS-USTR2,WS-USTR3
               END-UNSTRING.
               
               DISPLAY 'UNSTRING 1 :' WS-USTR1.
               DISPLAY 'UNSTRING 2 :' WS-USTR2.
               DISPLAY 'UNSTRING 3 :' WS-USTR3.
    
               STOP RUN.
           A000-PARA.
                DISPLAY "Hello world"
                STOP RUN.
    ```

  - 当执行到GO TO 会直接跳转到A000-PARA(标签名 用来标记一个段)继续执行 不会执行中间代码

  - 在 COBOL 中，GOTO 语句通常被认为是一种不良的编程风格，因为它可能会使程序逻辑难以理解和维护。更好的做法是使用 PERFORM 语句或其他结构化的控制语句来实现相同的逻辑。

  - 控制会永久转移到指定位置

  - 流程控制 

    - PROCEDURE DIVISION中可以定义多个标签

      - 如果所有标签都没有流程控制语句 没有结束语句 那么会按照标签顺序以此执行

        ```cobol
               PROCEDURE DIVISION.
               MAIN-PROCEDURE.
                    DISPLAY "HELLO WORLD1"
                    EXIT.
                        
               SUB-PROCEDURE.
                    DISPLAY "HELLO WORLD2"
                    EXIT.
                    END PROGRAM YOUR-PROGRAM-NAME.
        ```

      - 执行完MAIN-PROCEDURE 就会执行SUB-PROCEDURE 注意要用EXIT. 表示程序段结束符 不要用STOP RUN 会将整个程序结束


  ### File Handing

- 文件(File)

  - Cobol中文件是记录的集合 有点类似于关系型数据的概念

- 文件组织(File Organization)

  - 顺序文件(Sequential File Organization)
    - 按照记录的插入顺序 存储记录 后插入的记录在后
    - 类似于普通文件
  - 索引顺序文件(Indexed Sequential File Organiztion)
    - 在顺序文件的基础上,提供了索引 ,用来定位特定记录
    - 类似于数组

  - 相对文件组织(Relative File Organization)
    - 记录存储时分配编号 编号决定存储文字 可以通过编号访问特定记录
    - 类似与Hashmap

- 文件访问模式(File Acess)

  - Sequential Acess(顺序访问)
    - 顺序访问时 数据必须被连续的读取和写入 不能跳到特定位置 必须按照顺序来依次访问
    - 仅仅适用PS文件  无法随机选择记录 无法查询 
  - Random Acess(随机访问)
    - 容许跳到文件中的任意记录进行读写操作 不需要逐个访问之前的位置
    - VSAM文件
  - Dynamic Acess(动态访问)
    - 根据场景 可以切换 顺序访问和随机访问
    - 你需要读取10条记录,但是从第50条开始,你可以先切到随机访问跳到50条,然后切换成顺序访问开始访问10条

- 文件处理动词(File Handling Verbs)

  - OPEN 打开文件
    - OPEN INPUTD 以输入模式打开文件  读取文件
    - OPEN OUTPUT 以输出模式打开文件 写入文件
    - OPEN EXTEND 以拓展模式打开文件 附加写入文件 OUTPUT会删除原记录从头开始 而EXTENDS会从末尾附加
    - OPNE I-O 输入输出模式  用于读取和重写
  - READ 读取文件
    - READ 文件名 INTO 变量名 读取的记录会自动放入当前变量
    - 如果不是循环读取的话 只会读取文件的第一条记录
    - AT END MOVE  读取之后 读取完毕文件时做什么
    - NOT AT END 读取之后 没有读取完时的动作
  - WRITE 写入
  - REWRITR 更新
  - DELETE  删除
  - START 开始浏览
  - CLOSE 关闭文件

- 读取文件DEMO1  OpenCboolIDE无法执行 在线网站执行的 读取文件名不加后缀!

  - https://replit.com/

  - ```cobol
    000100 IDENTIFICATION DIVISION.
    000200 PROGRAM-ID. HELLO-WORLD.
           ENVIRONMENT DIVISION.
            INPUT-OUTPUT SECTION.
            FILE-CONTROL.
               SELECT INFILE ASSIGN TO DDINPUT
               ORGANIZATION IS SEQUENTIAL.
           DATA DIVISION.
            FILE SECTION.
                FD INFILE.
                01 NAME PIC A(80).
            WORKING-STORAGE SECTION.
                01 WS-NAME PIC A(80).
                01 WS-EOF PIC A VALUE SPACE.
    000300
    000400 PROCEDURE DIVISION.
             OPEN INPUT INFILE.
              PERFORM UNTIL WS-EOF ='Y'
                 READ INFILE INTO WS-NAME
                     AT END MOVE 'Y' TO WS-EOF
                     NOT AT END DISPLAY WS-NAME
                 END-READ
              END-PERFORM.
    000600 STOP RUN.
    
    ```

- 读取更新文件DEMO

  - 更新文件 文件不用创建 自动生成!

  ```cobol
  000100 IDENTIFICATION DIVISION.
  000200 PROGRAM-ID. HELLO-WORLD.
         ENVIRONMENT DIVISION.
          INPUT-OUTPUT SECTION.
          FILE-CONTROL.
             SELECT INFILE ASSIGN TO DDINPUT
             ORGANIZATION IS SEQUENTIAL.
             SELECT OUTFILE ASSIGN TO DDOUTPUT
             ORGANIZATION IS SEQUENTIAL.
         DATA DIVISION.
          FILE SECTION.
              FD INFILE.
              01 FS-RECORD PIC A(80).
              FD OUTFILE.
              01 FS-OUTRCD PIC A(80).
          WORKING-STORAGE SECTION.
              01 WS-RECORD PIC A(80).
              01 WS-EOF PIC A VALUE SPACE.
  000400 PROCEDURE DIVISION.
           OPEN INPUT INFILE.
           OPEN OUTPUT OUTFILE.
            PERFORM UNTIL WS-EOF ='Y'
               READ INFILE INTO WS-RECORD
                   AT END MOVE 'Y' TO WS-EOF
                   NOT AT END PERFORM A000-WRITE-PARA
               END-READ
            END-PERFORM.
            CLOSE INFILE.
  000600    STOP RUN.
            A000-WRITE-PARA.
            MOVE WS-RECORD TO FS-OUTRCD.
            WRITE FS-OUTRCD
            END-WRITE.
  
  ```

- FILE STATUS 文件状态

  - 文件操作后的状态信息 比如读取状态 写入 打开 或者关闭 是否成功

    - 00 : 操作成功完成
  - 01 : 在写入操作中,写入重复的键值和索引
    
    - 30: 请求的记录不存在
  - 其他值:代表不同的错误或者异常
    
  - 有点类似于SQL成功后的返回值....

  - 在FILE-CONTROL定义文件关联时追加STATUS即可显示

    ```cobol
               SELECT INFILE ASSIGN TO DDINPUT
               ORGANIZATION IS SEQUENTIAL
               FILE STATUS IS WS-STATUS.
    ```

  - 当更改FD定义的记录里面的变量忠厚 使用WRITE或者REWRITE即可更新

    ```cobol
            FILE SECTION.
                FD INFILE.
                  01 FS-RECORD.
                    05 FS-KEY PIC X(5).
                    05 FILLER PIC X.
                    05 FS-DISC PIC X(20).
    ```

    ```cobol
                MOVE 'WE ARE UPDATING THIS RECORD' TO FS-DISC
                REWRITE FS-RECORD
                END-REWRITE
    ```

- REWRITE和STATUS DEMO

  ```cobol
  000100 IDENTIFICATION DIVISION.
  000200 PROGRAM-ID. HELLO-WORLD.
         ENVIRONMENT DIVISION.
          INPUT-OUTPUT SECTION.
          FILE-CONTROL.
             SELECT INFILE ASSIGN TO DDINPUT
             ORGANIZATION IS SEQUENTIAL
             FILE STATUS IS WS-STATUS.
         DATA DIVISION.
          FILE SECTION.
              FD INFILE.
                01 FS-RECORD.
                  05 FS-KEY PIC X(5).
                  05 FILLER PIC X.
                  05 FS-DISC PIC X(20).
          WORKING-STORAGE SECTION.
            01 WS-RECORD.
              05 WS-KEY PIC X(5).
              05 FILLER PIC X.
              05 WS-DISC PIC X(20).
            01 WS-EOF PIC X VALUE SPACE.
            01 WS-STATUS PIC 99.
  000400 PROCEDURE DIVISION.
           OPEN I-O INFILE.
            PERFORM UNTIL WS-EOF ='Y'
               READ INFILE INTO WS-RECORD
                   AT END MOVE 'Y' TO WS-EOF
                   NOT AT END PERFORM A000-REWRITE-PARA
               END-READ
            END-PERFORM.
            CLOSE INFILE.
  000600    STOP RUN.
         A000-REWRITE-PARA.
            DISPLAY 'WS-KEY:' WS-KEY.
            IF WS-KEY = '10005'
              DISPLAY 'WS-RECORD 'WS-RECORD
              DISPLAY 'WS-STATUS' WS-STATUS
              MOVE 'WE ARE UPDATING THIS RECORD' TO FS-DISC
              DISPLAY 'FS-DISC:' FS-DISC
              REWRITE FS-RECORD
              END-REWRITE
            END-IF.
  
  ```

   

  ```cobol
  10008                     10009                     10005                     
  ```

    

  ```cobol
  WS-KEY:10008
  WS-KEY:10009
  WS-KEY:10005
  WS-RECORD 10005 WE ARE UPDATING THIS
  WS-STATUS00
  FS-DISC:WE ARE UPDATING THIS
  WS-KEY:
  0005
  ```

  ### Subroutines(子程序)

  - Call Verb(调用动词)

    - CALL动词将控制成一个程序转移到另一个程序
    - 适用CALL动词的是调用程序,被调的程序称为被调用程序
    - 调用后调用程序将停止执行,知道被调用程序执行完毕
    - EXIT PROGRAM 语句用户将控制从被调用程序转移回调用程序

  - Call By Reference (引用调用)

    - 调用时传递参数,如果是引用调用,被调用程序修改的参数,那么该值也会反映到调用程序

    - CALL语法默认为引用调用

      ```cobol
      CALL SUB-PROG-NAME USING param1,param2
      ```

    - DEMO1 在线环境无法执行 需要在OpenCobolIDE里面执行 子程序不要写STOP RUN.

      ```COBOL
            ******************************************************************
            * Author:
            * Date:
            * Purpose:
            * Tectonics: cobc
            ******************************************************************
             IDENTIFICATION DIVISION.
             PROGRAM-ID. PGM1.
             DATA DIVISION.
             FILE SECTION.
             WORKING-STORAGE SECTION.
                01 WS-NUM1 PIC 9(2) VALUE 99.
                01 WS-NUM2 PIC 9(2) VALUE 72.
                01 WS-ADD PIC 9(3).
                01 WS-PGM PIC X(8).
             PROCEDURE DIVISION.
               DISPLAY 'IN CALLLING MODULE'.
               DISPLAY 'WS-NUM1:' WS-NUM1.
               DISPLAY 'WS-NUM2:' WS-NUM2.
               ADD WS-NUM1 TO WS-NUM2 GIVING WS-ADD.
               DISPLAY 'WS-ADD: ' WS-ADD.
               MOVE 'PGM2' TO WS-PGM.
               CALL WS-PGM USING WS-NUM1,WS-NUM2.
            *  CALL WS-PGM USING BY CONTENT WS-NUM1,WS-NUM2.
               DISPLAY 'IN CALLLING MODULE'.
               ADD WS-NUM1 TO WS-NUM2 GIVING WS-ADD.
               DISPLAY 'WS-NUM1:' WS-NUM1.
               DISPLAY 'WS-NUM2:' WS-NUM2.
               DISPLAY 'WS-ADD:' WS-ADD.
                  STOP RUN.
             END PROGRAM PGM1.
      ```

      

      - 可以看到输出结果 子程序中变更了两个参数 也导致主程序中的值被变更了

      ```cobol
      IN CALLLING MODULE
      WS-NUM1:99
      WS-NUM2:72
      WS-ADD: 171
      IN CALLLED MODULE
      LS-NUM1:79
      LS-NUM2:68
      IN CALLLING MODULE
      WS-NUM1:79
      WS-NUM2:68
      WS-NUM3:147
      ```

      

  - Call By Content(内容调用)

    - 内容调用  被调用程序变更值 对调用程序不可见

    - 需要加BY CONTENT关键词

      ```cobol
      CALL sub-prog-name USING 
      BY CONTENT param1,BY CONTENT param2
      ```

    - 将上面的引用调用改为按内容调用

      ```cobol
            *   CALL WS-PGM USING WS-NUM1,WS-NUM2.
               CALL WS-PGM USING BY CONTENT WS-NUM1,WS-NUM2.
      ```

      ```cobol
      IN CALLLING MODULE
      WS-NUM1:99
      WS-NUM2:72
      WS-ADD: 171
      IN CALLLED MODULE
      LS-NUM1:79
      LS-NUM2:68
      IN CALLLING MODULE
      WS-NUM1:99
      WS-NUM2:72
      WS-ADD:171
      ```

  - Static Call(静态调用)

    - 在编译时就已经确定要调用的子程序 适用子程序名为固定值 需要在编译时设定选项 NODYNAM

      ```
      CALL 子程序名
      ```

        <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202404061937400.png" alt="image-20240406193716813" style="zoom:50%;" />

  - Dynamic Call(动态调用)

    - 在编译时不确定,在程序运行时才确定,调用子程序名为变量,可以在代码里更改变量值 从而调用不同的子程序 需要在编译时设定选项 DYNAM

      ```cobol
      01 SUB-NAME PIC X(10).
      
      
      
      IF CONDITION
      	MOVE 'XXXXX' TO SUB-NAME
      ELSE
      	MOVE 'BBBBB' T
      	
      CALL SUB-NAME
      ```

      

  ### Table Detail

- 定义

  - 01 table-name.

    - 05 sub-item OCCURS n times PIC X(10)

    > 以上代表该表有N个子项,每个子项,每个子项都是X类型,10长度

- 多维度表(嵌套)

  ```cobol
  01 table-name 
   05 sub-itemOCCURS 10 TIMES.
    - 10 ELEMENTS1 PIC X
    - 10 ELEMENTS2 OCCURS 8 TIMES
      - 15 ELEMENTS2-sub PIC X
  ```

  

- 引用表中数据

  - 下标:数据名称和其对应的出现次数(第几位出现).称为下标,最小下标为1,定义了表元素的第一次出现,如果使用的是变量名作为下标,必须是基本数字类型

    - 各数据在表中的编号,存储位置即下标

  - 定义:

    ```cobol
    01 table-name.
          05 table-element OCCURS 3 TIMES PIC X(03)
          	 MOVE "DEF" TO TABLE-ELEMENT(2)
    ```

    >  以上,便是将"DEF"赋给了下标为2的子项元素

  - 索引:通过为数据项出去创建索引,这个索引会被加入表的地址以定义其中的项

    - 通过索引来管理表
    - 提高更高效的查找代码
    - 要使用Search语句 表必须为索引表
    
  ```cobol
    05 sub-item OCCURS 10 TIMES INDEXED BY INX-A PIC X(05)
  ```
  
  > INX-A即为索引变量,索引存储的是数据偏移量,并不是数据实际存储位置
    >
    > 简单来说,一个数据的偏移量,就是一个数据和第一条数据的偏移位置量,存储单元的长度与数据长度有关
    >
    > 如果数据长度为5,那么第一个元素的索引为0,第二个索引的元素就为5,第三个就为10,以此为单位进行偏移
    >
    > 使用 INDEXD BY即可定义索引,索引值的计算(出现次数-1)*table.length
    >
    > 也可以使用USAGE IS INDEX单独定义索引
  
  ```
    //使用索引
    set  2 TO INX-A
    MOVE sub-item(INX-A) TO RESULT-DATA
  ```
  
  > 以上将2赋给了索引, 引用第二条数据,其实索引存储的不是2,而是第二条数据的偏移量,实际上存储的是5,计算方式为(n-1)*length,当然2和其对应的偏移量是系统自身转换的

- 表初始化

  - 读取文件,数据库动态加载
  - 硬编码 VALUES
  - INITIALIZE

- 表数据检索

  - Search
  - Birnary Search 二分查找

- 数据类型

  - 数值类型
    - 浮点型
      - V表示小数点位置 并不会存储小数点
    - 整数型
  - 符号类型:S
    - 正负数表达
      - S代表该数值是有符号的,主要用来保存正负数,代表+ -号
      - 若某一个数值不定义符号类型,那么只能存储正数,任何负数,都会转为正数存储
  - 分隔符:,用来分隔多位数字-
    - ** 平方: 2**8 2的8次方
  - 日期格式:通常使用/来分割
  - 流程控制语句:IF ELSE
  - Switch:EVALUATE WHEN
  - 循环:PERFORM UNTIL
    - 表循环语句 PERFORM VARYING UNTIL
  - 排序方法:SORT
  - 下标与索引的区别:下标就是一个普通的变量,而索引就是系统内部维护的变量
  - 定义下标变量可以使用 USAGE IS COMP来提高效率
    - 简写 COMP 以二进制存储数据
    - 计算不懂十进制,也不会数数字,所以都是以二进制存储数据,如果我们定义数据时以二进制定义数据,这样运算速度更快
    - comp:单精度浮点数(float)  纯粹用二进制存储数据
    - comp2:双精度浮点数(double) 纯粹用二进制存储数据 范围更大
    - comp3: 以BCD码表达0-9的数字,以二进制编码十进制代码,四位二进制数表达0-9这十个数,使得二进制和十进制可以快速转换
      - https://juejin.cn/post/7103883401622798350
    - comp4:表示整数
    - comp5:表示整数,但可以指定小数点
  - set语句可以操作索隐变量进行赋值和运算
    - set 索引 TO  数字 代表将索引变量变为后面的数字 
    - set 变量 TO 索引 代表将该变量赋给索引
    - 将索引改为索引往后偏移2位
      - set 索引 UP BY 2 //将会指向便宜2位后的数据
    - 往前偏移2位 偏移数值也可以为变量
      - set 索引 down by 2
  - Search:顺序查找
  - SearchAll:二分查找
  - 使用DESC.....和ASCE进行表元素排序

- 变长表和定长表

  - 变长表定义:OCCURS  后面加上DEPENDING ON

    - 此时OCCURS的后面不再是具体数字, 而是范围数字

      ```
      01 表名
      	05 子项 OCCURS 1 TO 9 TIMES
      					DEEPENDING ON 实际长度(可以是变量)
      ```

      

- 嵌套表:二维表格: 还是以最小元素为基础单位,以上都只是包含多少个基础单位

  ```
  01 表名
  	05 sub OCCURS 2 TIMES
  		10 sub-sub OCCURS 3 TIMES
  			15 table-item1 PIC X
  			15 table-item2 PIC X
  ```

  <img src="C:%5CUsers%5CPhelop%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20230529234333089.png" alt="image-20230529234333089" style="zoom:67%;" />

- 多层嵌套:

  ```
  01 NESTED-TABLE-3.
  	05 TABLE-DEPTH OCCURS 2 TIMES.
          10 TABLE-ROW-3 OCCURS 2 TIMES.
  			15 TABLE-COLUMN-3 OCCURS 3 TIMES.
  				20 TABLE-ITEM3-1 PIC X(1).
  				20 TABLE-ITEM3-2 PIC X(2).
  ```

  ![image-20230529234633418](https://raw.githubusercontent.com/1v10/Photo/main/photo/202305292346494.png)

  > 每个TABLE-DEPTH子项包含12个table-item3

- 嵌套表的具体访问方式

  ```
  01 NESTED-TABLE-2.
  	05 TABLE-ROW OCCURS 2 TIMES.
  		10 TABLE-COLUMN OCCURS 3 TIMES.
  			15 TABLE-ITEM PIC X.
  ```

  > 引用表中的具体数据, 方式如下,TABLE-ITEM(x1,x2) 或者TABLE-ITEM(x1 x2) 这两个下标分别对应TABLE-ROW和TABLE-COLUMN,X1的取值范围为1-2,x2的取值范围为1-3

  ```
  01 NESTED-TABLE-3.
  	05 TABLE-DEPTH OCCURS 2 TIMES.
  		10 TABLE-ROW-3 OCCURS 2 TIMES.
  			15 TABLE-COLUMN-3 OCCURS 3 TIMES.
  				20 TABLE-ITEM-3 PIC X.
  ```

  > TABLE-ITEM-3(X1,X2,X3),x1对应TALBE-DEPTH ,X2对应TABLE-ROW-3,XE对应TALBE-COLUMN-3
  >
  > 嵌套表嵌套几层,访问时就有几个下标,第一个下标对应表中的第一个嵌套,第n个下标对应表中的第N层嵌套

- 嵌套索引表

  - 每层嵌套都是一个索引表,有多个嵌套就有多少个索引

    ```
    01 NESTED-INDEX-TABLE.
    	05 TABLE-DEPTH OCCURS 2 TIMES
    			INDEXED BY NDX-A.
    					10 TABLE-ROW OCCURS 4 TIMES
    								NDEXED BY NDX-B.
    										15 TABLE-COLUMN OCCURS 5 TIMES
    														INDEXED BY NDX-C
    														PIC X (10).
    ```

    >  访问方式:TABLE-COLIMN(2,3,1)
    >
    >  2对应 NDX-A   第三层嵌套索引		实际偏移量:n-1 X 上一层长度 X 数量
    >
    >  3对应NDX-B 	第二层嵌套索引		实际偏移量 :n-1 X 上一层长度 X 数量
    >
    >  1对应NDX-C 	第一层嵌套索引		实际偏移量: n-1*10	

- 内部函数

  - Function开头即调用内部函数
  - Function 函数名(参数)

- 子程序调用

  - CALL 目标程序引用(可以是变量也可以是固定值)
  - using 指定调用子程序传递的参数(默认按照引用传递:即修改对调用者可见)
    - BY CONTENT可以指定传递变量的副本,此时修改对调用者不可见
      - BY VALUE 与BY CONTINUE作用相同  但是传递类型只能是基本数据类型
  - RETURNING 指定返回值, 可选项

- 拷贝库

  - 类似于调用子程序 将复用性代码放入拷贝库可以重复调用
  - COPY关键词 将当前代码编译时加入所COPY的代码

- OpenCobolIDE编译截图

  - ![image-20231231214901574](https://raw.githubusercontent.com/1v10/Photo/main/photo/202312312149666.png)