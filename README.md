# NFC-卡片
基于恩智浦NT3H1101W0FHK的NFC名片设计
<!-- wp:paragraph -->
<p>在看了稚辉君的Link-Card项目两天之后，我深切意识到：凭我现在的能力怕是完全没办法复现。</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1273,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image.png" alt="" class="wp-image-1273"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>于是，本想这圣诞节给朋友们送个link-card，但是似乎不太现实了。于是在GitHub上逛了一圈，遂找到了另一个有意思的NFC应用：NFC名片。</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1281,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/vcard-demo-1-576x1024.gif" alt="" class="wp-image-1281"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>硬件比较简单，添加联系人的功能虽说没啥用，但聊胜于无了。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size"><strong>电路设计</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>硬件选择基本就是原项目的方案。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>nfc芯片选择恩智浦的NT3H1101W0FHK，带1K存储器。</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1276,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image-1.png" alt="" class="wp-image-1276"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>用这个芯片还有一个好处，它可以从外部NFC设备（手机等）获得电力，可以给一些低功耗的设备供电，给MCU供电估计不行，但是点个LED灯还是很容易的。</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1279,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image-2.png" alt="" class="wp-image-1279"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>因此，基本的硬件设计还是很容易弄明白的：</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1284,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image-3.png" alt="" class="wp-image-1284"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>因为原方案已经给出了天线设计，第一版我也没有深究，后来觉得最好还是验证一下谐振频率，看看是不是符合NFC的通信频率13.56MHZ。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>首先计算天线电感：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>电感计算网站：http://www.edatop.com/tools/nfc/158751.html</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1288,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image-4.png" alt="" class="wp-image-1288"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>从datasheet中可以看到芯片的输入电容是50pF，带入LC电路的谐振频率计算公式可得：</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1292,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/07a0e3c1f84e242b763a7312665318c.png" alt="" class="wp-image-1292"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>可以看到大概误差10%左右，不过考虑到我们实际使用的天线方案是圆角矩形，和模型中的矩形线圈还有些差距，所以方案应该是可行的。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>为了验证，我又去意法半导体的NFC天线设计网站：<a href="https://eds.st.com/antenna/#/">https://eds.st.com/antenna/#/</a>，验证了一下该天线方案：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>输入天线参数，计算得：</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1299,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/16389656361-1024x623.png" alt="" class="wp-image-1299"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>所以说后续如果还需要改进，可以考虑重新设计天线，最佳的天线电感应该为2.7uH左右，但是考虑到天线自己的电容，目前的参数也是可行的。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size"><strong>PCB设计</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>方案验证完成之后就是制造加工阶段了。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>PCB的设计比较简单，总共也就4个元件，随便摆摆就行。但是这个画面确实太单调了：</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1308,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image-5.png" alt="" class="wp-image-1308"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>刚好看见立创EDA有导入图片的功能，所以找了圆神的一张图片：</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1310,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/16383590431.png" alt="" class="wp-image-1310"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>导入：</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1311,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image-6.png" alt="" class="wp-image-1311"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>可恶，丑爆了！</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>询问了几个PCB厂家的客服，也没法在板子上印出花来，只能我画什么就印什么，还只能用一种颜色，那么看来只能靠点线面画出圆神了。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>处理流程：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>PS转线稿→色阶加深→AI转矢量线稿→手动处理→导出dxf文件。</p>
<!-- /wp:paragraph -->

<!-- wp:gallery {"ids":[1314,1315,1316],"linkTo":"none"} -->
<figure class="wp-block-gallery columns-3 is-cropped"><ul class="blocks-gallery-grid"><li class="blocks-gallery-item"><figure><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/微信图片_20211208202901.png" alt="" data-id="1314" data-full-url="https://www.zyhweb.com/wp-content/uploads/2021/12/微信图片_20211208202901.png" data-link="https://www.zyhweb.com/nfc%e5%90%8d%e7%89%87/%e5%be%ae%e4%bf%a1%e5%9b%be%e7%89%87_20211208202901/" class="wp-image-1314"/></figure></li><li class="blocks-gallery-item"><figure><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/微信图片_202112082029011.png" alt="" data-id="1315" data-full-url="https://www.zyhweb.com/wp-content/uploads/2021/12/微信图片_202112082029011.png" data-link="https://www.zyhweb.com/nfc%e5%90%8d%e7%89%87/%e5%be%ae%e4%bf%a1%e5%9b%be%e7%89%87_202112082029011/" class="wp-image-1315"/></figure></li><li class="blocks-gallery-item"><figure><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/微信图片_202112082029012.png" alt="" data-id="1316" data-full-url="https://www.zyhweb.com/wp-content/uploads/2021/12/微信图片_202112082029012.png" data-link="https://www.zyhweb.com/nfc%e5%90%8d%e7%89%87/%e5%be%ae%e4%bf%a1%e5%9b%be%e7%89%87_202112082029012/" class="wp-image-1316"/></figure></li></ul></figure>
<!-- /wp:gallery -->

<!-- wp:paragraph -->
<p>将处理好的文件导入立创EDA，完美！</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1319,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image-7.png" alt="" class="wp-image-1319"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size"><strong>PCB制造</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>从EDA导出Gerber文件之后，直接在嘉立创下单助手下单</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1324,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image-8-1024x500.png" alt="" class="wp-image-1324"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>另外，如果不希望嘉立创在板子上印你的客户编号，要把不需要客户编号选上，其余大多数选项保持默认即可。</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1326,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/image-9-1024x500.png" alt="" class="wp-image-1326"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>下单支付，等待快递。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>此外，从EDA导出的BOM表，可以在网上任何一家淘宝店购买，不建议去立创商城（基本贵一倍）。</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1332,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/16389673341.png" alt="" class="wp-image-1332"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>当然，有钱的同学推荐直接在嘉立创做SMT贴片，成本大约15-20/张。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>购买元件自己焊接的成本大概5元/张（手残党除外）。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size"><strong>使用方法</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>终于得到成品。</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1338,"sizeSlug":"full","linkDestination":"none"} -->
<figure class="wp-block-image size-full"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/efb5815bc09e1468c571b610cd3f82d.jpg" alt="" class="wp-image-1338"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>现在所需要的工具，就是一个带NFC功能的手机，需要安装一款NFC读写软件NFC Tool Pro。<br>链接：https://pan.baidu.com/s/11uJz1nscOVvMSmZnw2qEJA<br>提取码：xgva<br>--来自百度网盘超级会员V5的分享</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>安装完成后，打开手机的NFC，在写/添加记录/联系人中录入自己的信息。</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1344,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/91da27833290a11bf916d93a0de6d23-461x1024.jpg" alt="" class="wp-image-1344"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>ok/写入。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>此时，NFC名片便存储了你的个人信息，靠近任何一个开着NFC功能的手机都可以直接添加联系人。如图所示：</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":1347,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img src="https://www.zyhweb.com/wp-content/uploads/2021/12/7fca0f072d174ad5e14943c7e9e802e-461x1024.jpg" alt="" class="wp-image-1347"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph {"fontSize":"medium"} -->
<p class="has-medium-font-size"><strong>结语</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>所有工程文件已上传至Github：。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>另外，带电路的NFC名片不可避免地会因为电子元件的厚度无法很好地存放，现在如果只是单纯地将一些信息存在一些小物件上，可以通过NFC标签来实现，大可不必如此绕远路通过这种办法。</p>
<!-- /wp:paragraph -->
