## Android部分组件



##### CheckBox

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingRight="10dp"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:orientation="vertical"
    app:layout_behavior="@string/appbar_scrolling_view_behavior"
    tools:context=".MainActivity">

    <TextView android:text="爱好:"
        android:textSize="24sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/tv" />

    <RelativeLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content">
        <CheckBox
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="音乐"
            android:id="@+id/chb_music"
            android:layout_alignParentLeft="true"
            android:layout_alignParentStart="true"
            android:layout_marginTop="10dp"
            android:checked="false" />

        <CheckBox
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="游戏"
            android:id="@+id/chb_game"
            android:layout_below="@+id/chb_music"
            android:layout_alignParentLeft="true"
            android:layout_alignParentStart="true" />

        <CheckBox
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="旅游"
            android:id="@+id/chb_trip"
            android:layout_alignTop="@+id/chb_music"
            android:layout_alignRight="@+id/chb_film"
            android:layout_alignLeft="@+id/chb_film" />

        <CheckBox
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="看电影"
            android:id="@+id/chb_film"
            android:layout_below="@+id/chb_trip"
            android:layout_alignParentRight="true"
            android:layout_alignParentEnd="true" />

    </RelativeLayout>
    <Button
        android:id="@+id/end"
        android:text="完成"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

    <TextView
        android:paddingTop="10dp"
        android:id="@+id/result_tv"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        />
</LinearLayout>
```

​	CompoundButton.OnCheckedChangedListener 接口可用于对 CheckBox 的状态进行监听。当 CheckBox 的状态在未被选中和被选中之间变化时，该接口的 onCheckedChanged() 方法会被系统调用。CheckBox 通过 setOnCheckedChangeListener() 方法将该接口对象设置为自己的监听器。

```java
package introduction.android.widgetdemo;

import android.os.Bundle;
import android.support.design.widget.FloatingActionButton;
import android.support.design.widget.Snackbar;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.Toolbar;
import android.view.View;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.CompoundButton;
import android.widget.TextView;
import java.util.ArrayList;

public class MainActivity extends AppCompatActivity implements CompoundButton.OnCheckedChangeListener {
    private CheckBox musicCkb;
    private CheckBox tripCkb;
    private CheckBox filmCkb;
    private CheckBox gameCkb;
    private TextView result_tv;
    private Button endBtn;
    //爱好数组
    ArrayList<String> hobbies=new ArrayList<String>();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //初始化控件
        musicCkb = (CheckBox) findViewById(R.id.chb_music);
        tripCkb = (CheckBox) findViewById(R.id.chb_trip);
        filmCkb = (CheckBox) findViewById(R.id.chb_film);
        gameCkb = (CheckBox) findViewById(R.id.chb_game);
        result_tv = (TextView) findViewById(R.id.result_tv);
        endBtn= (Button) findViewById(R.id.end);
        //设置监听器
        musicCkb.setOnCheckedChangeListener(this);
        tripCkb.setOnCheckedChangeListener(this);
        filmCkb.setOnCheckedChangeListener(this);
        gameCkb.setOnCheckedChangeListener(this);
        //为button设置监听器
        endBtn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                StringBuilder sb=new StringBuilder();
              for (int i =0;i<hobbies.size();i++) {
                  //把选择的爱好添加到string尾部
                  if(i==(hobbies.size()-1))
                  {
                      sb.append(hobbies.get(i));
                  }else {
                      sb.append(hobbies.get(i)+",");
                  }
              }
                //显示选择结果
                result_tv.setText("你选择了："+sb);
            }
        });
    }

    @override
    public void onCheckedChanged(CompoundButton buttonView, Boolean isChecked)
    {
        if(isChecked){
            hobbies.add(buttonView.getText().toString().trim());
        }else{
            hobbies.remove(buttonView.getText().toString().trim());
        }
    }
}
```



##### RadioButton

​	RadioGroup 为单项选择按钮组，其中可以包含多个 RadioButton，即单选按钮

​	事件监听接口使用的是 RadioGroup.OnCheckedChangeListener()，使用 setOnCheckedChangeListener() 方法将监听器设置到单选按钮上。

```java
package introduction.android.widgetdemo;

import android.app.Activity;
import android.os.Bundle;
import android.widget.RadioButton;
import android.widget.RadioGroup;
import android.widget.TextView;


public class RadioGroupActivity extends Activity {
    private TextView textView;
    private RadioGroup radiogroup;
    private RadioButton radio1,radio2,radio3,radio4;

    @Override
    protected void onCreate(Bundle saveInstanceState) {
        super.onCreate(saveInstanceState);
        this.setContentView(R.layout.radiogroup);
        textView = (TextView) findViewById(R.id.radiohello);
        radiogroup = (RadioGroup)findViewById(R.id.radiogroup1);
        radio1 = (RadioButton) findViewById(R.id.radiobutton1);
        radio2 = (RadioButton) findViewById(R.id.radiobutton2);
        radio3 = (RadioButton) findViewById(R.id.radiobutton3);
        radio4 = (RadioButton) findViewById(R.id.radiobutton4);
        radiogroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(RadioGroup group, int checkedId) {
                String text="我最喜欢运动是";
                if (checkedId == radio1.getId()) {
                    text+=radio1.getText().toString();
                    textView.setText(text);
                } else if(checkedId == radio2.getId()){
                    text+=radio2.getText().toString();
                    textView.setText(text);
                }else if(checkedId == radio3.getId()) {
                    text += radio3.getText().toString();
                    textView.setText(text);
                }else if(checkedId == radio4.getId()) {
                    text += radio4.getText().toString();
                    textView.setText(text);
                }
            }
        });
    }
}
```



##### TextView

程序开发人员可以设置 TextView 的字体大小、颜色、样式等属性。

```java
public void onClick(View v) {
    //TODO Auto-generated method stub
    setTitle("button1 被用户点击了");
    Log.i("widgetDemo", "button1 被用户点击了。");
    TextView textView = (TextView)findViewById(R.id.textView1);
    textView.setText("设置TextView的字体");
    textView.setTextColor(Color.RED);
    textView.setTextSize(TypedValue.COMPLEX_UNIT_SP,20);
    textView.setTypeface(Typeface.defaultFromStyle(Typeface.BOLD));
}
```

- 通过 setText() 方法更改 textView 的显示内容为“设置 TextView 的字体”。
- 通过 setTextColor() 方法修改 textView 显示字体的颜色为红色。
- 通过 setTextSize() 方法修改 textView 显示字体的大小为 20sp。
- 通过 setTypeface() 方法修改 textView 显示字体的风格为加粗。



##### EditText

```java
final EditText editText = (EditText) findViewById(R.id.editText1);
		//设置监听器
        editText.addTextChangedListener(new TextWatcher() {

            @Override
            public void beforeTextChanged(CharSequence charSequence, int start, int count, int after) {

            }
		//文本改变时的函数
            @Override
            public void onTextChanged(CharSequence s, int start, int before, int count) {
                String text = editText.getText().toString();
                textView.setText(text);
            }

            @Override
            public void afterTextChanged(Editable s) {
            }
        });
```



##### Spinner

​	下拉列表

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <TextView
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="textview"/>
    <Spinner
        android:id="@+id/spinner1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
</LinearLayout>
```

```java
package introduction.android.widgetDemo;

import java.util.ArrayList;
import java.util.List;
import android.app.Activity;
import android.os.Bundle;
import android.view.MotionEvent;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Spinner;
import android.widget.TextView;

public class SpinnerActivity extends Activity {

    private List<String> list = new ArrayList<String>();
    private TextView textview;
    private Spinner spinnertext;
    private ArrayAdapter<String> adapter;

    public void onCreate(Bundle savedlnstanceState) {
        super.onCreate(savedlnstanceState);
        setContentView(R.layout.spiner);
        //第一步：定义下拉列表内容
        list.add("A型");
        list.add("B型");
        list.add("O型");
        list.add("AB型");
        list.add("其他");
        textview = (TextView) findViewByld(R.id.textViewl);
        spinnertext = (Spinner) findViewByld(R.id.spinnerl);
        //第二步：为下拉列表定义一个适配器
        adapter = new ArrayAdapter<String>(this, android.R.layout.simple_spinner_item, list);
        //第三步：设置下拉列表下拉时的菜单样式
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        //第四步：将适配器添加到下拉列表上
        spinnertext.setAdapter(adapter);
        //第五步：添加监听器，为下拉列表设置事件的响应
        spinnertext.setOnltemSelectedListener(new Spinner.OnltemSelectedListener() {
            public void onltemSelected(AdapterView<?> argO, View argl, int arg2, long arg3) {
                // TODO Auto-generated method stub
                /* 将所选spinnertext的值带入myTextView中*/
                textview.setText("你的血型是:" + adapter.getItem(arg2));
                /* 将 spinnertext 显示^*/
                argO.setVisibility(View.VISIBLE);
            }

            public void onNothingSelected(AdapterView<?> argO) {
                // TODO Auto-generated method stub
                textview.setText("NONE");
                argO.setVisibility(View.VISIBLE);
            }
        });
        

        //将spinnertext添加到OnTouchListener对内容选项触屏事件处理
        spinnertext.setOnTouchListener(new Spinner.OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
                // TODO Auto-generated method stub
                // 将mySpinner隐藏
                v.setVisibility(View.INVISIBLE);
                Log.i("spinner", "Spinner Touch事件被触发!");
                return false;
            }
        });

        //焦点改变事件处理
        spinnertext.setOnFocusChangeListener(new Spinner.OnFocusChangeListener() {
            public void onFocusChange(View v, boolean hasFocus) {
                // TODO Auto-generated method stub
                v.setVisibility(View.VISIBLE);
                Log.i("spinner", "Spinner FocusChange事件被触发！");
            }
        });

    }
}
```













































































