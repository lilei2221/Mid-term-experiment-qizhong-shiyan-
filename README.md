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
private void insertSampleNotes() {
        // 删除所有现有的笔记，确保每次启动应用都会插入新的样本笔记
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





