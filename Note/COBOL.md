## COBOL

- CoBol的执行:在线执行网站:[cobol代码在线运行 (lddgo.net)](https://www.lddgo.net/code/runcode/cobol)

  - [在线工具大全 (lddgo.net)](https://www.lddgo.net/) 
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

- 四个部

  - 标识部:程序标识
  - 环境部:程序环境配置
  - 数据部:程序变量,文件声明
    - 文件节
    - 工作存储节
  - 过程部:操作指令
    - 是程序完成工作的地方,statements便在此处,

- JCL:负责与z/OS交互,包括让编译代码, 让z/OS执行

- zome CLI:如果npm安装后 --version报错,再安装一个安全模块即可

  ```java
  zowe plugins install @zowe/secure-credential-store-for-zowe-cli
  ```

- 变量/数据项

  - 9:Numberic(0-9)
  - A:Alphabetic(A-Z,a-z或者空格)
  - X:任意字符

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

  - ## 表

    - 相同数据项的集合,从属性而言被称为表元素,标识COBOL中的数组

    - 定义

      - 01  table-name

        - 05 sub-item OCCURS N TIMES.
          - 10 ELEMENTS1 PIC X(2)
          - 10 ELEMENTS2 PIC 9(2)

        > table-name是数组名称,sub-item是子项,该子项包含两个元素,ELEMENTS1和ELEMENTS2
        >
        > n代表重复N个子项
        > OCCURS不能出现在01!

    - 单元素定义

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
        - 索引不能赋值,不能运算

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