```json
// tasks.json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Compile", // 任务名称，与launch.json的preLaunchTask相对应
            "command": "clang", // 要使用的编译器
            "args": [ // 编译命令参数
                "${file}", //要编译的文件名，你也可以改成 *.cpp 表示编译当前目录所有的cpp文件
                "-o", //指定生成的程序名字
                //"${file}.exe", 
                "${fileDirname}/${fileBasenameNoExtension}.exe", //这是你要生成的程序名字
                "-Wall", // 开启额外警告
                "-g", // 生成和调试有关的信息
                "-static-libgcc", // 静态链接
                "-fcolor-diagnostics", //彩色信息
                "-w", //屏蔽警告
                "-std=c11", // C语言最新标准为c11，或根据自己的需要进行修改
                // onle gcc生成的程序使用GBK编码，不加这一条会导致Win下输出中文乱码
                //"-fexec-charset=GBK", 

                "--target=x86_64-w64-mingw", // 默认target为msvc，不加这一条就会找不到头文件

                // 用MinGW写C时留着，否则不需要，用于支持printf的%zd和%Lf等
                // "-D__USE_MINGW_ANSI_STDIO", 

                //以下都是链接库参数，需要链接什么库就加在这
                "-lws2_32",
                "-lIphlpapi",
                "-lgdi32"
            ],
            "type": "shell",
            "group": {
                "kind": "build",
                "isDefault": true // 设为false可做到一个tasks.json配置多个编译指令，需要自己修改本文件，我这里不多提
            },
            "presentation": {
                "echo": true,
                "reveal": "always", // 在“终端”中显示编译信息的策略，可以为always，silent，never。具体参见VSC的文档
                "focus": false, // 设为true后可以使执行task时焦点聚集在终端，但对编译c和c++来说，设为true没有意义
                "panel": "shared" // 不同的文件的编译信息共享一个终端面板
            }
        }
    ],
}
```
