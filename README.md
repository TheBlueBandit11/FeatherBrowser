# Feather Browser

A compact native Win32 C++20 browser shell for Windows 10/11, backed by the system's Microsoft Edge WebView2 Evergreen Runtime.

## Build

1. Install Visual Studio 2022 and select **Desktop development with C++** plus a Windows 10/11 SDK.
2. Install the **Microsoft Edge WebView2 Runtime** if it is not already installed: https://developer.microsoft.com/microsoft-edge/webview2/
3. Open `FeatherBrowser.vcxproj` in Visual Studio 2022. Allow NuGet package restore.
4. Select `x64` and `Release`, then Build > Build Solution.
5. Run `bin\Release\FeatherBrowser.exe` (or press Ctrl+F5 from Visual Studio).

The project uses the NuGet WebView2 SDK and links its static loader. The runtime itself is not bundled, keeping the app package small and letting Microsoft ship security updates.

## Controls

- Address bar + Enter: navigate or search
- Ctrl+L: focus address bar
- Ctrl+T: new tab
- Ctrl+W: close current tab
- Back / Forward / Reload / Home: navigation
- Star: save current page as a bookmark
- Star-list: open the most recently saved bookmark (the dialog lists saved bookmarks)
- Download arrow: open the downloads folder
- Half-circle: toggle the basic dark/light control palette

Data is stored in `%LOCALAPPDATA%\FeatherBrowser`. Downloads go to its `Downloads` subfolder.

## Troubleshooting

- If Visual Studio reports `WebView2.h` missing, right-click the solution and choose **Restore NuGet Packages**, then confirm the `Microsoft.Web.WebView2` package is installed for this project.
- The source uses the WebView2 `DocumentTitleChanged` event with `IUnknown*` event arguments, as required by the SDK.
- Windows API declarations for `ShellExecuteW` are provided by `<shellapi.h>`.
- Unicode and `WIN32_LEAN_AND_MEAN` definitions are set in the project configuration, not repeated in the source.

## Important limitations

This is a compact browser shell, not a new browser engine. WebView2 uses Chromium's multi-process architecture, and RAM usage depends heavily on websites, their scripts, and the number of live tabs. A single executable does not mean a single process. The Evergreen runtime is shared with other apps and is kept updated for security.

The current privacy protection is deliberately conservative: no browser telemetry, accounts, feeds, or custom background polling are added. A full, maintained tracker-blocking engine is not included; implementing one responsibly requires a regularly updated filter list and robust request-filtering tests. The browser currently does not claim to block all trackers. Inactive tabs are hidden but not automatically suspended yet, to avoid breaking audio, downloads, and page state. This project should be built and tested on Windows; it has not been compiled or benchmarked in this Linux authoring environment, so no build-success or performance numbers are claimed.
