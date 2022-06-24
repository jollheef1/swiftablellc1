
ctwin32-dialog
=============================

>平时写对话框程序挺多的，一般都是在VS里直接拉一个框然后CreateDialog(xxx)
>写来写去发现繁琐的东西不少，后来就写了这个 - 简单的封装。

>\#include "stdafx.h" 这个是vs的预编译头，不是用vs编译的话直接删除就好了

>代码量很少，简单的浏览下头文件就知道大概怎么调用了


#### 例子：

```c++

// about button callback
// 回调的格式是这样， @hDlg = 父窗口   @windowId是本按钮的id
int CALLBACK about_callback( HWND hDlg, DWORD windowId )
{
	MessageBoxA( 0, "callback runninig!", "", 0 );
	return 0;
}

// main dialog
void show()
{
	//初始化对话框
	ctwin32::ctDialog ctd;
	ctd.createMainDialog( 560, 280 );
	//
	ctd.setTitle( "Running..." );
	//
	//背景色
	ctd.setbgcolor( RGB( 240, 240, 240 ) );
	//前景色
	RECT rt = {0,ctd.hMainDlgRect.bottom-70,
        ctd.hMainDlgRect.right,ctd.hMainDlgRect.bottom};
	ctd.setForecolor( RGB( 35, 39, 54 ), rt );

	//其他组件
	ctd.drawBmp( IDB_BITMAP1, 150, 70, 50, 50 );        //现在只支持bmp格式
	ctd.setFontColor( RGB( 81,81,81 ) );
	ctd.createText( "正在初始化网络配置...", 200, 85, 300, 40, 26 );
	ctd.createbutton( "about", 10, 10, about_callback );

	// UI消息循环开始，线程在这里阻塞
	ctd.showMainDialog();
}

// entry.
int main()
{
	show();
    return 0;;
}

```
里面用到的IDB_BITMAP1 （上传的是jpg格式 ，转为bmp即可）：
![输入图片说明](http://git.oschina.net/uploads/images/2016/1129/021949_1e9e57ad_632350.jpeg "在这里输入图片标题")


测试一下，效果如下：
![输入图片说明](http://git.oschina.net/uploads/images/2016/1129/111557_a32a98d4_632350.jpeg "在这里输入图片标题")
