# Build Feather Browser on a Windows build server

This package includes a GitHub Actions workflow. It builds on Microsoft's hosted Windows Server 2022 runner and uploads `FeatherBrowser.exe` as an artifact. You do not need Visual Studio installed on your own PC.

## Steps

1. Sign in to GitHub and create a **new private repository** (for example, `FeatherBrowser`).
2. Extract this ZIP on your PC.
3. Upload the extracted files and folders to the repository's `main` branch. Make sure `.github/workflows/windows-build.yml` is included. If the `.github` folder is hidden by your file manager, enable hidden items.
4. Open the repository on GitHub and click **Actions**.
5. Select **Build Feather Browser (Windows x64)**, click **Run workflow**, then **Run workflow** again.
6. Open the running workflow. If it succeeds, scroll to **Artifacts** and download `FeatherBrowser-Windows-x64`.
7. Extract the artifact ZIP to get `FeatherBrowser.exe`.

The workflow downloads the WebView2 SDK and builds the app. The target PC still needs the Microsoft Edge WebView2 Runtime installed. The hosted build can reveal further C++ errors; if it fails, open the run and read the first compiler error in the **Build Release x64** step.

## Honest status

This is a build workflow, not a prebuilt or verified executable. The code has not been compiled in this environment. The workflow must complete successfully before an EXE is available.
