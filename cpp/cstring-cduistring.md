## 使用 CString

MFC 中，使用 CString 需要包含头文件 `#include <atlstr.h>`

## UTF-8 to CString

```cpp
/**
 * 把 UTF-8 的字符串的字节数组转为 CString.
 *
 * @param utf8 UTF-8 的字节数组
 * @param ok   转换成功时为 TRUE，失败时为 FALSE
 * @return 返回 UTF-8 的字符串对应的 CString
 */
CString CStringFromUtf8(const char *utf8, BOOL *ok = NULL) {
    CString result;

    if (NULL != ok) { *ok = TRUE; }

    if (NULL == utf8) {
        if (NULL != ok) { *ok = FALSE; }
        return result;
    }

    int unicodeLen = ::MultiByteToWideChar(CP_UTF8, 0, utf8, -1, NULL, 0);
    wchar_t *unicode = new wchar_t[unicodeLen + 1];

    ::MultiByteToWideChar(CP_UTF8, 0, utf8, -1, (LPWSTR)unicode, unicodeLen);
    result = unicode;

    delete[] unicode;
    return result;
}
```

## UTF-8 to CDuiString

```cpp
/**
* 把 UTF-8 的字符串的字节数组转为 CDuiString.
*
* @param utf8 UTF-8 的字节数组
* @param ok   转换成功时为 TRUE，失败时为 FALSE
* @return 返回 UTF-8 的字符串对应的 CDuiString
*/
CDuiString CDuiStringFromUtf8(const char *utf8, BOOL *ok = NULL) {
    CDuiString result;

    if (NULL != ok) { *ok = TRUE; }

    if (NULL == utf8) {
        if (NULL != ok) { *ok = FALSE; }
        return result;
    }

    int unicodeLen = ::MultiByteToWideChar(CP_UTF8, 0, utf8, -1, NULL, 0);
    wchar_t *unicode = new wchar_t[unicodeLen + 1];

    ::MultiByteToWideChar(CP_UTF8, 0, utf8, -1, (LPWSTR)unicode, unicodeLen);
    result = unicode;

    delete[] unicode;
    return result;
}
```

> CString 可以直接构造 CDuiString: `CDuiString st1 = CString("Hello")`



