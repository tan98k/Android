# Android VIew 和ViedFroup	

​	Android 系统中所有的UI类都是建立在View和ViewGroup两个类的基础上，所有的子类称为Widget，所有的ViewGroup的子类称为Layout

#### Android布局

​	FrameLayout（单帧布局）、LinearLayout（线性布局）、AbsoluteLayout（绝对布局）、RelativeLayout（相对布局）和TableLayout（表格布局）

##### FrameLayout

指定屏幕上的一块空白区域，在该区域填充一个单一对象。默认情况下，这些组件都将被固定在屏幕的左上角，后放入的组件会放在前一个组件上进行覆盖填充，形成部分遮挡或全部遮挡。



##### LinearLayout

​    该布局可以使放入其中的组件以水平方式或者垂直方式整齐排列，通过 android:orientation 属性指定具体的排列方式，通过 weight 属性设置每个组件在布局中所占的比重。

```xml
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical">

    <LinearLayout
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:layout_weight="1"
        android:orientation="horizontal">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="fill_parent"
            android:layout_gravity="center_horizontal"
            android:layout_weight="1"
            android:background="#aa0000"
            android:text="@string/red" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="fill_parent"
            android:layout_gravity="center_horizontal"
            android:layout_weight="1"
            android:background="#00aa00"
            android:text="@string/green" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="fill_parent"
            android:layout_gravity="center_horizontal"
            android:layout_weight="1"
            android:background="#0000aa"
            android:text="@string/blue" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="fill_parent"
            android:layout_gravity="center_horizontal"
            android:layout_weight="1"
            android:background="#aaaa00"
            android:text="@string/yellow" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:layout_weight="1"
        android:orientation="vertical">

        <TextView
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="@string/row1"
            android:textSize="15pt" />

        <TextView
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="@string/row2"
            android:textSize="15pt" />

        <TextView
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="@string/row3"
            android:textSize="15pt" />

        <TextView
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="@string/row4"
            android:textSize="15pt" />
    </LinearLayout>
</LinearLayout>
```

​	第一个布局通过orientation="horizontal" 将布局设置为横向排列。第二个布局通过orientation="vertical"将布局设置为纵向排列。

​	layout_weight 用于定义一个线性布局中某组件的重要程度。



##### RelativeLayout

相对布局，这种布局让组件以相对于容器或者容器内的另外一个组件的相对位置进行放置的布局

​															RelativeLayout 布局常用属性

|                  属性                   |                     描述                     |
| :-------------------------------------: | :------------------------------------------: |
|     android:layout_above="@id/xxx"      |          将控件置于给定 ID 控件之上          |
|     android:layout_below="@id/xxx"      |          将控件置于给定 ID 控件之下          |
|    android:layout_toLeftOf="@id/xxx"    |   将控件的右边缘和给定 ID 控件的左边缘对齐   |
|   android:layout_toRightOf="@id/xxx"    |   将控件的左边缘和给定 ID 控件的右边缘对齐   |
| android:layout_alignBaseline="@id/xxx"  | 将控件的 baseline 与给定 ID 的 baseline 对齐 |
|    android:layout_alignTop="@id/xxx"    |   将控件的上边缘和给定 ID 控件的上边缘对齐   |
|  android:layout_alignBottom="@id/xxx"   |   将控件的底边缘和给定 ID 控件的底边缘对齐   |
|   android:layout_alignLeft="@id/xxx"    |   将控件的左边缘和给定 ID 控件的左边缘对齐   |
|   android:layout_alignRight="@id/xxx"   |   将控件的右边缘和给定 ID 控件的右边缘对齐   |
|  android:layout_alignParentLeft="true"  |      将控件的左边缘和父控件的左边缘对齐      |
|  android:layout_alignParentTop="true"   |      将控件的上边缘和父控件的上边缘对齐      |
| android:layout_alignParentRight="true"  |      将控件的右边缘和父控件的右边缘对齐      |
| android:layout_alignParentBottom="true" |      将控件的底边缘和父控件的底边缘对齐      |
|  android:layout_centerInParent="true"   |          将控件置于父控件的中心位置          |
| android:layout_centerHorizontal="true"  |         将控件置于水平方向的中心位置         |
|  android:layout_centerVertical="true"   |         将控件置于垂直方向的中心位置         |

```xml
<?xml version="1.0" encoding="utf-8"?>

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent">

    <TextView
        android:id="@+id/label"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:text="@string/hello" />

    <EditText
        android:id="@+id/enter"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_below="@+id/label" />

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_below="@+id/enter"
        android:text="@string/butltext" />

    <Button
        android:id="@+id/ok"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignBottom="@+id/button1"
        android:layout_alignParentLeft="true"
        android:text="@string/but2text" />

</RelativeLayout>
```

##### tableLayout

表格布局，以行列的方式管理组件。

```xml
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent">
    <TableRow>
    	<TextView
                  android:text="column1"></TextView>
    </TableRow>
</TableLayout>    
```

TableLayout 布局提供了几个特殊属性，可以实现以下特殊效果。

- android:shrinkColumns 属性：该属性用于设置可收缩的列。当可收缩的列太宽以至于布局内的其他列不能完全显示时，可收缩列会纵向延伸，压缩自己所占的空间，以便于其他列可以完全显示出来。android:shrinkColumns="1" 表示将第 2 列设置为可收缩列，列数从 0 开始。
- android:stretchColumns 属性：该属性用于设置可伸展的列。可伸展的列会自动扩展长度以填满所有可用空间。android:stretchColumns="1" 表示将第 2 列设置为可伸展的列。
- android:collapseColumns 属性：该属性用于设置隐藏列。android:collapseColumns="1" 表示将第 2 列隐藏不显示。



##### AbsoluteLayout

​	绝对布局，放入该布局的组件需要通过 android:layout_x 和 android:layout_y 两个属性指定其准确的坐标值，并显示在屏幕上。

​	AbsoluteLayout 布局可用以完成任何的布局设计，灵活性很大，但是在实际的工程应用中不提倡使用这种布局。因为使用这种布局不但需要精确计算每个组件的大小，增大运算量，而且当应用程序在不同屏幕尺寸的手机上运行时会产生不同效果。

```xml
<?xml version="1.0" encoding="utf-8"?>
<AbsoluteLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_x="32px"
        android:layout_y="53px"
        android:text="Button" />

    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_x="146px"
        android:layout_y="53px"
        android:text="Button" />

    <Button
        android:id="@+id/button3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_x="85px"
        android:layout_y="135px"
        android:text="Button" />

</AbsoluteLayout>
```

layout_x:距离左边                                                             layout_Y:距离上面

- 像素：缩写为 px。表示屏幕上的物理像素。
- 磅：points，缩写为 pt。1pt 等于 1 英寸的 1/72，常用于印刷业。
- 放大像素：sp。主要用于字体的显示，Android 默认使用 sp 作为字号单位。
- 密度独立像素： dp，该尺寸使用 160dp 的屏幕作为参考，然后用该屏幕映射到实际屏幕，在不同分辨率的屏幕上会有相应的缩放效果以适用于不同分辨率的屏幕。
- 毫米：mm。

##### WebView

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

```xml
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical">

    <WebView
        android:id="@+id/webView1"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
    
</LinearLayout>
```

```java
package introduction.android.webView;

import android.app.Activity;
import android.os.Bundle;
import android.webkit.WebView;

public class WebViewDemoActivity extends Activity {
    private WebView webView;

    @Override
    public void onCreate(Bundle saveInstanceState) {
        super.onCreate(saveInstanceState);
        setContentView(R.layout.main);
        webView = (WebView) findViewById(R.id.webView1);
        webView.getSettings().setJavaScriptEnabled(true);
        webView.loadUrl("http://www.google.com");
    }
}
```





































































