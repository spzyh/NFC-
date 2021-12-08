在看了稚辉君的Link-Card项目两天之后，我深切意识到：凭我现在的能力怕是完全没办法复现。

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image.png)

于是，本想这圣诞节给朋友们送个link-card，但是似乎不太现实了。于是在GitHub上逛了一圈，遂找到了另一个有意思的NFC应用：NFC名片。

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/vcard-demo-1-576x1024.gif)

硬件比较简单，添加联系人的功能虽说没啥用，但聊胜于无了。

**电路设计**

硬件选择基本就是原项目的方案。

nfc芯片选择恩智浦的NT3H1101W0FHK，带1K存储器。

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image-1.png)

用这个芯片还有一个好处，它可以从外部NFC设备（手机等）获得电力，可以给一些低功耗的设备供电，给MCU供电估计不行，但是点个LED灯还是很容易的。

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image-2.png)

因此，基本的硬件设计还是很容易弄明白的：

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image-3.png)

因为原方案已经给出了天线设计，第一版我也没有深究，后来觉得最好还是验证一下谐振频率，看看是不是符合NFC的通信频率13.56MHZ。

首先计算天线电感：

电感计算网站：http://www.edatop.com/tools/nfc/158751.html

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image-4.png)

从datasheet中可以看到芯片的输入电容是50pF，带入LC电路的谐振频率计算公式可得：

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/07a0e3c1f84e242b763a7312665318c.png)

可以看到大概误差10%左右，不过考虑到我们实际使用的天线方案是圆角矩形，和模型中的矩形线圈还有些差距，所以方案应该是可行的。

为了验证，我又去意法半导体的NFC天线设计网站：https://eds.st.com/antenna/#/，验证了一下该天线方案：

输入天线参数，计算得：

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/16389656361-1024x623.png)

所以说后续如果还需要改进，可以考虑重新设计天线，最佳的天线电感应该为2.7uH左右，但是考虑到天线自己的电容，目前的参数也是可行的。

**PCB设计**

方案验证完成之后就是制造加工阶段了。

PCB的设计比较简单，总共也就4个元件，随便摆摆就行。但是这个画面确实太单调了：

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image-5.png)

刚好看见立创EDA有导入图片的功能，所以找了圆神的一张图片：

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/16383590431.png)

导入：

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image-6.png)

可恶，丑爆了！

询问了几个PCB厂家的客服，也没法在板子上印出花来，只能我画什么就印什么，还只能用一种颜色，那么看来只能靠点线面画出圆神了。

处理流程：

PS转线稿→色阶加深→AI转矢量线稿→手动处理→导出dxf文件。

- ![img](https://www.zyhweb.com/wp-content/uploads/2021/12/微信图片_20211208202901.png)
- ![img](https://www.zyhweb.com/wp-content/uploads/2021/12/微信图片_202112082029011.png)
- ![img](https://www.zyhweb.com/wp-content/uploads/2021/12/微信图片_202112082029012.png)

将处理好的文件导入立创EDA，完美！

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image-7.png)

**PCB制造**

从EDA导出Gerber文件之后，直接在嘉立创下单助手下单

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image-8-1024x500.png)

另外，如果不希望嘉立创在板子上印你的客户编号，要把不需要客户编号选上，其余大多数选项保持默认即可。

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/image-9-1024x500.png)

下单支付，等待快递。

此外，从EDA导出的BOM表，可以在网上任何一家淘宝店购买，不建议去立创商城（基本贵一倍）。

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/16389673341.png)

当然，有钱的同学推荐直接在嘉立创做SMT贴片，成本大约15-20/张。

购买元件自己焊接的成本大概5元/张（手残党除外）。

**使用方法**

终于得到成品。

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/efb5815bc09e1468c571b610cd3f82d.jpg)

现在所需要的工具，就是一个带NFC功能的手机，需要安装一款NFC读写软件NFC Tool Pro。
链接：https://pan.baidu.com/s/11uJz1nscOVvMSmZnw2qEJA
提取码：xgva
--来自百度网盘超级会员V5的分享

安装完成后，打开手机的NFC，在写/添加记录/联系人中录入自己的信息。

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/91da27833290a11bf916d93a0de6d23-461x1024.jpg)

ok/写入。

此时，NFC名片便存储了你的个人信息，靠近任何一个开着NFC功能的手机都可以直接添加联系人。如图所示：

![img](https://www.zyhweb.com/wp-content/uploads/2021/12/7fca0f072d174ad5e14943c7e9e802e-461x1024.jpg)

**结语**

教程参见我的个人网站：https://www.zyhweb.com/nfc%e5%90%8d%e7%89%87/

所有工程文件已上传至Github：https://github.com/spzyh/NFC-Card。

另外，带电路的NFC名片不可避免地会因为电子元件的厚度无法很好地存放，现在如果只是单纯地将一些信息存在一些小物件上，可以通过NFC标签来实现，大可不必如此绕远路通过这种办法。