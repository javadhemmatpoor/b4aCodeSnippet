# Change Color StatusBar And NavigationBar

* function ChangeColor:

```vb
Public Sub ChangeColor(color As Int)
    ' تغییر رنگ استاتوس بار و نویگیشن بار باهم
    Dim p As Phone
    If p.SdkVersion >= 21 Then
        NavigationBarColor(color)
        StatusBarColor(color)
    End If
End Sub

' تابع تغییر رنگ نویگیشن پایین
Public Sub NavigationBarColor(color As Int)
    Dim jo As JavaObject
    jo.InitializeContext
    Dim window As JavaObject = jo.RunMethodJO("getWindow", Null)
    window.RunMethod("addFlags", Array (0x80000000))
    window.RunMethod("clearFlags", Array (0x04000000))
    window.RunMethod("setNavigationBarColor", Array(color))
End Sub

'  تابع تغییر رنگ نوار وضعیت بالا
Public Sub StatusBarColor(color As Int)
    Dim jo As JavaObject
    jo.InitializeContext
    Dim window As JavaObject = jo.RunMethodJO("getWindow", Null)
    window.RunMethod("addFlags", Array (0x80000000))
    window.RunMethod("clearFlags", Array (0x04000000))
    window.RunMethod("setStatusBarColor", Array(color))
        
    Dim view As JavaObject = window.RunMethodJO("getDecorView",Null)

    'Light style with black icons and text
    ' حالت لایت نوشته ها مشکی
    view.RunMethod("setSystemUiVisibility",Array(Bit.Or(0x00002000,view.RunMethod("getSystemUiVisibility",Null)))) 
    ' حالت دارک نوشته ها سفید
    '  view.RunMethod("setSystemUiVisibility",Array(0)) 'Dark style with White icons and text
End Sub

Sub color_status
    ChangeColor(Colors.RGB(255,255,255))
End Sub
```

* use just one Activity:

```vb
ChangeColor(Colors.RGB(255,255,255))
```

* use all Activity:

```vb
color_status
```

[hp](http://hemmatpoor.ir)
