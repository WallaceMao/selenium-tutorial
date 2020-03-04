# selenium IDE



## 1 提纲

### 1.1 selenium IDE快速生成自动化测试脚本

提前准备工作：

- 安装firefox火狐浏览器：https://www.firefox.com.cn/

- 安装selenium IDE火狐浏览器插件，用新安装的火狐浏览器打开：https://addons.mozilla.org/zh-CN/firefox/addon/selenium-ide/

- 确认火狐浏览器的右上角出现带有“Se”图标的插件，点击后可以打开selenium IDE



### 1.2 selenium测试代码解析

### 1.3 selenium高级用法



## 1 说明

selenium 三大组件：



- selenium WebDriver：使用脚本代码来驱动浏览器，模拟人的操作。

- selenium IDE：图形化界面用来录制浏览器操作，生成java/python/js/C#等多种语言的测试脚本代码

- selenium Grid：用来部署到多台机器上，同时进行计算。只需要写一遍测试代码，就可以同时测试不同操作系统、类型、分辨率下浏览器的表现。



关于selenium IDE

```

Though you will be able to use Selenium IDE without prior knowledge in programming, you should at least be familiar with HTML, JavaScript, and the DOM (Document Object Model) to utilize this tool to its full potential.

```



## 2 从一个例子入手

### 2.1 录制浏览器操作

- 1. 在IDE中点击“Add new test”，新增一个test，命名为“1-浏览器录制”。

- 2. 点击IDE中的“Start recording”按钮，输入url：https://www.tingkelai.com，IDE会自动启动浏览器，打开https://www.tingkelai.com页面，如果没有全屏显示，可以设置窗口最大化。

- 3. 点击右上角的“登录”按钮，跳转到登录页面，输入不存在的账户（abcd）和密码（123），点击“登录”按钮

- 4. 弹出“账户或密码错误”提示

- 5. 点击IDE中的“Stop recording”按钮，停止录制。

- 6. 在IDE中点击“Save project”按钮，保存项目。



### 2.2 运行录制好的命令

- 连续运行命令（可条件命令运行速度）：点击IDE中“Run current test”按钮。

- 单步运行命令：点击选中其中一条命令，点击IDE中的“Step over current command”按钮，将从选中的命令开始，单步执行。

- 断点运行：与单步运行类似。



## 3 三种类型的命令

### 3.1 Action（行动）

模拟人在网页上的操作：鼠标操作、键盘操作等，常用的Action命令有：



- open：浏览器打开网页

- click：鼠标点击

- double click：鼠标双击

- mouse over：鼠标移动

- type：键盘输入



### 3.2 Asserstion（条件判断）

判断某种条件是否符合



- assert：严格断言，一旦条件不符合，马上终止测试

- verify：不严格验证，即使条件不符合，只会打印一条错误信息，测试会继续

- waitFor：等待条件满足。条件满足了就继续，超过30s不满足会超时



### 3.3 Accessor（存储）

用来存储变量



## 4 Action基本操作——手动创建脚本

### 4.1 脚本创建过程

- 1. 在IDE中点击“Add new test”，新增一个test，命名为“2-Action命令演示”。

- 2. 确认base url中的网址是：https://www.tingkelai.com。

- 3. open /tingkelai/login：open命令可以打开相对路径，也可以打开绝对路径

- 4. set window size 1550x838：设置浏览器大小，防止元素不显示。点击“Run current test”运行一遍，打开浏览器。

- 5. type id=name 13810360000，可以使用“Select target in page”按钮

- 6. type id=password 123456，可以使用“Select target in page”按钮

- 7. click css=.ant-btn，可以使用“Select target in page”按钮

- 8. 点击“Run current test”运行一遍，打开浏览器。

- 9. mouse over css=.listBox:nth-child(3)，可以使用“Select target in page”按钮

- 10. click css=.showBtn，可以使用“Select target in page”按钮

- 11. 在IDE中点击“Save project”按钮，保存项目。



说明：

- 如果去掉第9步，直接使用click命令，脚本将不能正常运行，会一直卡在等待状态，直到30秒之后超时报错。这是因为第10步中点击的元素“css=.showBtn”在页面上是不显示的，需要在脚本中先使用mouse over命令让鼠标移动到元素上，等元素显示出来之后再点击。selenium模拟的是人对浏览器的操作，模拟过程中不能有人的干预。



## 5 Assertion基本操作

### 5.1 脚本创建过程

- 1. 在IDE中点击“Add new test”，新增一个test，命名为“3-Assertion命令演示”。

- 2. 确认base url中的网址是：https://www.tingkelai.com。

- 3. open /tingkelai/login

- 4. set window size 1550x838：设置浏览器大小，防止元素不显示。点击“Run current test”运行一遍，打开浏览器。

- 5. verify title 听客来：验证title，验证失败仍然继续执行

- 6. assert title 听客来：断言title，验证失败终止命令执行

- 7. assert text css=.desc 中国第一套助听器门店专用的销售管理软件：断言某个元素所含的文本

- 7. type id=name abcd

- 8. type id=password 123

- 9. click css=.ant-btn

- 10. wait for element visible css=.ant-message 30000：等待某个元素出现

- 11. assert text css=.ant-message 账号或密码错误：验证元素信息



说明：

- 在第10步时，原本css=.ant-message这个元素是不显示的，等请求返回了之后才会显示，所以这里需要使用wait for xxx命令等待元素显示了再执行验证。

- 在第11步时，由于css=.ant-message这个元素显示的时间比较短，可能来不及点击“Select target in page”按钮选择这个元素。这种情况下的处理方式有两种：（1）查页面源代码；（2）咨询开发页面的前端工程师



## 6 Accessor基本操作

### 6.1 脚本创建过程

- 1. 在IDE中点击“Add new test”，新增一个test，命名为“4-Accessor命令演示”。

- 2. 确认base url中的网址是：https://www.tingkelai.com。

- 3. open /tingkelai/login

- 4. store abcde phoneNumber

- 5. echo ${phoneNumber}

- 6. store text css=.desc desc

- 7. echo ${desc}

- 8. type id=name ${desc}



说明：

- echo命令可以将变量打印到log面板，log面板记录了命令执行的过程



## 7 多标签操作

### 7.1 脚本创建过程

- 1. 在IDE中点击“Add new test”，新增一个test，命名为“5-多标签操作演示”。

- 2. 确认base url中的网址是：https://www.tingkelai.com。

- 3. open /tingkelai/login

- 4. set window size 1550x838

- 5. store window handle mainWindow

- 6. click linkText=申请试用，注意要在这里点击“add new window configuration”，设置window name为“applyWindow”

- 7. select window handle=${applyWindow}

- 8. type css=.text-field > .ant-input abcd，可以用“Select target in page”选择

- 9. select window handle=${mainWindow}

- 10. type id=name 13810360000

- 11. close

- 12. select window handle=${applyWindow}

- 13. close



## 8 语句控制

### 8.1 条件判断

- if/else if/else/end



### 8.2 循环

- times/end

- do/repeat if

- while/end



### 8.3 执行js脚本

- execute script

- execute async script



### 8.3 脚本创建过程演示

- 1. 在IDE中点击“Add new test”，新增一个test，命名为“6-语句控制演示”。

- 2. 确认base url中的网址是：https://www.tingkelai.com。

- 3. execute script return 'abcd' myVar1

- 4. echo ${myVar1}

- 5. if

- 6. echo success

- 7. else

- 8. echo fail

- 9. end

- 10. times 3

- 11. echo hello

- 12. end



## alert/prompt/confim弹窗（略）



```

Because of its simplicity, Selenium IDE should only be used as a prototyping tool, not an overall solution for developing and maintaining complex test suites.

```