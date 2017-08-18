---
layout: post
title:  "MFC界面美化攻略"
date:   2014-09-19 18:16:59
author: Akimoto
categories: Academics
tags:	MFC programming
cover:  "/assets/instacode.png"
---

# <font face="德彪钢笔行书字库"><font color="blue">资源文件：</font></font>
Bitmap:PS里输出24位windows的BMP图片<br />
Cursor:光标可以自绘<br />
Wave: WMV格式的声音文件<br />
ICON：这个网上可以转化<br />
# <font face="德彪钢笔行书字库"><font color="blue">1.字体：</font></font>
面板属性里更改。<br />
# <font face="德彪钢笔行书字库"><font color="blue">2.Edit控件文字颜色：</font></font>
添加CtlColor（），增添<br />
if (IDC_STATIC == pWnd->GetDlgCtrlID())//判断正在绘制的是不是指定的控件<br />
{<br />
pDC->SetTextColor(RGB(0, 0, 255));//设置它的文本显示<br />
}
# <font face="德彪钢笔行书字库"><font color="blue">3.背景图片：</font></font>
增添Paint（）函数，else后修改为<br />
//CDialogEx::OnPaint();   这句话注释掉<br />
		CPaintDC   dc(this);<br />
		CRect   rect;<br />
		GetClientRect(&rect);<br />
		CDC   dcMem;<br />
		dcMem.CreateCompatibleDC(&dc);<br />
		CBitmap   bmpBackground;<br />
		bmpBackground.LoadBitmap(IDB_BITMAP1);<br />
		BITMAP   bitmap;<br />
		bmpBackground.GetBitmap(&bitmap);<br />
		CBitmap   *pbmpOld = dcMem.SelectObject(&bmpBackground);<br />
		dc.StretchBlt(0, 0, rect.Width(), rect.Height(), &dcMem,0, <br />0,bitmap.bmWidth, bitmap.bmHeight, SRCCOPY);
# <font face="德彪钢笔行书字库"><font color="blue">4.背景音乐：</font></font>
添加头文件<br />
 #include <mmsystem.h><br />
 #pragma comment( lib, "Winmm.lib" )<br />
在InitDialog（）函数里写<br />
PlaySound((LPCTSTR)IDR_WAVE1, AfxGetInstanceHandle(), SND_RESOURCE | SND_ASYNC);
# <font face="德彪钢笔行书字库"><font color="blue">5.光标自绘：</font></font>
在资源里新建一个CURSOR,增添SetCursor（）函数，写入<br />
SetCursor(LoadCursor(AfxGetInstanceHandle(), MAKEINTRESOURCE(IDC_CURSOR2)));<br />
返回值记住改为false
# <font face="德彪钢笔行书字库"><font color="blue">6.皮肤更改：</font></font>
复制 SkinH.dll、SkinH.lib、SkinH.h 以及皮肤文件Aero.she 至工程目录下；<br />
在工程中引入 .h 头文件及 Lib 静态库，记得在stdafx.h里声明，<br />
 #include "SkinH.h"<br />
 #pragma comment(lib,"SkinH.lib")<br />
在创建窗口之前加载皮肤文件，这里是对话框初始化的时候，第一句。<br />
BOOL CPifuTestDlg::OnInitDialog()<br />
{<br />
	SkinH_AttachEx(("Aero.she"), NULL); //这句核心<br />
	CDialog::OnInitDialog();<br />
	……<br />
	……<br />
	return TRUE;  // return TRUE  unless you set the focus to a control<br />
}<br />
在销毁窗口之前卸载皮肤文件<br />
void CPifuTestDlg::OnDestroy() <br />
{<br />

SkinH_Detach();//这句是核心<br />
PostQuitMessage (0) ;<br />
CDialog::OnDestroy();<br />

// TODO: Add your message handler code here<br />

}
# <font face="德彪钢笔行书字库"><font color="blue">7.光标移至控件上时显示说明:</font></font>
首先在对话框类（CMyDlg)里添加一个m_ToolTip类对象（public:公有），CToolTipCtrl m_ToolTip;然后在对话框类里的OnInitDialog函数添加以下语句：<br />
m_ToolTip.Create(this);<br />
m_ToolTip.AddTool(&m_Quit,”文本信息”);<br />
其中m_Quit为按钮控件关联的变量<br />
接着往对话框类添加一个虚函数，步骤是右击对话框类，选择Add Virtual Function。然后双击左边列表框里PreTranslateMessage,把它添加到右边的列表框，然后双击右边列表框里的PreTranslateMessage，这样我们就添加了虚函数，这个虚函数有一个参数MSG *pMsg;MSG这个结构在API常用函数里有解释。这里只是说一下这个函数意思，这个函数会截获所有发送到对应窗口的消息。
在这个函数添加这个语句：m_ToolTip.RelayEvent(pMsg);<br />
完整的就是：<br />
BOOL CMyDlg::PreTranslateMessage(MSG* pMsg)<br />
{<br />
// TODO: Add your specialized code here and/or call the base class<br />
m_ToolTip.RelayEvent(pMsg);<br />
return CDialog::PreTranslateMessage(pMsg);<br />
}
# <font face="德彪钢笔行书字库"><font color="blue">8.显示系统时间：</font></font>
在InitDialog（）写入计时器<br />
SetTimer(1, 1000, NULL);<br />
增加Timer（）函数，写入<br />
{<br />
	// TODO:  在此添加消息处理程序代码和/或调用默认值<br />
	CTime time = CTime::GetCurrentTime();<br />
	CString sTime = time.Format(_T("%Y-%m-%d, %H:%M:%S"));<br />
	SetDlgItemText(IDC_EDIT5, sTime);<br />
	CDialogEx::OnTimer(nIDEvent);<br />
}
# <font face="德彪钢笔行书字库"><font color="blue">9.替换exe图标：</font></font>
在Bitmap中将原图标删去，新图标ID命名为IDB_MAINFRAME，替换后重新生成DeBug即可。



<!--
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

## Adding New Posts

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

### Tags and Categories

If you list one or more categories or tags in the front matter of your post, they will be included with the post on the page as links. Clicking the link will bring you to an auto-generated archive page for the category or tag, created using the [jekyll-archive][jekyll-archive] gem.

### Cover Images

To add a cover image to your post, set the "cover" property in the front matter with the relative URL of the image (i.e. <code>cover: "/assets/cover_image.jpg"</code>).

### Code Snippets

You can use [highlight.js][highlight] to add syntax highlight code snippets:

Use the [Liquid][liquid] `{% raw %}{% highlight <language> %}{% endraw %}` tag to add syntax highlighting to code snippets.

For instance, this template...
{% highlight html %}
{% raw %}{% highlight javascript %}    
function demo(string, times) {    
  for (var i = 0; i < times; i++) {    
    console.log(string);    
  }    
}    
demo("hello, world!", 10);
{% endhighlight %}{% endraw %}
{% endhighlight %}

...will come out looking like this:

{% highlight javascript %}
function demo(string, times) {
  for (var i = 0; i < times; i++) {
    console.log(string);
  }
}
demo("hello, world!", 10);
{% endhighlight %}

Syntax highlighting is done using [highlight.js][highlight]. You can change the active theme in [head.html](https://github.com/bencentra/centrarium/blob/2dcd73d09e104c3798202b0e14c1db9fa6e77bc7/_includes/head.html#L15).

### Images

Lightbox has been enabled for images. To create the link that'll launch the lightbox, add <code>data-lightbox</code> and <code>data-title</code> attributes to an <code>&lt;a&gt;</code> tag around your <code>&lt;img&gt;</code> tag. The result is:

<a href="//bencentra.com/assets/images/falcon9_large.jpg" data-lightbox="falcon9-large" data-title="Check out the Falcon 9 from SpaceX">
  <img src="//bencentra.com/assets/images/falcon9_small.jpg" title="Check out the Falcon 9 from SpaceX">
</a>

For more information, check out the [Lightbox][lightbox] website.

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
[highlight]:   https://highlightjs.org/
[lightbox]:    http://lokeshdhakar.com/projects/lightbox2/
[jekyll-archive]: https://github.com/jekyll/jekyll-archives
[liquid]: https://github.com/Shopify/liquid/wiki/Liquid-for-Designers--->
