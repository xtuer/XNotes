```cpp
// duilib 中将所有的东西都同等对待，所以处理起来非常方便（别说把按钮放到标题栏上，就算把标题栏放在按钮上都没问题）
// CControlUI *option = static_cast<CControlUI*>(m_PaintManager.FindControl(_T("option1")));

#include "stdafx.h"
#include <exdisp.h>
#include <comdef.h>

class CDuiFrameWnd : public CWindowWnd, public INotifyUI {
public:
    virtual LPCTSTR GetWindowClassName() const { return _T("CDuiFrameWnd"); }

    // 重写事件处理函数
    virtual void Notify(TNotifyUI &msg) {
        if (msg.sType == "click") {
            if (msg.pSender->GetName() == "myButton") {
                ::MessageBox(NULL, _T("Hello"), NULL, NULL);
                return;
            }
        }

        WindowImplBase::Notify(msg);
    }

    // 重写事件处理函数
    virtual LRESULT HandleMessage(UINT uMsg, WPARAM wParam, LPARAM lParam) {
        LRESULT result = 0;

        switch (uMsg) {
        case WM_CREATE: result = OnCreate(uMsg, wParam, lParam); break;
        default:;
        }

        if (paintManager.MessageHandler(uMsg, wParam, lParam, result)) {
            return result;
        }

        return CWindowWnd::HandleMessage(uMsg, wParam, lParam);
    }

    // 不同事件处理函数独立到不同的函数中
    LRESULT OnCreate(UINT uMsg, WPARAM wParam, LPARAM lParam) {
        CControlUI *button = new CButtonUI();
        button->SetText(_T("我是一个按钮"));
        button->SetBkColor(0xFFFF0000);

        paintManager.Init(m_hWnd);
        paintManager.AttachDialog(button);

        return 0;
    }

protected:
    CPaintManagerUI paintManager;
};

int APIENTRY WinMain(HINSTANCE hInstance, HINSTANCE /*hPrevInstance*/, LPSTR /*lpCmdLine*/, int nCmdShow) {
    CPaintManagerUI::SetInstance(hInstance);
    CPaintManagerUI::SetResourcePath(CPaintManagerUI::GetInstancePath());   // 设置资源的默认路径（此处设置为和exe在同一目录）

    CDuiFrameWnd duiFrame;
    duiFrame.Create(NULL, _T("DUIWnd"), UI_WNDSTYLE_FRAME, WS_EX_WINDOWEDGE);
    duiFrame.ShowModal();

    return 0;
}

------------------------------------- 相同的功能使用 WindowImplBase 实现 ---------------------------------

class CDuiFrameWnd : public WindowImplBase {
public:
    virtual LPCTSTR    GetWindowClassName() const   {   return _T("DUIMainFrame");  }
    virtual CDuiString GetSkinFile()                {   return _T("duilib.xml");  }
    virtual CDuiString GetSkinFolder()              {   return _T("");  }

    // 重写事件处理函数
    virtual void Notify(TNotifyUI &msg) {
        if (msg.sType == "click") {
            if (msg.pSender->GetName() == "myButton") {
                ::MessageBox(NULL, _T("Hello"), NULL, NULL);
                return;
            }
        }

        WindowImplBase::Notify(msg);
    }
};

int APIENTRY _tWinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPTSTR lpCmdLine, int nCmdShow) {
    CPaintManagerUI::SetInstance(hInstance);

    CDuiFrameWnd duiFrame;
    duiFrame.Create(NULL, _T("DUIWnd"), UI_WNDSTYLE_FRAME, WS_EX_WINDOWEDGE);
    duiFrame.CenterWindow();
    duiFrame.ShowModal();
    return 0;
}
```

```cpp
CControlUI *button = new CButtonUI();
button->SetText(_T("Button"));
button->SetBkColor(0xFF00FF00);

manager.Init(m_hWnd);
manager.AttachDialog(button);

__super::HandleMessage(uMsg, wParam, lParam);

----------------------------------------------------------------------
virtual void Notify(TNotifyUI &msg) {
	if (msg.sType == DUI_MSGTYPE_CLICK && msg.pSender->GetName() == "closeBtn") {
		::MessageBox(NULL, _T("click"), NULL, NULL);
	}
}

<HorizontalLayout /> <!-- 自动占据剩余空间，/ 前少空格就报错 -->
<Default name="Label" value="bkcolor=&quot; #FF888888 &quot;" />

----------------------------------------------------------------------

static_cast<CListUI*>(manager.FindControl("myList"))

virtual void InitWindow() {
	CComboUI *combo = static_cast<CComboUI*>(m_PaintManager.FindControl("combo"));

	if (combo) {
		// Combo
		for (int i = 0; i < 10; ++i) {
			CListLabelElementUI *item = new CListLabelElementUI();
			item->SetText("One");
			item->SetUserData(CDuiString("你好啊 http://www.qtdebug.com"));
			combo->Add(item);
		}
	}
}

CDuiString senderName = msg.pSender->GetName();

if (msg.sType == DUI_MSGTYPE_CLICK && senderName == "helloButton") {
	// Combo
	CComboUI *combo = static_cast<CComboUI*>(m_PaintManager.FindControl("combo"));
	combo->NeedUpdate();

	CListLabelElementUI *item = static_cast<CListLabelElementUI*>(combo->GetItemAt(combo->GetCurSel()));
	CDuiString text;
	text.Format("%d - %s", combo->GetCurSel(), item->GetUserData());

	::MessageBox(NULL, text, NULL, NULL);
}
```



