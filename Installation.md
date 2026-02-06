# Overview
> In this article, we will cover installing Severe, and the most common issues users face in the process.
# Requirements
- **Windows 10/11:** note that some prehistoric/new versions of **Windows 11** might not work, in that case, you should wait for it to be officially supported by **Severe** or downgrade your version. We also don't promise tweaked redistributions of Windows to work out of the box, few that have been tested are: **Atlas**, and **XOS**.
- **Internet Connection**
- **Turned off anti-virus:** both Windows Defender, and user-installed anti-viruses can interfere with **Severe**. We recommend using [**Winaero Tweaker**](https://winaerotweaker.com/) or [**Defender Control**][https://github.com/pgkt04/defender-control]
## Redistributes
This is needed to be installed **before** Severe for smoother experience, and also to fix some of the problems (for example: the overlay not showing up).
- [DirectX End-User Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=8109)
- [.NET SDK](https://dotnet.microsoft.com/en-us/download)
- [Visual C++ Runtime](https://www.techpowerup.com/download/visual-c-redistributable-runtime-package-all-in-one/)
# Downloading
Install **severe.rar** from the `#downloads` channel on the official Discord server, afterwards continue by **extracting**, and **running the upgrade.exe** file.

After, you should see a new file in the same folder as **upgrade.exe** called **software.exe**, this is your primary executable that **you should be running to launch Severe.**

Run **software.exe**, and ideally, after a bit of waiting, you should see an overlay on **Roblox** asking you to either **log-in** or **register**. If you're a first time user, please continue with registering, a few key details however:
- **Note down your username and password:** this is critical to ensure that your account won't get lost.
- **Avoid special characters:** spaces, symbols should be avoided at all cost, please use an alphanumeric password consisting of letters **A-Z**, and **0-9** numbers.
# Issues
## HWID Mismatch
We utilize **HWID** to provide a secure connection from your machine to our servers, changing a part in your PC can sometimes cause this to change.
In this case, please navigate to our [Keyauth Page](https://keyauth.cc/panel/SHELUV_PERKS/v-severe) and press **"Reset HWID"**.
## Executable not opening
This is a frequent issue with custom file explorers, please use the native file explorer or utilize the command prompt to open the file.
## Loading Loop / Bad Post Code
Incase **Severe** is stuck whilst loading, the most frequent resolution is disabling your anti-virus software, such as **Malwarebytes**, or **Avast**. In some cases, your password/username can be an issue, for example having a special character in your password.
## GLFW Error
Reopen Roblox.
## D3DCompiler_43.dll
Download this [file](https://www.dll-files.com/download/0c20f567e2e586f6bcf3f0ce3ae64aab/d3dcompiler_43.dll.html?c=Yko1VjlUSWd4WFJaZ2w5OG1hQjFVQT09) and move it into `C:/Windows/System32`.
## HTTPs Verification Failed
Use [**Cloudflare's 1.1.1.1**](https://one.one.one.one/) or a VPN.
## This app can't run on your PC
Disable all anti-viruses, redownload **Severe** and run **upgrade.exe**.
## Hosts
First, download [this file](https://pixeldrain.com/u/jWJfBB3Q), afterwards, move it to `C:/Windows/System32/Drivers/etc`.
## Don't see your issue?
Contact support via the official **Discord server**, and please, remain patient. In edge cases, where a new-user can't get their **Severe** working, and has registered an account before, a refund can be negotiated.