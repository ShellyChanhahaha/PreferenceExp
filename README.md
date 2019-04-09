# 实验四

## 实验目的

使用PrefereceFragment实现设置页面

## 实验内容

设置四组设置项 

In-line preferences ：

​	CheckBoxPreference 

Dialog-based preferences：	

​	EditTextPreference 

​	ListPreference 

Launch preferences：

​	PreferenceScreen: 跳转到另一个PreferenceScreen 

​	PreferenceScreen: 启动一个网页 

Preference attributes：

​	CheckBox: 父选项 

​	CheckBox: 子选项，当父选项勾选时呈现

## 实验代码

### MainActivity.java

```java
package com.assignment.preferenceexp;

import android.preference.PreferenceActivity;
import android.preference.PreferenceFragment;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends PreferenceActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        getFragmentManager().beginTransaction()
                .replace(android.R.id.content, new PreFragment())
                .commit();
       // addPreferencesFromResource(R.xml.preference);

    }
}
```

### PreFragment.java

```java
package com.assignment.preferenceexp;

import android.os.Bundle;
import android.preference.PreferenceFragment;

public class PreFragment extends PreferenceFragment {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // Load the preferences from an XML resource
        addPreferencesFromResource(R.xml.preference);
    }
}
```

### Preference.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">

    <PreferenceCategory
        android:key="KEY_INLINE"
        android:title="@string/inline">
        <CheckBoxPreference
            android:key="KEY_CHECKBOX"
            android:summary="@string/inline_checkbox_summary"
            android:title="@string/inline_checkbox_title"/>
    </PreferenceCategory>

    <PreferenceCategory
        android:key="KEY_DIALOGBASED"
        android:title="@string/dialogbased_title">
        <EditTextPreference
            android:key="KEY_ANIMAL"
            android:title="@string/edit_text_title"
            android:summary="@string/edit_text_summary"
            android:dialogTitle="@string/animal_summary"/>
        <ListPreference
            android:key="KEY_LIST_PREFERENCE_I"
            android:title="@string/list_preference_title_O"
            android:summary="@string/list_preferenc_summary_O"
            android:dialogTitle="@string/list_preference_title_I"
            android:entries="@array/list_entries"
            android:entryValues="@array/list_entries_value"/>
    </PreferenceCategory>

    <PreferenceCategory
        android:key="KEY_LAUNCH_PREFERENCE_O"
        android:title="@string/launch_preference_O">
        <PreferenceScreen
            android:key="KEY_LAUNCH_PREFERENCE_I"
            android:title="@string/launch_preference_I"
            android:summary="@string/launch_preference_I_summary">
                <CheckBoxPreference
                    android:key="KEY_LAUNCH_PREFERENCE_CHECKBOX"
                    android:title="@string/toggle_preference"
                    android:summary="@string/toggle_preference_summary"/>
        </PreferenceScreen>
        <PreferenceScreen
            android:title="@string/intent_preference_tite"
            android:summary="@string/intent_preference_summary">
            <intent
                android:action="android.intent.action.VIEW"
                android:data="@string/intent_preference_data"/>
        </PreferenceScreen>

    </PreferenceCategory>
    <PreferenceCategory
        android:key="KEY_PREFERENCE_ATTRIBUTE"
        android:title="@string/preference_attribute">
        <CheckBoxPreference
            android:key="KEY_PREFERENCE_ATTRIBUTE_PARENT"
            android:title="@string/preference_attribute_parent_checkbox_title"
            android:summary="@string/preference_attribute_parent_checkbox_summary"/>
        <CheckBoxPreference
            android:key="KEY_PREFERENCE_ATTRIBUTE_CHILD"
            android:title="@string/preference_attribute_child_checkbox_title"
            android:summary="@string/preference_attribute_child_checkbox_summary"
            android:dependency="KEY_PREFERENCE_ATTRIBUTE_PARENT"/>
    </PreferenceCategory>
</PreferenceScreen>
```

## 结果截图

### 整体效果

[![pictureScreenshot_2019-04-09-21-56-48-84.png](https://i.loli.net/2019/04/09/5cacad176dc4c.png)](https://i.loli.net/2019/04/09/5cacad176dc4c.png)

### EditPreference效果

[![pictureScreenshot_2019-04-09-21-57-23-02.png](https://i.loli.net/2019/04/09/5cacad5521da3.png)](https://i.loli.net/2019/04/09/5cacad5521da3.png)

### ListPreference效果

[![pictureScreenshot_2019-04-09-21-57-36-74.png](https://i.loli.net/2019/04/09/5cacad82a99db.png)](https://i.loli.net/2019/04/09/5cacad82a99db.png)

### 跳转至另一个PreferenceScreen

[![pictureScreenshot_2019-04-09-21-57-51-58.png](https://i.loli.net/2019/04/09/5cacada54e38c.png)](https://i.loli.net/2019/04/09/5cacada54e38c.png)

### dependency效果

[![pictureScreenshot_2019-04-09-21-58-01-73.png](https://i.loli.net/2019/04/09/5cacb0ad4d94c.png)](https://i.loli.net/2019/04/09/5cacb0ad4d94c.png)