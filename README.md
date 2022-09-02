# GNU Arm embedded toolchain for macOS

The GNU Embedded Toolchain for Arm is a ready-to-use, open source suite of tools
for C, C++ and Assembly programming targeting Arm Cortex-M and Cortex-R family 
of processors. It includes the GNU Compiler (GCC) and is available free of 
charge directly from Arm for embedded software development on Windows, Linux and
macOS operating systems.

<div>
<img src="https://raw.githubusercontent.com/chipcode-nl/gcc-arm-mac/master/images/macOS.png" alt="macOS" width="24%">
<img src="https://raw.githubusercontent.com/chipcode-nl/gcc-arm-mac/master/images/GNU.png" alt="GNU" width="24%">
<img src="https://raw.githubusercontent.com/chipcode-nl/gcc-arm-mac/master/images/Cortex-M.png" alt="Cortex-M" width="24%">
<img src="https://raw.githubusercontent.com/chipcode-nl/gcc-arm-mac/master/images/Cortex-R.png" alt="Cortex-R" width="24%">
</div>

This repository is the original macOS version of the GNU Compiler from Arm 
packaged for Visual Studio Code:
[GNU Arm embedded toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)

## Install
In Visual Studio Code goto extensions (shift+cmd+x), search for '*chipcode-nl*' 
and install the extension that is suited for your operating system. 

The extension has four paths for the toolchain. You can use them in the 
tasks.json.

- arm-none-eabi.bin
- arm-none-eabi.include
- arm-none-eabi.lib

Here is an example of tasks.json for GNU make. 
```javascript
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "build firmware",
      "type": "shell",
      "command": "make test",
      "options": {
        "env": {
          "INCLUDE": "${config:arm-none-eabi.include}",
          "LIB": "${config:arm-none-eabi.lib}",
        }
      },
      "osx": {
        "options": {
          "env": {
            "PATH": "${config:arm-none-eabi.bin}:${env:PATH}",
          }
        },
      },
      "linux": {
        "options": {
          "env": {
            "PATH": "${config:arm-none-eabi.bin}:${env:PATH}",
          }
        },
      },
      "windows": {
        "options": {
          "env": {
            "PATH": "${config:arm-none-eabi.bin};${env:PATH}",
          }
        },
      },
      "group": {
        "kind": "build",
        "isDefault": true,
      },
      "problemMatcher": "$gcc"
    }
  ]
}
```
With the following makefile:
```makefile
.PHONY: test

test:
	@echo $(PATH)
	@echo $(INCLUDE)
	@echo $(LIB)
```

## Release Notes

### Version 1.0.2
Added license

### Version 1.0.1
Fixed library path

### Version 1.0.0
GNU Arm Embedded Toolchain
Version 10-2020-q4-major
Released: December 11, 2020

GNU Make 4.3
