---
search:
  keyword:
    - gamepot
---

#### **We provide the <a href="https://guide.ncloud-docs.com/docs/en/home" target="_blank">[Manual]</a>and <a href="https://api.ncloud-docs.com/docs/en/home" target="_blank">[API Reference]</a>separately to offer more detailed information on how to use the NAVER CLOUD PLATFORM and help maximize the use of the API.**

<a href="https://api.ncloud-docs.com/docs/en/game-gamepot" target="_blank">Go to Gamepot API Reference >></a><br />
<a href="https://guide.ncloud-docs.com/docs/en/game-gamepot-overview" target="_blank">Go to Gamepot Manual >></a>

# GamePot Tools - Beta

> ### This is a machine-translated document that may have errors in vocabulary, syntax, or grammar. We will soon provide you with the document translated by a professional translator.
>
> #### If you have any questions, please [contact us](https://www.ncloud.com/support/question).
>
> We will make every effort to further enhance our services.

This is a guide to GamePot Tools provided by GAMEPOT of NAVER CLOUD PLATFORM.

## Introduction to GAMEPOT Tools

**Q. What is Gamepot Tools?**

Package dependency issues that can occur during game development through the Unity engine can be identified and managed at a glance.
This is a management tool provided by GamePod SDK.

In addition to the existing library modules provided by the IMPT SDK, you can manage various third-party libraries with one click.

You can diagnose and resolve the package dependency status for each platform and module.

## 1. Getting Started

### Step 1. Get GamePot Tools plugin

Connect to the created GAMEPOT dashboard and download the latest plugin.
<br>
**Other> Download SDK> Unity> Download GamePot Tools**

### Step 2. Import plugin

> Unity version 2017.4.x or higher.

Select the downloaded `GamePotTools_xxxx.unitypackage` file from **Assets> Import Package> Custom Package** menu.

![gamepot_unitools_01](./images/gamepot_unitools_01.png)

Check the plugin and import it to add it to the project.

![gamepot_unitools_02](./images/gamepot_unitools_02.png)

### Step 3. Android/iOS

In the case of GamePot Tools, since it requires a namespace for each platform, it works normally with the Android/iOS build environment set. Please check if **File> Build Settings> Android/iOS** modules are all downloaded in Unity Editor.

![gamepot_unitools_03](./images/gamepot_unitools_03.png)

## 2. Using

![gamepot_unitools_04](./images/gamepot_unitools_04.png)

You can launch GamePot Tools by clicking the **Window> GamePot Tools** tab.

![gamepot_unitools_05](./images/gamepot_unitools_05.png)

① Check the version of GamePot Tools and execute the update when the latest version is updated.

② You can check the gamepot guide on the web page.

③ You can check the Naver Cloud Platform Guide on the web page.

④ Download GamePot Sdk with minimum module configured.

### Android Fingerprint Tool

Various fingerprints are acquired from the KetStore set in the current project.

![gamepot_unitools_06](./images/gamepot_unitools_06.png)

Click the **Key tool** button.

> Unity platform setting should be changed to Android.

![gamepot_unitools_07](./images/gamepot_unitools_07.png)

① Check the KeyStore information set in the current project's PlayerSetting.

② Acquire the Sha1 fingerprint.

③ Obtain the Base64 hash.

④ Enter the path to the APK file and obtain the hash.

⑤ Move to Android studio installation page.

⑥ Move to JDK download page.

⑦ It moves to the local storage where the deleted package is saved through the Install function.

⑧ Move to the local storage where the cache data is stored.

### Gamepot Settings Tool

It manages various settings of GamePot.

![gamepot_unitools_08](./images/gamepot_unitools_08.png)

#### Android

Set up the Gamepot project environment for Android Bulid.
It is reflected in `Android> mainTemplate.gradle`.

![gamepot_unitools_09](./images/gamepot_unitools_09.png)

#### IOS

Gamepot project environment for IOS Bulid.
It is reflected in `IOS> GamePotConfig-info.plist`.

![gamepot_unitools_10](./images/gamepot_unitools_10.png)

### Module Installation

Manage platform-specific modules and libraries.

![gamepot_unitools_11](./images/gamepot_unitools_11.png)

① Platform can be selected. (Android / iOS)

② You can select the module you want to configure in the project. For modules that are already configured, they remain active.

③ You can check the dependency package list for the module and check the status in the project.

④ For the selected module list, configure the required dependency package.

#### Install Package

- Since there is no corresponding package in the project, download it from the CDN server.

![gamepot_unitools_14](./images/gamepot_unitools_14.png)

- Duplicate package exists. Only the recommended version of the package is left, and the rest are deleted.

![gamepot_unitools_15](./images/gamepot_unitools_15.png)

- The latest version of the package is installed. Stay current.
  <br>If you click the'Selected' button again to deselect it, you can delete the existing package and download it again from the CDN server.

![gamepot_unitools_16](./images/gamepot_unitools_16.png)

When you click the install button, package resolving will start.

![gamepot_unitools_12](./images/gamepot_unitools_12.png)

### Change language

The language of GamePot Tools will be changed to the language of your choice. English, Korean, Japanese and Chinese are supported.

![gamepot_unitools_13](./images/gamepot_unitools_13.png)
