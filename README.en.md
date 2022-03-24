<div align="center">
<h1>JsHook</h1>

[![Xposed](https://img.shields.io/badge/-Xposed-3DDC84?style=flat&logo=Android&logoColor=white)](#)
[![GitHub release](https://img.shields.io/github/release/Xposed-Modules-Repo/me.jsonet.jshook.svg)](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/releases/latest)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Channel&color=0088cc)](https://t.me/jshookapp)
[![Telegram](https://img.shields.io/static/v1?label=Telegram&message=Chat&color=0088cc)](https://t.me/jshookgroup)
[![LSPosed Downloads](https://img.shields.io/github/downloads/Xposed-Modules-Repo/me.jsonet.jshook/total?label=LSPosed%20Downloads&logo=Android&labelColor=F48FB1&logoColor=ffffff&color=0088cc)](https://modules.lsposed.org/module/me.jsonet.jshook)

hook artifact in android support java layer and native layer

[中文的README](https://github.com/Xposed-Modules-Repo/me.jsonet.jshook/blob/main/README.md)
</div>

## About the module

Xposed is a module framework that can change the behavior of your system and applications without touching any APK. This means that modules can work on different versions and even ROMs without any changes.

JsHook is the use of Xposed framework for the initialization of any app to inject Rhino/Frida, Xposed module development requires a certain Java syntax base, the technical threshold is high, while JsHook injected Rhino/Frida is great, only need to know a short Js syntax base, you can use the phone to quickly make their own hook plug-ins, and hook support java layer and native layer.

## Module compatibility

1. Xposed api 82
2. Android 7 - 12

## How to use the module

### How to enable scripts

Before enabling the script, please make sure the selected application has enabled the hook service option, if it is LSPosed non-global scope in addition to check the system when activating the module also need to check the corresponding script effective application, each time you change the script content need to restart the app being hooked.

### How to choose an hook framework

If you are familiar with Xposed hook method, Rhino is recommended, using js call Xposed framework methods, and high compatibility; and Frida belongs to another hook framework, need to have some understanding of Frida, it is difficult to get started, and does not support some models and apps.

## Cautions

Version 1.0.2 before the default is rhino hook, so the previous use of frida need to use the framework management will be set to frida global default , import framework currently only supports frida-gadget.

## Script Description

### Universal

Log Printing：

```js
common.log('...');
```

Message Tips：

```js
common.toast('...');
```

Get Context：

```js
common.getcontext();
```

### rhino

hook constructor

```js
common.hookAllConstructors('com.test.test', function (param) {
    //Before the execution of the constructor
    //Print the first argument received by the constructor
    common.log(param.args[0]);
    //Modify the value of this parameter
    param.args[0] = 'fuck';
}, function (param) {
    //After the execution of the constructor
    //...
});
```

hook constructor with specified parameters

```js
common.hookConstructor('com.test.test', ['java.lang.String', 'int'], function (param) {
    //...
}, function (param) {
    //...
});
```

hook class method

```js
common.hookAllMethods('com.test.test', function (param) {
    //...
}, function (param) {
    //...
});
```

hook the class method with the specified parameters

```js
common.hookMethod('com.test.test', ['java.lang.String', 'int'], function (param) {
    //...
    //Modify return value
    param.setResult('fuck');
}, function (param) {
    //...
    //Get the return value of the class method and print it
    common.log(param.getResult());
});
```

Modifying static variable values

```js
common.setStaticObjectField('com.test.test', 'Variable Name', 'Variable Value');
```

Modifying dynamic variable values

```js
//param.thisObject Get in the hook callback method
common.setObjectField(param.thisObject, 'Variable Name', 'Variable Value');
```

[View more](https://p-bakker.github.io/rhino/tutorials/scripting_java/)

### frida

[View more](https://frida.re/docs/javascript-api/)