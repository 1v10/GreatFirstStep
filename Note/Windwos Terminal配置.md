#### 优点

- 简单美观
- 占用内存低
- <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202404201319141.png" alt="image-20240420131949817" style="zoom:50%;" />

#### 下载方式

- Microsoft Store搜索即可Windows Terminal即可 Win10也可以下载使用
- [Windows Terminal - Microsoft Apps](https://apps.microsoft.com/detail/9n0dx20hk701?rtc=1&hl=en-us&gl=US)

#### 配置VPS

- 点击设置

- <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202404201325024.png" alt="image-20240420132530959" style="zoom: 50%;" />
- 点机JSON文件

- <img src="https://raw.githubusercontent.com/1v10/Photo/main/photo/202404201336231.png" alt="image-20240420132556177" style="zoom:50%;" />

- 会打开一个JSON文件 把已经存在配置复制一份

- ![image-20240420134045087](https://raw.githubusercontent.com/1v10/Photo/main/photo/202404201340123.png)

- 然后相关信息进行更改即可 最终效果 guid可以通过Power Shell生成

  - ```powershell
    [guid]::NewGuid()
    ```

  - ```json
    "list": 
    [
        {
            "commandline": "%SystemRoot%\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
            "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
            "hidden": false,
            "name": "Windows PowerShell"
        },
        {
            "commandline": "ssh   VPS用户名@IP地址 -p 22",
            "guid": "{ede02617-b3e8-4192-9ef1-16fa199f5de8}",
            "hidden": false,
            "name": "Tab显示名称"
        }
    ]
    ```

    

- 点击主页的小箭头就会多一个你刚才的配置 点击输入密码即可
- ![image-20240420132939297](https://raw.githubusercontent.com/1v10/Photo/main/photo/202404201329387.png)

- 如果你不想输入密码 通过配置SSH密钥方式  点击直接连接服务器

#### 美化 

- 网上有很多主题 我这里只说最简单的毛玻璃和透明 我感觉已经很好看了
- 同样的方式点开JSON配置文件 在Profiles中的defaults中增加以下选项即可 
- 第一个选项是开启毛玻璃 第二个选项是透明底
- ![image-20240420133431420](https://raw.githubusercontent.com/1v10/Photo/main/photo/202404201334467.png)

- 其实已经很好看了
- ![image-20240420134019524](https://raw.githubusercontent.com/1v10/Photo/main/photo/202404201340670.png)

