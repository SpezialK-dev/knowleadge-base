
# A small guid on how to set up your proxmark under Arch linux

[Installation Guid](https://github.com/RfidResearchGroup/proxmark3/blob/master/doc/md/Installation_Instructions/Linux-Installation-Instructions.md)
[Compilation instructions](https://github.com/RfidResearchGroup/proxmark3/blob/master/doc/md/Use_of_Proxmark/0_Compilation-Instructions.md)

## Choosing a firmware 

The normal firmware proxmark firmware seems to be outdated ? The most maintained firmware seems to be the one from [iceman](https://github.com/RfidResearchGroup/proxmark3) . Here we also have documentation for Arch linux.


## Installing the right dependencies 

```shell
sudo pacman -Syu git base-devel readline bzip2 lz4 arm-none-eabi-gcc \
arm-none-eabi-newlib qt5-base bluez python gd --needed
```

IMPORTANT remove [modem manager ](https://github.com/RfidResearchGroup/proxmark3/blob/master/doc/md/Installation_Instructions/ModemManager-Must-Be-Discarded.md)


the clone the repo
```shell
git clone https://github.com/RfidResearchGroup/proxmark3.git
```

# Some issues that I ran into while compiling it myself

```shell
/bin/sh: line 1: ./bmptst: Permission denied
make[2]: *** [Makefile:34: bmptst] Error 1
make[1]: *** [Makefile:949: deps/reveng/libreveng.a] Error 2
make[1]: *** Waiting for unfinished jobs....
In file included from /usr/include/qt/QtCore/qfuture.h:45,
                 from /usr/include/qt/QtCore/QtCore:97,
                 from /usr/include/qt/QtGui/QtGuiDepends:3,
                 from /usr/include/qt/QtGui/QtGui:3,
                 from src/proxguiqt.h:30,
                 from src/proxguiqt.cpp:19:
/usr/include/qt/QtCore/qfutureinterface.h:284:37: error: template-id not allowed for constructor in C++20 [-Werror=template-id-cdtor]
  284 |     explicit QFutureInterface<void>(State initialState = NoState)
      |                                     ^~~~~
/usr/include/qt/QtCore/qfutureinterface.h:284:37: note: remove the ‘< >’
In file included from /usr/include/qt/QtCore/qfuture.h:45,
                 from /usr/include/qt/QtCore/QtCore:97,
                 from /usr/include/qt/QtGui/QtGuiDepends:3,
                 from /usr/include/qt/QtGui/QtGui:3,
                 from src/proxguiqt.h:30,
                 from src/proxgui.cpp:22:
/usr/include/qt/QtCore/qfutureinterface.h:284:37: error: template-id not allowed for constructor in C++20 [-Werror=template-id-cdtor]
  284 |     explicit QFutureInterface<void>(State initialState = NoState)
      |                                     ^~~~~
/usr/include/qt/QtCore/qfutureinterface.h:284:37: note: remove the ‘< >’
In file included from /usr/include/qt/QtCore/qfuture.h:45,
                 from /usr/include/qt/QtCore/QtCore:97,
                 from /usr/include/qt/QtGui/QtGuiDepends:3,
                 from /usr/include/qt/QtGui/QtGui:3,
                 from src/proxguiqt.h:30,
                 from src/proxguiqt.moc.cpp:10:
/usr/include/qt/QtCore/qfutureinterface.h:284:37: error: template-id not allowed for constructor in C++20 [-Werror=template-id-cdtor]
  284 |     explicit QFutureInterface<void>(State initialState = NoState)
      |                                     ^~~~~
/usr/include/qt/QtCore/qfutureinterface.h:284:37: note: remove the ‘< >’

```

was the error that I encountered

The trouble shooting steps that I took to fix this issue.

fixing the permission problems was a problem on my side, where my drive permissions where configured incorrectly after fixing that we are still left with the error in compiling the software. 

I think the easiest quickest solution would be to disable QT gui features since a terminal interface would be enough for me. 

## running it without QT enabled 

since QT refuses to work I will need to do a small work around, I dont want to thinker around in the header files since that could and most likely would break my system.


Now I am trying to build it with the Docker image for archlinux, since these are firstly isolated and secondly they dont have the QT problem (since they dont use QT)

This seemed to have worked?
It passed through so it compiled something???