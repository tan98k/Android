

## DAY　01

| Android 架构 |                                                              |
| :----------- | ------------------------------------------------------------ |
| 应用程序     |                                                              |
| 应用框架     | 活动管理器、窗口管理器、内容提供者、视图系统、包管理器、电话管理器、资源管理器、位置管理器、通知管理器 |
| 核心类库     |                                                              |
| Linux内核    |                                                              |

------

#### 4类组件：

​	Activity、Service、BroadcastReceiver、ContentPrivider

##### Activity

​	Activity 是用户和应用程序交互的窗口。Activity 之间的跳转可以有返回值。

​    Activity以栈的形式维护，有自己的生命周期，在不同的时期会调用不同的方法：创建 onCreate()、激活 onStart()、恢复 onResume()、暂停 onPause()、停止 onStop()、销毁 onDestroy()和重启 onRestart() 等



##### Service

​	Service 是没有视图的程序，它没有用户界面，可以在后台运行，相当于一个服务。

​	通过 Context.startService(Intent service) 可以启动一个 Service，通过 Context. bindService() 可以绑定一个 Service。



##### BroadcastReceiver

​	它用来接收来自系统和其他应用程序的广播，并做出回应。

​	只要注册了 BroadcastReceiver，即使对应的事件广播来临时应用程序并未启动，系统也会自动启动该应用程序对事件进行处理。另外，用户还可以通过 Context.sendBroadcast() 将自己的 Intent 对象广播给其他的应用程序。

​	BroadcastReceiver 的 2 种注册方式：

- 在 AndroidManifest. xml 中进行静态注册；
- 在运行时的代码中使用 Context.registerReceiver() 进行动态注册。



##### ContentProvider

​	文件、数据库等数据在 Android 系统内是私有的，仅允许被特定应用程序直接使用。在两个程序之间，数据的交换或共享由 ContentProvider 实现。

​	

------

### 组件

##### Activity

​	activity的注册：在 <application> 标签下添加 <activity> 标签

```xml
<manifest ... >
    <application ... >
        <activity android:name = ".ExampleActivity" />
        ...
    </application ... >
    ...
</manifest >
```

​	如果是主Activity，为其添加 <intent-filter> 标签

```
<activity Android:name = ".ExampleActivity" Android:icon = "@drawable/app_icon">
    <intent-filter>
        <action Android:name = "Android.intent.action.MAIN" />
        <!-表示该 Activity 作为主 Activity 出现-->
        <category Android:name = "Android.intent.category.LAUNCHER" />
        <!-表示该 Activity 会被显示在最上层的启动列表中。 -->
    </intent-filter>
</activity>
```

​	启动Activity

```java
//一般通过startActivity()来启动，其信息有Intent对象来传递
Intent intent = new Intent(this,AnotherActivity.class);
startActivity(intent);
//启动名字为AnotherActivity的Activity
```

```java
/*有时，用户不需要知道要启动的 Activity 的名字，而可以仅制定要完成的行为，由 Android 系统来为用户挑选合适的 Activity*/
Intent intent = new Intent(Intent.ACTION_SEND);
intent.putExtra(Intent.EXTRA_EMAIL,recipientArray);
//Intent.EXTRA_EMAIL 放置的是 recipientArray 中存储的要发送的 E-mail 的目标地址
startActivity(intent);
```

```java
/*当需要从启动的Activity获取返回值的说话，使用startActivityForResult()代替startActivity()，并且实现onActivityResult()方法来获取返回值*/
Intent intent = new Intent(Intent.ACTION_PICK,Contacts.CONTENT_URI);
startActivityForResult(intent,PICK_CONTACT_REQUEST);
//用户选择了联系人后，相关信息会被存储到Intent对象中，并且返回onActivityResult()方法中
```

​	关闭Activity

```
//使用finish()方法关闭 Activity ，使用finishActivity()方法关闭之前启动的其他Activity
```

#### Activity 数据传递

Activity数据传递共有三种方式：

1. 通过Intent传递简单数据
2. 通过Bundle传递相对复杂的数据或者对象
3. 通过startActivityForResult可以方便地进行来回传递

##### 使用intent

```java
//在Activity1传递数据
Intent intent = new Intent(Activity1.this, Activity2.class);
intent.putExtra("authot", "leebo");
Activity1.this.startActivity(intent);

//在Activity2取出数据
Intent intent = getIntent();
String value = intent.getStringExtra("author");
```

##### 使用Bundle

```
//在传递数据的 Activity1 中：
Intent intent = new Intent(Activity1.this, Activity2.class);
Bundle myBundle = new BUndle();
myBundle.putString("author","leebo");
intent.putExtras(myBundle);
Activity1.this.startActivity(intent);

//在取出数据的 Activity2 中:
Intent intent = getIntent();
BUndle myBundle = intent.getExtras();
String value = myBundle.getString("author");
```

##### 使用startActivityForResult

```java
//在Activity1中
final int REQUEST_CODE = 1;
Intent intent = new Intent(Activity1.this, Activity2.class);
Bundle myBundle = new Bundle();
myBundle.putString("author","leebo");
intent.putExtras(myBundle);
startActicityForResult(intent, REQUEST_CODE);

//重载onActivityResult方法，来接收传过来的数据
protected void onActivityResult(int requestCode, int resultCode, Intent intent){
	if(requestCode == this.REQUEST_CODE){
		switch(resultCode){
			case RESULT_OK:
				Bundle b = intent.getExtras();
				String str = b,getString("Result");
				break;
			default:
				break;
		}
	}
}

//在Activity2中
Intent intent = getIntent();
Bundle myBundle = getIntent().getExtras();
String author = getBundle.getString("author");
Intent intent = new intent();
Bundle bundle = new Bundle();
bundle.putString("Result", "from Activity2");
intent.putExtras(bundle);
Activity2.this.setResult(RESULE_OK, intent);
finish();
```

------

##### Android 资源

三种类型的资源文件：XML 文件、位图文件（图像）和 RAW 文件（声音等）。

------

### AndroidManifest.xml

​	AndroidManifest.xml包含了安卓系统运行程序前所需要的重要信息，包括名称、图标、包名称、模块组成、授权、sdk最低版本等

```XML
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android = "http://schemas.android.com/apk/res/android"
    package = "demo.hbyz.myapplication3">

    <application
        android:allowBackup = "true"
        android:icon = "@mipmap/ic_launcher"
        android:label = "@string/app_name"
        android:roundIcon = "@mipmap/ic_launcher_round"
        android:supportsRtl = "true"
        android:theme = "@style/AppTheme">

        <activity android:name = ".MainActivity">
            <intent-filter>
                <action android:name = "android.intent.action.MAIN" />
                <category android:name = "android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

    </application>

</manifest>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest>

    <uses-permission />
    <permission />
    <permission-tree />
    <permission-group />
    <instrumentation />
    <uses-sdk />
    <uses-configuration /> 
    <uses-feature /> 
    <supports-screens /> 
    <compatible-screens /> 
    <supports-gl-texture /> 

    <application>

        <activity>
            <intent-filter>
                <action />
                <category />
                <data />
            </intent-filter>
            <meta-data />
        </activity>

        <activity-alias>
            <intent-filter>. . .</intent-filter>
            <meta-data />
        </activity-alias>

        <service>
            <intent-filter>. . .</intent-filter>
            <meta-data/>
        </service>

        <receiver>
            <intent-filter>. . .</intent-filter>
            <meta-data />
        </receiver>

        <provider>
            <grant-uri-permission />
            <meta-data />
            <path-permission />
        </provider>

        <uses-library />

    </application>

</manifest>
```

manifest标签:根标签

applicatrion:应用标签，只能有一个

|   名称   |                             作用                             |
| :------: | :----------------------------------------------------------: |
| activity | 每一个 Activity 都要求有一个 activity 标签,并使用 Android:name 属性来指定类的名称。这必须包含核心的启动 Activity 和其他所有可以显示的屏幕或者对话框。每一个 Activity 节点都允许使用 intent-filter 子标签来指定哪个 Intent 启动该活动。 |
| service  | 应用程序中使用的每一个 Service 类都要创建一个新的 service 标签。（Service 标签也支持使用 intent-filter 子标签来允许后面的运行时绑定。） |
| provider | provider 标签用来说明应用程序中的每一个内容提供器。内容提供器是用来管理数据库访问以及程序内和程序间共享的。 |
| receiver | 通过添加 receiver 标签，可以注册一个广播接收器，而不用事先启动应用程序。广播接收器就像全局事件监听器一样，一旦注册了之后，无论何时，只要与它相匹配的 Intent 被应用程序广播出来，它就会立即执行。通过在声明中注册一个广播接收器，可以使这个进程实现完全自动化。如果一个匹配的 Intent 被广播了，应用程序就会自动启动，你注册的广播接收器也会开始运行。 |

uses-permission:声明自定义的权限

perssion:限制访问某个应用程序组件



#### 线程操作

主线程为UI线程，Android 的单线程模式必须遵守两个规则：

- 不允许阻塞 UI 线程。

- 不允许在 UI 线程之外访问 Android 的 UI 组件包。

  

  ```
  public void onClick(View v){
      new Thread(new Runnable(){
          public void run(){
              Bitmap b = loadImageFrameWork("http://example.com.image.png");
              mImageView.setImageBitmap(b);
          }
      }).start();
  }
  //这段代码违反了单线程模式的第二原则，不能在UI线程外访问Android的UI组件包。
  ```

  ##### Android 提供了几种方法，从其他线程中访问 UI 线程：

  - Activity.runOnUiThread（可运行）
  - View.post（可运行）
  - View.postDelayed（Runnable接口，长）

```java
//使用View.post(Runnable)来修正上面代码
public void onClick(View v){
    new Thread(new Runnable(){
        public void run(){
            final Bitmap bitmap =  loadImageFrameNetWork("http://example.com/image.png");
            mImageView.post(new Runnable(){
                public void run(){
                    mImageView.setImageBitmap(bitmap);
                }
            });
        }
    }).start();
}
```

##### 使用异步任务(AsyncTask)

```java
/*
	异步任务允许以异步的形式对用户界面进行操作。先阻塞工作线程，再在UI线程中呈现结果，此过程不对线程和handler进行人工干预
	使用异步任务，需继承AsyncTask类并且实现dolnBackground回调方法，该对象运行在后台线程池中
	要更新UI时，需要实现onPostExecute()方法来分发doOInBackground()返回的结果。由于此方法运行在UI线程中，因此能够安全地更新UI，然后在UI线程中调用execute()来执行任务。	
*/
public void onClick(View v){
    new DownloadImageTask().execute("http://example.com/image.png");
}

private class DownloadImageTask extends AsyncTask<String, Void, Bitmap>{
    protected Bitmap doInBackground(String[] urls){
        return loadImageFromNetwork(urls[0]);
    }
    //用于分发doOInBackground()返回的结果
    protected void onPostExecute(Bitmap result){
        mImageView.setImageBitmap(result);
    }
}
```

AsyncTask 工作方式的概述：

- 可以用 generics 来指定参数的类型、进度值和任务最终值。
- 工作线程中的 doInBackground() 方法会自动执行。
- onPreExecute()、onPostExecute() 和 onProgressUpdate() 方法都在 UI 线程中调用。
- doInBackground() 的返回值会传给 onPostExecute()。
- 在 doInBackground() 内的任何时刻，都可以调用 publishProgress() 来执行 UI 线程中的 onProgressUpdate()。
- 可以在任何时刻、任何线程内取消任务。





















































