# Memory Viewer

## Overview

If you're familiar with ReClass / Cheat Engine's "dissect structure" tool, this is basically just that minus the control that you have with ReClass, and/or Cheat Engine. The "MEM" tab essentially just iterates through all the offsets in the specified address, and displays its value in several data-types, ranging from dword (int32), double (f64), float (f32), string, and boolean. You're also able to copy and write to these offsets in such data-types. It also provides RTTI (Run-time type information) for offsets.&#x20;

## Layout

The first page that will be open once you navigate to this tab, is the DataModel address. once expanded you will see something like this.

<div align="left"><figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure></div>

The first pink hexadecimal number here (0x0), is offset. This number typically never changes if you're using a pointer for the same class of structure.

The second gray number (0x7ff6a1442b70) is the hexadecimal 64-bit address that this value points to. You can copy this value with the button "copy" at the bottom.

The text value pinkish (H7???) is the string value.

Next column, contains values, such as dword, qword, double, float, and bool. You can set these values accordingly with the buttons below.
