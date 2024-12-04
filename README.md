android期中实验：

基本功能：

1.NoteList界面中笔记条目增加时间戳显示

2.查询功能

扩展功能：

3.设置背景

4.笔记排序

笔记时间戳和笔记查询功能：

![image](https://github.com/user-attachments/assets/dfc2b321-2cf2-457b-bc4a-9d7c62dc9fa3)

![image](https://github.com/user-attachments/assets/67c5e6e4-8184-4edf-8aa9-20599a6564f6)

![image](https://github.com/user-attachments/assets/a4c0b78a-5c75-4f55-b432-b53300c731ea)

![image](https://github.com/user-attachments/assets/c0a9dc46-5d29-44d4-8d4a-ee5aa138644a)

设置背景：

![image](https://github.com/user-attachments/assets/74ca6502-35bb-40a2-9a79-82dd1ba23868)

![image](https://github.com/user-attachments/assets/57267d7c-f3a1-496e-abc7-04788a1928e0)

![image](https://github.com/user-attachments/assets/96507cad-b906-4b6e-ab01-0e4a33b3ef58)
（这里已经修改完背景）

笔记排序：

按照时间排序：

![image](https://github.com/user-attachments/assets/78a7da23-dae6-4f15-8398-a43f3e491b02)

按颜色排序（根据颜色的整数值来进行排序。颜色在代码中通常表示为 ARGB（Alpha, Red, Green, Blue）格式的整数值，因此可以按数值大小排序）：

![image](https://github.com/user-attachments/assets/a46aaecc-fe11-44bb-a242-dabb99261984)

笔记颜色代码：

```
private void insertSampleNotes() {
        
        getContentResolver().delete(NotePad.Notes.CONTENT_URI, null, null);

        ContentValues values = new ContentValues();
        long currentTime = System.currentTimeMillis();

        // Sample Note 1
        values.put(NotePad.Notes.COLUMN_NAME_TITLE, "Sample Note 1");
        values.put(NotePad.Notes.COLUMN_NAME_NOTE, "This is the first sample note.");
        values.put(NotePad.Notes.COLUMN_NAME_CREATE_DATE, currentTime);
        values.put(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR, Color.YELLOW);
        getContentResolver().insert(NotePad.Notes.CONTENT_URI, values);

        // Sample Note 2
        values.clear();
        values.put(NotePad.Notes.COLUMN_NAME_TITLE, "Sample Note 2");
        values.put(NotePad.Notes.COLUMN_NAME_NOTE, "This is the second sample note.");
        values.put(NotePad.Notes.COLUMN_NAME_CREATE_DATE, currentTime + 1000); // 1 second later
        values.put(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR, Color.LTGRAY);
        getContentResolver().insert(NotePad.Notes.CONTENT_URI, values);

        // Sample Note 3
        values.clear();
        values.put(NotePad.Notes.COLUMN_NAME_TITLE, "Sample Note 3");
        values.put(NotePad.Notes.COLUMN_NAME_NOTE, "This is the third sample note.");
        values.put(NotePad.Notes.COLUMN_NAME_CREATE_DATE, currentTime + 2000); // 2 seconds later
        values.put(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR, Color.GREEN);
        getContentResolver().insert(NotePad.Notes.CONTENT_URI, values);

        // Sample Note 4
        values.clear();
        values.put(NotePad.Notes.COLUMN_NAME_TITLE, "Sample Note 4");
        values.put(NotePad.Notes.COLUMN_NAME_NOTE, "This is the fourth sample note.");
        values.put(NotePad.Notes.COLUMN_NAME_CREATE_DATE, currentTime + 3000); // 3 seconds later
        values.put(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR, Color.CYAN);
        getContentResolver().insert(NotePad.Notes.CONTENT_URI, values);

        // Sample Note 5
        values.clear();
        values.put(NotePad.Notes.COLUMN_NAME_TITLE, "Sample Note 5");
        values.put(NotePad.Notes.COLUMN_NAME_NOTE, "This is the fifth sample note.");
        values.put(NotePad.Notes.COLUMN_NAME_CREATE_DATE, currentTime + 4000); // 4 seconds later
        values.put(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR, Color.MAGENTA);
        getContentResolver().insert(NotePad.Notes.CONTENT_URI, values);

        // Sample Note 6
        values.clear();
        values.put(NotePad.Notes.COLUMN_NAME_TITLE, "Sample Note 6");
        values.put(NotePad.Notes.COLUMN_NAME_NOTE, "This is the sixth sample note.");
        values.put(NotePad.Notes.COLUMN_NAME_CREATE_DATE, currentTime + 5000); // 5 seconds later
        values.put(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR, Color.BLUE);
        getContentResolver().insert(NotePad.Notes.CONTENT_URI, values);
    }
```

基本功能

1. NoteList界面中笔记条目增加时间戳显示
 
1.1 添加目的

在 NoteList 界面上，增加每条笔记的时间戳显示，用来展示每条笔记的最后修改时间。这是为了提升用户体验，让用户可以清晰地查看每条笔记的修改日期。

1.2 修改查询字段，增加时间戳列

在 NotesList.java 中，修改 PROJECTION 数组，增加时间戳字段 COLUMN_NAME_MODIFICATION_DATE：

```
private static final String[] PROJECTION = new String[] {
    NotePad.Notes._ID, // 0
    NotePad.Notes.COLUMN_NAME_TITLE, // 1
    NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE // 2 - 新增时间戳字段
};
```

1.3 修改布局文件，增加时间戳 TextView

在 res/layout/noteslist_item.xml 文件中，新增一个 TextView 用于显示时间戳。该 TextView 显示在笔记标题下方，以较小字体显示时间，避免干扰主标题内容。

```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="5dp">

    <!-- 原来的标题 TextView -->
    <TextView
        android:id="@android:id/text1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textAppearance="?android:attr/textAppearanceLarge"
        android:gravity="center_vertical"
        android:singleLine="true" />

    <!-- 新增的时间戳 TextView -->
    <TextView
        android:id="@+id/note_timestamp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="12sp"
        android:textColor="#808080"
        android:gravity="center_vertical"
        android:paddingTop="2dp" />
</LinearLayout>
```

1.4 更新适配器，绑定时间戳字段到 TextView

在 NotesList.java 的 onCreate() 方法中，修改 SimpleCursorAdapter，将时间戳字段绑定到布局中的 TextView。

```
String[] dataColumns = {
    NotePad.Notes.COLUMN_NAME_TITLE, 
    NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE  // 新增时间戳字段
};

int[] viewIDs = {
    android.R.id.text1, 
    R.id.note_timestamp  // 绑定到布局中的时间戳 TextView
};

SimpleCursorAdapter adapter = new SimpleCursorAdapter(
    this,                     // Context
    R.layout.noteslist_item,  // 指定列表项的布局文件
    cursor,                   // 数据来源
    dataColumns,
    viewIDs
);
setListAdapter(adapter);
```

1.5 格式化时间戳为可读的日期格式

通过 SimpleDateFormat 对时间戳进行格式化，使其成为用户友好的日期格式，设置时区为中国北京时间（Asia/Shanghai）。

```
adapter.setViewBinder(new SimpleCursorAdapter.ViewBinder() {
    @Override
    public boolean setViewValue(View view, Cursor cursor, int columnIndex) {
        if (view.getId() == R.id.note_timestamp) {
            // 获取时间戳
            long timestamp = cursor.getLong(columnIndex);

            // 创建日期格式化对象，并设置为中国北京时间（Asia/Shanghai 时区）
            SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm");
            dateFormat.setTimeZone(TimeZone.getTimeZone("Asia/Shanghai"));

            // 将时间戳转换为北京时间
            String date = dateFormat.format(new Date(timestamp));
            ((TextView) view).setText(date);
            return true;  // 我们处理了这个绑定
        }
        return false;  // 其他字段交由默认绑定处理
    }
});
```

1.6 更新数据库插入和更新逻辑

确保在笔记插入和更新时，COLUMN_NAME_MODIFICATION_DATE 字段会被正确地设置为当前时间。

```
// 在 NotePadProvider.java 中的 insert 方法中
if (!values.containsKey(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE)) {
    values.put(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, System.currentTimeMillis());
}

// 在 update 方法中，将修改日期更新为当前时间
values.put(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, System.currentTimeMillis());
```

1.7 结果：

通过这些步骤，NotesList 界面上每个笔记项下方都会显示其最后修改时间，格式为“年-月-日 时:分”，并且显示时区为中国北京时间（Asia/Shanghai）。

2. 查询功能
   
2.1 添加目的

为用户提供快速查询笔记的功能，通过 SearchView 组件允许用户输入关键字，查询数据库中的笔记。查询条件为笔记的标题和内容包含用户输入的关键字。

2.2 在界面中添加 SearchView 组件

在 NotesList.java 的 onCreate() 方法中，动态创建 SearchView 并添加到界面顶部。

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    // 获取 ListView
    ListView listView = getListView();

    // 创建 SearchView
    SearchView searchView = new SearchView(this);
    searchView.setLayoutParams(new ListView.LayoutParams(
            ListView.LayoutParams.MATCH_PARENT,
            ListView.LayoutParams.WRAP_CONTENT
    ));
    searchView.setQueryHint("搜索笔记标题或内容");

    // 将 SearchView 添加到 ListView 的 Header
    listView.addHeaderView(searchView);

    // 设置查询监听器
    searchView.setOnQueryTextListener(new SearchView.OnQueryTextListener() {
        @Override
        public boolean onQueryTextSubmit(String query) {
            searchNotes(query);  // 执行查询
            return true;
        }

        @Override
        public boolean onQueryTextChange(String newText) {
            searchNotes(newText);  // 动态查询
            return true;
        }
    });
}
```

2.3 实现 searchNotes 方法

在 NotesList.java 中添加 searchNotes 方法，通过 ContentResolver.query() 查询笔记标题和内容，更新列表显示。

```
private void searchNotes(String query) {
    // 定义查询条件，搜索标题或内容中包含关键字的笔记
    String selection = NotePad.Notes.COLUMN_NAME_TITLE + " LIKE ? OR " +
                       NotePad.Notes.COLUMN_NAME_NOTE + " LIKE ?";
    String[] selectionArgs = new String[]{"%" + query + "%", "%" + query + "%"};

    // 执行查询
    Cursor cursor = getContentResolver().query(
            NotePad.Notes.CONTENT_URI,       // 查询 URI
            PROJECTION,                      // 返回的列
            selection,                       // 查询条件
            selectionArgs,                   // 查询参数
            NotePad.Notes.DEFAULT_SORT_ORDER // 排序
    );

    // 更新适配器的数据
    ((SimpleCursorAdapter) getListAdapter()).changeCursor(cursor);
}
```

2.4 结果：

通过这些操作，用户可以在 SearchView 中输入关键字，实时查询笔记的标题或内容。查询结果会根据输入实时更新，提供高效的搜索体验。

扩展功能

3. 设置背景

3.1 添加目的
用户能够自定义笔记背景色，以提高视觉效果和个性化设置。我们为每个笔记添加背景设置功能。

3.2 设置背景颜色

在 NotePadProvider.java 中，确保插入和更新笔记时支持 background_color 字段的设置。

// 在 NotePadProvider.java 中的 insert 方法中


if (!values.containsKey(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR)) {

    values.put(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR, Color.WHITE); // 默认背景色
    
}

// 在 update 方法中设置背景色

values.put(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR, newColor);


3.3 修改布局文件，支持动态背景设置

在 noteslist_item.xml 中，使用动态设置背景颜色来修改笔记项的背景。



int backgroundColor = cursor.getInt(cursor.getColumnIndex(NotePad.Notes.COLUMN_NAME_BACKGROUND_COLOR));

view.setBackgroundColor(backgroundColor);



3.4 结果：
用户能够动态设置和更新笔记的背景颜色，界面展示会实时反映用户的个性化设置。

4. 笔记排序
   
4.1 添加目的

支持笔记列表的排序功能，包括按时间、按内容大小等排序方式，允许用户更方便地查看笔记。

4.2 排序按钮和功能实现

通过按钮切换排序方式，在 NotesList 中添加按时间或按内容大小排序的功能。


sortBySizeButton.setOnClickListener(new View.OnClickListener() {

    @Override
    
    public void onClick(View v) {
    
        toggleSortOrder(); // 切换排序方式
        
    }
    
});


private void toggleSortOrder() {

    if (isSortedByContentSize) {
    
        loadNotes(NotePad.Notes.DEFAULT_SORT_ORDER); // 默认按时间排序
        
        sortBySizeButton.setText("按内容大小排序"); // 更新按钮文本
        
    } else {
    
        loadNotes("LENGTH(" + NotePad.Notes.COLUMN_NAME_NOTE + ") ASC"); // 按内容大小排序
        
        sortBySizeButton.setText("按时间排序"); // 更新按钮文本
        
    }
    
    isSortedByContentSize = !isSortedByContentSize; // 切换排序状态
    
}

4.3 结果：

用户可以通过按钮切换排序方式，实时查看按时间或内容大小排序的笔记列表，增强了列表的可操作性。




