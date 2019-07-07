---
layout: post
title:  "Intel HD issues"
date: 2019-07-07 11:30:26 +0800
---

I had a funny issue recently. I tried to make work OpenGL on Python on my PC at the office. Python is much easier to maintain and program than C++. And it has a nice package manager. But whatever I tried, it just showed me that I have an OpenGL 1.1 instead of 3.1 which my graphics card says.

I've tried to recompile PyOpenGL, but it did nothing.
The funny thing is I had C++ version of the program and exactly the same program written on Python. One was working and the other not.
They both were using the same OpenGL32.dll and glfw3.dll. I was afraid I have to go deeper into assembly to find out what's going on, which could take me even more days, but luckily I have found the answer on some forum.

At the office, I have an Intel HD Graphics 2000 video card. It turns out that Intel does not support this video card drivers for a long time, especially for Windows 10. But why my C++ program works? And why I do have nice shader graphics on shadertoy.com? The reason is how windows decide which dlls are available to which program. It is written in Manifest-resource inside an .exe file in supported OS section.

In my case it was in python.exe. When I removed {8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a} GUID (windows 10) from python.exe Manifest section, both C++ and Python versions work like a charm.
