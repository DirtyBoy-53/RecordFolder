# WebService-(asmx)发布至IIS记录(VS2019) #
## 一、项目发布到本地文件夹 ##
###Ⅰ、通过解决方案点击发布###
![](https://s4.ax1x.com/2021/12/28/Ts7WPs.png)<br/>
###Ⅱ、选择目标为文件夹###
![TsqcVO.png](https://s4.ax1x.com/2021/12/28/TsqcVO.png)<br/>
###Ⅲ、填入路径###
![TsqyqK.png](https://s4.ax1x.com/2021/12/28/TsqyqK.png)<br/>
###Ⅲ、生成改解决方案后点击发布
![TsLwTS.png](https://s4.ax1x.com/2021/12/28/TsLwTS.png)<br/>
###Ⅳ、进入先前填写的路径，查看生成的文件###
![TsLH61.png](https://s4.ax1x.com/2021/12/28/TsLH61.png)<br/>
----------

##二、项目部署##
###Ⅰ、安装IIS###
<font color =#FF000>**控制面板** ➤ **程序功能** ➤ **打开或关闭windows功能**；</font><br/>
<font color =#FF000>**Internet Information Service**中勾选**Web管理工具**和**万维网服务**；</font><br/>
<font color =#FF000>将**万维网服务**中的**应用程序开发功能**全部勾选；</font><br/>
点击**确定**后等待更改完成<br/>
![Tsvdjs.png](https://s4.ax1x.com/2021/12/28/Tsvdjs.png)<br/>
###Ⅱ、验证IIS是否安装成功###
更改完成后建议先重启电脑，然后在浏览器网址栏输入localhost回车，如果出现下面的画面，即表明IIS安装成功。<font color =#ff000>(如果发生错误，请根据错误提示解决)</font><br/>
![T60Ite.png](https://s4.ax1x.com/2021/12/29/T60Ite.png)<br/>

###Ⅲ、环境部署###
1、**控制面板** ➤ **管理工具**(如果找不到，可以把右上角的查看方式改为小图标试一下) ➤ **Internet Information Services (IIS)管理器**<br/>

![T6DQPg.png](https://s4.ax1x.com/2021/12/29/T6DQPg.png)<br/>
2、双击打开**Internet Information Services (IIS)管理器**<br/>
![T6WudA.png](https://s4.ax1x.com/2021/12/29/T6WudA.png)
3、网站 ➤ 右键添加网站<br/>
填入网站名称,这个随意定义;<br/>
物理路径为先前发布生成的路径;<br/>
连接为 ➤ 特定用户 ➤ 用户名填写管理员账户(在开始处可以看到自己当前账户名) ➤ 密码为开机时输入的密码(我是没有密码，导致搞了好久都没搞出来，索性直接去添加了密码) ➤ 确认密码（和密码是一样的） ➤ 确认<br/>
![T6s7Uf.png](https://s4.ax1x.com/2021/12/29/T6s7Uf.png)<br/>
<br/>
账户名可以从开始这里点击账户即可查看<br/>
![T6cwvQ.png](https://s4.ax1x.com/2021/12/29/T6cwvQ.png)<br/>
测试设置（如果身份验证和授权都是通过就OK）<br/>
![T6y1Re.png](https://s4.ax1x.com/2021/12/29/T6y1Re.png)<br/>
IP地址不用更改<br/>
端口号改为8090<br/>
###Ⅳ、查看部署网站###
点击网站名 ➤ 浏览网站
![T6y5z4.png](https://s4.ax1x.com/2021/12/29/T6y5z4.png)<br/>
如果在网页能看到发布文件夹中的文件则表明基本成功<br/>
![T66nyj.png](https://s4.ax1x.com/2021/12/29/T66nyj.png)<br/>
单击后缀为axmx的文件，如果进入下图中的页面，则表明本次部署完成成功。<br/>
![T66N6J.png](https://s4.ax1x.com/2021/12/29/T66N6J.png)<br/>

**<font color =#FF000>2021/12/29 9:46:24 </font>**<br/>
**<font color =#FF000>本次记录是为了解决公司项目中的问题，方便下次更换电脑或新同事需要部署时给出适当的提示；  
记录中并没有贴出过程中遇到的所有错误，但大部分的错误都有明确的提示，相信都能根据提示解决。</font>**