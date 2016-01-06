# NsRefreshLayout 
֧������View������ˢ�¿ؼ���ͬʱ֧������ˢ�¡�

## Ч��Ԥ��

![demo](https://github.com/xiaolifan/NsRefreshLayout/blob/master/art/demo.gif?raw=true)

## ����˵��

```xml
<declare-styleable name="NsRefreshLayout">
    <!--Loading��ͼ������ɫ-->
    <attr name="load_view_bg_color" format="color|reference"/>
    <!--��������ɫ-->
    <attr name="progress_bar_color" format="color|reference"/>
    <!--����������ɫ-->
    <attr name="progress_bg_color" format="color|reference"/>
    <!--Loading��ͼ��������ɫ-->
    <attr name="load_text_color" format="color|reference"/>
    <!--����ˢ����������-->
    <attr name="pull_refresh_text" format="string|reference"/>
    <!--����������������-->
    <attr name="pull_load_text" format="string|reference"/>
    <!--�Ƿ��Զ��������ظ���-->
    <attr name="auto_load_more" format="boolean"/>
    <!--����ˢ���Ƿ����-->
    <attr name="pull_refresh_enable" format="boolean"/>
    <!--���������Ƿ����-->
    <attr name="pull_load_enable" format="boolean"/>
</declare-styleable>
```

## ����

```xml
<?xml version="1.0" encoding="utf-8"?>
<com.xlf.nrl.NsRefreshLayout
    android:id="@+id/nrl_test"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:auto_load_more="false"
    tools:context="com.xlf.nrl.demo.MainActivity">

    <android.support.v7.widget.RecyclerView
        android:id="@+id/rv_test"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layoutManager="LinearLayoutManager"
        tools:listitem="@layout/item_test"/>
</com.xlf.nrl.NsRefreshLayout>
```

```java
package com.xlf.nrl.demo;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.RecyclerView;
import android.view.Menu;
import android.view.MenuItem;

import com.xlf.nrl.NsRefreshLayout;

public class MainActivity extends AppCompatActivity implements
        NsRefreshLayout.NsRefreshLayoutController, NsRefreshLayout.NsRefreshLayoutListener {

    private boolean loadMoreEnable = true;
    private NsRefreshLayout refreshLayout;
    private RecyclerView rvTest;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        refreshLayout = (NsRefreshLayout) findViewById(R.id.nrl_test);
        refreshLayout.setRefreshLayoutController(this);
        refreshLayout.setRefreshLayoutListener(this);

        rvTest = (RecyclerView) findViewById(R.id.rv_test);
        TestRecyclerAdapter adapter = new TestRecyclerAdapter(this);
        rvTest.setAdapter(adapter);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        MenuItem item = menu.add(0, 0, 0, "�����������ع���");
        item.setShowAsAction(MenuItem.SHOW_AS_ACTION_ALWAYS);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        loadMoreEnable = false;
        return true;
    }

    @Override
    public boolean isPullRefreshEnable() {
        return true;
    }

    @Override
    public boolean isPullLoadEnable() {
        return loadMoreEnable;
    }

    @Override
    public void onRefresh() {
        refreshLayout.postDelayed(new Runnable() {
            @Override
            public void run() {
                refreshLayout.finishPullRefresh();
            }
        }, 1000);
    }

    @Override
    public void onLoadMore() {
        refreshLayout.postDelayed(new Runnable() {
            @Override
            public void run() {
                refreshLayout.finishPullLoad();
            }
        }, 1000);
    }

}
```

## License
-------

    Mozilla Public License, version 2.0
