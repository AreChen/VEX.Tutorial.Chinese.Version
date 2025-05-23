# VEX Tutorial / VEX 教程

## A collection of code snippets and examples showing syntax and capabilities of VEX language inside SideFX Houdini / 展示 SideFX Houdini 中 VEX 语言语法及能力的代码片段和示例集合

## 译者导语 / Translator's Introduction
### 翻译此篇教程目的如下 / The purpose of translating this tutorial is as follows:
#### 一、帮助国内 Houdini 爱好者们了解 VEX，为国内 VFX 事业做贡献。 / 1. To help Houdini enthusiasts in China understand VEX and contribute to the domestic VFX industry.
#### 二、学习 VEX 提升自我。 / 2. To learn VEX and improve myself.
#### 三、英语学习与练习。 / 3. To learn and practice English.
#### 此篇教程并不是简单翻译，我通过亲身练习&学习对教程二次创造，增改内容，引入 Houdini 官方 HelpFile 帮助理解，与大家共同进步。 / This tutorial is not a simple translation. Through personal practice and learning, I have recreated and modified the content, incorporating Houdini's official HelpFile to aid understanding, and to progress together with everyone.

## 未来计划 / Future Plans
### 待完成后进行二次校对，图文并茂，增添 Hip 文件 / After completion, conduct a second review, enrich with images and text, and add Hip files.

<p align="right"><small><sup>by Juraj Tomori</sup></small></p>
<p align="right"><small><sup>Translate & Recreate By AreChen</sup></small></p>
<br>

### Intro / 前言
Recently I made a small lecture for other students at Filmakademie. They requested an introduction lecture to using VEX. I did not focus on practical examples and fancy operations, but on syntax, capabilities, and usage. During the lecture, I got some ideas on extending the content. So I looked more into the topics and collected them along with explanations inside one hip file. This tutorial belongs to a series of my posts at my [blog](https://jurajtomori.wordpress.com/). However, because of the formatting and other limitations of Wordpress, I decided to place it here. It will also be easier to keep track of changes.  
最近我在 Filmakademie 为一些学生做了一个小讲座。他们要求介绍一下 VEX，我并没有为他们展示实际案例也没有炫技，而是更加注重在 VEX 的语法、功能及用法上。在演讲中，我更加开拓思路，所以我对 VEX 做了更加深入地研究，并将它们收集在 .hip 文件中并赋予了解释，这套教材本来放在我的个人[博客](https://jurajtomori.wordpress.com/)，但由于 Wordpress 的某些限制，我将它们放在 GITHUB 中，这样更加方便追踪它的变化。

### How to use it / 如何使用
You can clone, or [directly download](https://github.com/AreChen/vex_tutorial/archive/VEX.Tutorial.Chinese.Version.zip) this repository.  
It contains **examples.hipnc** and [**vex/include/myLib.h**](./vex/include/myLib.h) files which are full of various examples with explanations in comments.  
It is best to check all the nodes with open *Geometry Spreadsheet* and *Console Output* windows to see values of attributes and output text. Alternatively, you can use this page for quick looking at the topics covered and most of the code that I include here as well. I am not including here all of the code since sometimes it might not make a lot of sense outside of Houdini. Where necessary, I include related functions from *myLib.h* or attach screenshots.  
您可以克隆或[直接下载](https://github.com/AreChen/vex_tutorial/archive/VEX.Tutorial.Chinese.Version.zip)此仓库。  
它包含 **examples.hipnc** 和 [**vex/include/myLib.h**](./vex/include/myLib.h) 文件，其中包含各种示例以及注释。  
检阅时最好打开 **Geometry Spreadsheet** 和 **Console Output** 窗口检查这些节点以查看属性输出的值。或者，您可以使用此页面快速查看所涵盖的主题以及此处包含的大部分代码。这里并没有涵盖所有的代码，因为有时它可能在 Houdini 之外并没有多大意义。必要时我会在 **myLib.h** 中包含相关函数或附上截图。

### Topics / 主题
* [Automatic attribute creation / 自动属性创建](#automatic-attribute-creation--自动属性创建)
* [Getting transformation from OBJs / 从 OBJ 获取变换](#getting-transformation-from-objs--从-obj-获取变换)
* [Intrinsics / 内在属性](#intrinsics--内在属性)
* [VDB intrinsics / VDB 内在属性](#vdb-intrinsics--vdb内在属性)
* [Volumes / 体积](#volumes--体积)
* [VOPs / Using Snippets / VOPs / 使用片段](#vops--using-snippets--vops--使用片段)
* [VOPs / Using Inline Code / VOPs / 使用内联代码](#vops--using-inline-code--vops--使用内联代码)
* [DOPs / Volumes workflow / DOPs / 体积工作流程](#dops--volumes-workflow--dops--体积工作流程)
* [DOPs / Gas Field Wrangle / DOPs / 气体场操作](#dops--gas-field-wrangle--dops--气体场操作)
* [DOPs / Gas Field Wrangle - accessing DOPs and SOPs data / DOPs / 气体场操作 访问 DOPs 和 SOPs 数据](#dops--gas-field-wrangle---accessing-dops-and-sops-data--dops--气体场操作-访问-DOPs-和-SOPs-数据)
* [DOPs / Geometry workflow / DOPs / 几何体工作流程](#dops--geometry-workflow--dops--几何体工作流程)
* [DOPs / Geometry Wrangle / DOPs / 几何体操作](#dops--geometry-wrangle--dops--几何体操作)
* [DOPs / Geometry Wrangle - accessing fields / DOPs / 几何体操作 访问字段](#dops--geometry-wrangle---accessing-fields--dops--几何体操作-访问字段)
* [Conditions / 条件](#conditions--条件)
* [Loops / 循环](#loops--循环)
* [Stopping For-Each SOP from VEX / 从 VEX 停止 For-Each SOP](#stopping-for-each-sop-from-vex--从-VEX-停止-For-Each-SOP)
* [Printing and formatting / 打印和格式化](#printing-and-formatting--打印和格式化)
* [Printing attributes / 打印属性](#printing-attributes--打印属性)
* [Including external VEX files / 包含外部 VEX 文件](#including-external-vex-files--包含外部-vex-文件)
* [Include math.h / 包含 math.h](#include-mathh--包含-mathh)
* [Using macros / 使用宏](#using-macros--使用宏)
* [Functions / 函数](#functions--函数)
* [Functions overloading / 函数重载](#functions-overloading--函数重载)
* [Variables casting / 变量转换](#variables-casting--变量转换)
* [Vectors swizzling / 向量重组](#vectors-swizzling--向量重组)
* [Functions casting / 函数类型转换](#functions-casting--函数转换)
* [Structs / 结构体](#structs--结构体)
* [Structs in Attribute Wrangle / 属性操作中的结构体](#structs-in-attribute-wrangle--属性操作中的结构体)
* [Groups / 组](#groups--组)
* [Attribute typeinfo / 属性类型信息](#attribute-typeinfo--属性类型信息)
* [Attributes to create / 要创建的属性](#attributes-to-create--要创建的属性)
* [Enforce prototypes / 强制原型](#enforce-prototypes--强制原型)
* [Attribute default values / 属性默认值](#attribute-default-values--属性默认值)

### Tutorial / 教程

#### Reading parameter values / 读取参数值
```C
/*
multi-line comments can be typed
using this syntax
使用此语法可以进行多行注释
*/

// in vex you can evaluate values from parameters on this node 
// 在 VEX 中你可以通过节点的参数计算数值
// by calling ch*() function, with * representing a signature, check the docs 
// 调用 ch*() 函数，*表示拥有多个 ch() 函数，具体参阅文档(F1)
// for the full list, some of them: chv() - vector, chu() - vector2, chs() - string 
// 其中一些是: chv() - vector(矢量/三维向量), chu() - vector2(二维向量), chs() - string(字符串)
// chramp() - ramp, chp() - vector4, chi() - int, chf() - float, ch4() - matrix, ch3() - matrix3 ... 
// chramp() - (渐变), chp() - (四维向量), chi() - (整型数值), chf() - (浮点数值), ch4() - (4X4矩阵), ch3() - (3X3矩阵) ...
// you can also use optional argument for time which will enable you to evaluate the channel at different frame
// 你也可以使用时间作为参数
// the channel at different frame
// 使你可以在不同帧数上计算通道的值
// once you type ch*() in your code, you can press a button on the right, to
// 当你在代码中使用了 ch*() 
// generate a UI parameter for it automatically, you can do the same by hand as well
// 你可以手动点击右边的按钮生成滑动条以供控制参数
float y = chf("y_position");
vector col = chv("color");
matrix3 xform = ch3("xform");

// you can also reference parameters from external nodes
// 你也可以提取外部节点的参数
// if there is an expression (Python/hscript) in the parameter,
// 如果在参数中含有表达式(Python/Hscript)
// it will be evaluated
// 将会被计算
float up = chf("../params_1/move_up");

// apply variables to attributes
// 将变量赋予属性
v@P.y += y*5;
v@Cd = col;
v@P *= xform;
v@P.y += up;

v@myVec = 1.456;
v@myVec += v@N.y;
```

#### Reading attributes / 读取属性
```C
float blend = chf("blend");
float blendPig = chf("blend_pig");
vector P1, P2, P3, P_new;

// this is one way of reading attributes, this is only valid, when
// point count is exactly the same in both inputs, then attribute from
// point from second input with the same @ptnum is retrieved
// v@P can also be replaced with @P, since its signature can be guessed as it is
// commonly used attribute, however I prefer explicit declaration :)
// 这是一种读取属性的方式，但只有当两个输入值完全相同时才会生效
// 从第二个 point 获取属性并检索相同的 @ptnum v@P 也可以用 @P 替换 
// 从它的标识可看出来它是常用属性，但我更喜欢明确的声明:)
// v@ - vector向量, i@ - integer整型, f@ - float浮点, 3@ - matrix3 3x3矩阵, p@ - vector4 四维向量
// 4@ - matrix4 4x4矩阵, 2@ - matrix2 2x2矩阵, u@ - vector2 二维向量, s@ - string字符串,
// P1 = v@P;
// P2 = v@opinput1_P; // inputs numbering starts at 0, therefore 1 refers to the second input
                     // 输入值从第0位开始，因此1是指第二个输入值

// this approach is useful for querying attributes from different points (other from the currently processed one)
// node input numbering starts from 0 (first input), 1 (second input) ...
// 这种方法有利于从不同的点查询属性，节点输入编号从0(第一个输入),1(第二个输入)等……

P1 = point(0, "P", @ptnum);
P2 = point(1, "P", @ptnum);

// note that you can also read attributes from node, which is not connected
// 注意，你可以从其它节点读取属性，如果没有链接到当前节点需要使用"op:"语法
// to the current node using the "op:" syntax
// this is valid for any function which is expecting geo handle (sampling from other volumes...)
// 这个方法可以适用于任何函数的处理(从其他体积采样等……)
// note that Houdini network UI will not detect this dependency when Show -> Dependency links display is enabled
// 注意，在 Houdini 网络中当显示->依赖链接时，UI 将不会检测到这种依赖性 
P3 = point("op:../pig_shape", "P", @ptnum);

// blend positions
// 混合位置属性
P_new = lerp(P1, P2, blend);
P_new = lerp(P_new, P3, blendPig);

v@P = P_new;
```

#### Exporting attributes / 输出属性
```C
// create a new attribute simply by typing *@attrib_name with
// * representing its signature
// 通过输入 *类型@属性名称 以创建一个新属性
// v@ - vector, i@ - integer, f@ - float, 3@ - matrix3, p@ - vector4
// 4@ - matrix4, 2@ - matrix2, u@ - vector2, s@ - string

v@myVector = {1,2,3};
// vectors with functions/variables in them need to be created with set()
// 向量函数/变量创建时 需要使用 set() 初始化
u@myVectorFunc = set(@Frame, v@P.y);
u@myVector2 = {4,5};
f@myFloat = 400.0;
i@myInteger = 727;
3@myMatrix3x3 = matrix3( ident() ); // this line contains function casting, which is explained in functions_casting section
                                    // 这一行包含着构造函数，将会在 functions_casting 章节中讲到
4@myMatrix4x4 = matrix( ident() );
s@myString = "abc";

// attributes can be set to different point from the currently processed one
// and if they do not exist, they need to be added first
// setpointattrib() is also the only way of setting an attribute on newly
// created points
// 可以为不同的点设置一个不同的属性
addpointattrib(0, "Cd", {0,0,0});// 全局属性设置
int  addpointattrib(int geohandle, string name, <type>defvalue)
int  addpointattrib(int geohandle, string name, <type>defvalue[])

setpointattrib(0, "Cd", 559, {1,0,0});// 局部属性设置
int  setpointattrib(int geohandle, string name, int point_num, <type>value, string mode="set")
int  setpointattrib(int geohandle, string name, int point_num, <type>value[], string mode="set")

// arrays can be exported as well
// 数组也可以输出
v[]@myVectorArray = { {1,2,3}, {4,5,6}, {7,8,9} };
u[]@myVector2Array = { {4,5}, {6,7} };
f[]@myFloatArray = { 4.0, 2.7, 1.3};
i[]@myIntegerArray = {132, 456, 789};
// arrays containing functions/variables need to be initialized with array() function
// 数组包含函数/变量时，需要使用 array() 函数初始化
3[]@myMatrix3x3Array = array( matrix3( ident() ), matrix3( ident() ) * 5 );
4[]@myMatrix4x4Array = array( matrix( ident() ), matrix( ident() ) * 9 );
s[]@myStringArray = { "abc", "def", "efg" };
<matrix> ident()
// 返回识别到的矩阵参数到指定矩阵类型.
```

#### Reading arrays / 读取数组
```C
// this is how you can create local array variables and load array attributes into them
// 本章将介绍如何创建本地数组变量并读取数组属性
vector myVectorArray[] = v[]@myVectorArray;

matrix3 a = ident() * 5;

v@P.x *= a.yy; // you can access matrix components using this syntax
               // 你可以通过以下语法访问阵列元素
// x -> 1st element, y -> 2nd, z -> 3rd, w -> 4th
// x 第一位元素, y 第二位元素, z 第三位元素, w 第四位元素
v@P.y = 4[]@myMatrix4x4Array[1].ww; // second array matrix, last element 第二个矩阵数组的最后一个元素
v@P.z = u[]@myVector2Array[1][0]; // this is how you can access array of vectors - second array, first element
                                  // 访问向量数组的第二个数组的第一个元素
```

#### Arrays / 数组
```C
int numbers[] = array(1,2,3,4);

// arrays can be handled in Pythonic way
// 数组可以使用 Python 的方式处理
numbers = numbers[::-1]; // array reverse 数组翻转

// reading from arrays
// 从数组中读取
i@firstItem = numbers[0];
// writing into arrays
// 写入数组
numbers[0] += 1;
// indexing can also go backwards
// 也可以倒着索引
i@secondLastItem = numbers[-2];

// slicing
// 切分
i[]@firstHalf = numbers[:2];
i[]@secondHalf = numbers[2:];

// some useful functions
// 一些有用的函数
i@returnedPopVal = pop(numbers); // removes the last element and returns it
                                // 移除最后的元素并且返回它
push(numbers, i@returnedPopVal); // appends element to the array
                                // 添加元素到数组
i@lenghtOfArray = len(numbers);// 返回长度

i[]@numbers = numbers; // export into integer array attribute
                      // 导出整数数组属性

// flattening an array of vectors and reverting it
// 将一个向量数组转换成一维数组，并恢复向量数组
vector vectors[] = { {1,2,3}, {4,5,6}, {7,8,9} };
f[]@serializedVectors = serialize(vectors);
v[]@unserializedFloats = unserialize(f[]@serializedVectors);
```

#### Arrays and strings example / 数组及字符串样例
```C
// simple example of manipulating strings and arrays
// it will convert /path/to/the/project/file/project_v3.hipnc
// into            /path/to/the/project/file/preview/project_v3_img_0001.jpg
// with 0001 being current frame number
// 简单的操作字符串和数组的例子，它将转换 /path/to/the/project/file/project_v3.hipnc
// 到 /path/to/the/project/file/preview/project_v3_img_0001.jpg
// 0001 代表当前帧数

string path = chs("path"); // get string from path parameter of the current hipfile
                          // 获取当前 .hip 文件路径字符串
s@pathOrig = path; // store into attribute original value
                  // 存储并初始化值

string pathSplit[] = split(path, "/"); // split path into array of strings based on "/" character
                                      // 将路径使用"/"分割

string fileName = pop(pathSplit); // remove last value of the array and assign it into a variable
                                // 移除数组的最后一个值并将其赋值给一个变量
string fileNameSplit[] = split(fileName, "."); // split string into an array based on "." character
                                              // 将数组使用"."分割
fileNameSplit[0] = fileNameSplit[0] + sprintf("_img_%04d", @Frame); // append into the string _img_0001 (current frame number)
                                                    // 将 _img_0001 添加至字符串(@Frame 当前帧数)
fileNameSplit[-1] = "jpg"; // change file extension
                          // 改变文件扩展名
fileName = join(fileNameSplit, "."); // convert array of strings into a one string with "." between original array elements
                                    // 转换字符串数组到一个字符串变量并使用 "." 分开
push(pathSplit, "preview"); // append "preview" string into the array of strings
                           // 添加"preview"字符串到字符串数组
push(pathSplit, fileName); // append file name into the array of strings
                          // 添加文件名到字符串数组

path = "/" + join(pathSplit, "/"); // convert array of strings into one string, starting with "/" for root, because it is not added before the first element, only to in-betweens
                                  // 转换字符串数组到一个字符串 以"/"开始，因为并不是在第一个元素之前添加而是在两者之间

s@path = path; // output into the attribute
              // 输出到属性
```


#### Reading and writing Matrices / 矩阵的读写
```C
// To initialize a vector or a matrix with a variable/attribute we have to use the set method
// 要用变量/属性初始化向量或矩阵，我们必须使用 set 方法
float   f = 0;
vector  v = set(f,f,f);
matrix3 m = set(f,f,f,f,f,f,f,f,f);
        m = set(v,v,v);

// We can then read the value back by
// 然后我们可以通过以下方式读取值
float f = getcomp(m,0,0);
// However we can not read back a vector directly instead we have to use:
// 但是我们不能直接读取向量，而是必须使用：
f = set(getcomp(m,0,0));
v = set(getcomp(m,0,0),
        getcomp(m,0,1),
        getcomp(m,0,2));
// Likewise the setcomp can be used
// 同样可以使用 setcomp
setcomp(m,f,0,0);
```

#### Checking for attributes / 检查属性
```C
// it is also possible to determine if incoming geometry has an attribute
// 还可以确定输入几何体是否具有属性

i@hasCd = hasattrib(0, "point", "Cd");
i@hasN = hasattrib(0, "point", "N");
i@hasOrient = hasattrib(0, "point", "orient");
i@hasPscale = hasattrib(0, "point", "pscale");
```

#### Automatic attribute creation / 自动属性创建
```C
// if you use @attribute and it does not exist, 
// then it will be automatically created
// this might lead to problems, when you have a typo and a 
// new attribute is created
// 如果你使用 @attribute 且它不存在，
// 那么它将自动创建
// 当你拼写错误时可能会导致问题，
// 一个新属性将被创建

f@foo = 4;
f@boo = v@Cd.y;
// v@CD = {1,1,0}; // this line does not work here, otherwise it would create new v@CD attribute
// v@CD = {1,1,0}; // 这行代码在这里不起作用，否则会创建新的 v@CD 属性

// if you remove * character from "Attributes to Create" parameter
// below, then you need to manually specify new attributes
// to be created, if you then have a typo and use v@CD instead
// of v@Cd, node will report an error
// 如果你从下面的“Attributes to Create”参数中移除 * 字符，
// 那么你需要手动指定要创建的新属性，
// 如果你拼写错误并使用 v@CD 而不是 v@Cd，节点将报告错误
```

#### Getting transformation from OBJs / 从 OBJ 获取变换
```C
// VEX is well integrated into Houdini, it can for example fetch
// world space transformation matrix from an OBJ node, let it be a null OBJ
// or part from a rig, camera or whatever object there which has a transformation
// optransform() will contain also all parent transformations
// VEX 与 Houdini 很好地集成，例如它可以从 OBJ 节点获取
// 世界空间变换矩阵，可以是空的 OBJ，
// 也可以是来自装备、相机或任何具有变换的对象的部分
// optransform() 还将包含所有父变换

string nodePath = chs("node_path"); // parameter is a string, but I went into "Edit Parameter Interface" and specified it to be a Node Path
// nodePath 是一个字符串参数，但我在“Edit Parameter Interface”中指定它为 Node Path
matrix xform = optransform(nodePath);

v@P *= invert(xform);
```

#### Intrinsics / 内在属性
```C
// a lot of information and functionality is stored in
// "intrinsic" attributes, they might be hidden to many users
// because they do not show up in primitive attributes list
// by default
// they are however very useful and important for manipulating
// and controlling those primitives from VEX
// 很多信息和功能存储在
// “intrinsic”属性中，对许多用户来说可能隐藏，
// 因为它们默认情况下不会出现在基本属性列表中
// 然而，它们对于从 VEX 操作和控制这些基本元素非常有用和重要

// you can display intrinsics in Geometry Spreadsheet, in primitive attributes
// and Show All Intrinsics in Intrinsics drop-down menu
// intrinsics that are greyed out are read-only, the rest is also writable
// 你可以在 Geometry Spreadsheet 中的基本属性中显示内在属性，
// 并在 Intrinsics 下拉菜单中选择 Show All Intrinsics
// 灰色的内在属性是只读的，其余的也可以写入

// in this example I will show you how to access and modify those
// values, I will refer to them based on their point numbers as
// those intrinsics vary based on the primitive we are dealing with
// 0 - packed geo, 1 - VDB, 2 - sphere, 3 - packed disk, 4 - abc
// if you change order of inputs in merge, then those numbers will change
// in our case @ptnum matches @primnum
// 在这个例子中，我将向你展示如何访问和修改这些值，
// 我将根据它们的点号来引用它们，
// 因为这些内在属性根据我们处理的基本元素而变化
// 0 - 打包几何体, 1 - VDB, 2 - 球体, 3 - 打包磁盘, 4 - abc
// 如果你在 merge 中更改输入顺序，那么这些数字将改变
// 在我们的例子中，@ptnum 与 @primnum 匹配

// this is the type of our primitive
// 这是我们基本元素的类型
s@primitiveType = primintrinsic(0, "typename", @ptnum);

matrix3 xform = ident();

// sphere
// 球体
if (@ptnum == 2) {
    // accessing sphere volume and area
    // 访问球体体积和面积
    f@sphereVolume = primintrinsic(0, "measuredvolume", @ptnum);
    f@sphereArea = primintrinsic(0, "measuredarea", @ptnum);
    
    // changing sphere scale, rotation which is not accessible through standard attributes
    // this intrinsic is also present on other primitives
    // 更改球体比例、旋转，这些无法通过标准属性访问
    // 这个内在属性也存在于其他基本元素上
    xform = primintrinsic(0, "transform", @ptnum);
    scale(xform, {1,2,3});
    rotate(xform, radians(45), normalize({1,2,3}) );
}

// packed geo
// 打包几何体
if (@ptnum == 0) {
    // change viewport display to point cloud
    // 更改视口显示为点云
    setprimintrinsic(0, "viewportlod", @ptnum, "points", "set");
    
    // move packed's pivot to the bottom
    // bounds are stored in this order: xmin, xmax, ymin, ymax, zmin, zmax
    // 将打包的枢轴移到底部
    // 边界按此顺序存储：xmin, xmax, ymin, ymax, zmin, zmax
    float bounds[] = primintrinsic(0, "bounds", @ptnum);
    vector pivot = primintrinsic(0, "pivot", @ptnum);
    pivot.y = bounds[2];
    setprimintrinsic(0, "pivot", @ptnum, pivot, "set");
    v@P.y = bounds[2];
    
    // and now transform the primitive along its new pivot :)
    // 现在沿着新的枢轴变换基本元素 :)
    xform = primintrinsic(0, "transform", @ptnum);
    scale(xform, {1,2,3});
    rotate(xform, radians(-45), normalize({1,2,3}) );
}

// packed disk
// 打包磁盘
if (@ptnum == 3) {
    // changing this intrinsic can point the primitive into different geometry on disk
    // so instead of boring cube let's have something way cooler
    // this is very powerful - e.g. controlling your instances, see my other blog post about using it
    // https://jurajtomori.wordpress.com/2016/09/29/rain-and-ripples-rnd/
    // 更改这个内在属性可以将基本元素指向磁盘上的不同几何体
    // 所以与其使用无聊的立方体，不如来点更酷的东西
    // 这非常强大 - 例如控制你的实例，参见我关于使用它的其他博客文章
    // https://jurajtomori.wordpress.com/2016/09/29/rain-and-ripples-rnd/
    setprimintrinsic(0, "unexpandedfilename", @ptnum, "$HH/geo/HoudiniLogo.bgeo", "set");
    
    // and our mandatory transformation :)
    // 还有我们必须的变换 :)
    xform = primintrinsic(0, "transform", @ptnum);
    scale(xform, 5);
    rotate(xform, radians(-90), {1,0,0} );
}

// alembic
// alembic 文件
if (@ptnum == 4) {
    // make him move in the loop, he has 48 frames of animation
    // 让他在循环中移动，他有 48 帧动画
    float frame = @Frame / 24;
    frame = frame % 2;
    setprimintrinsic(0, "abcframe", @ptnum, frame, "set");
    
    // get some useful info
    // 获取一些有用的信息
    s@abcObjPath = primintrinsic(0, "abcobjectpath", @ptnum);
    s@abcFilePath = primintrinsic(0, "abcfilename", @ptnum); // also useful intrinsic
    // s@abcFilePath = primintrinsic(0, "abcfilename", @ptnum); // 也很有用的内在属性
    s@abcType = primintrinsic(0, "abctypename", @ptnum);
    s@abcVis = primintrinsic(0, "viewportlod", @ptnum);
    
    // scale the bear up
    // 放大熊
    xform = primintrinsic(0, "transform", @ptnum);
    scale(xform, 20);
}

// all of the primitives have "transform" intrinsic, so I update it at the end
// 所有的基本元素都有“transform”内在属性，所以我在最后更新它
setprimintrinsic(0, "transform", @ptnum, xform, "set");
```


#### VDB intrinsics / VDB 内在属性
```C
// for some reason updating VDB's transform and other primitives transform
// did not work properly from one wrangle, so I put it here
// VDB's transform is 4x4 matrix, while other prims have 3x3 matrices
// 由于某种原因，从一个 wrangle 更新 VDB 的变换和其他基本元素的变换
// 无法正常工作，所以我把它放在这里
// VDB 的变换是 4x4 矩阵，而其他基本元素是 3x3 矩阵

// VDB
if (@ptnum == 1) {
    // accessing useful information
    // 访问有用的信息
    i@vdbVoxels = primintrinsic(0, "activevoxelcount", @ptnum);
    s@vdbClass = primintrinsic(0, "vdb_class", @ptnum);
    s@vdbType = primintrinsic(0, "vdb_value_type", @ptnum);
    s@vdbVis = primintrinsic(0, "volumevisualmode", @ptnum);
    v@vdbVoxelSize = primintrinsic(0, "voxelsize", @ptnum);
    
    // changing volume transformation
    // 更改体积变换
    matrix xform4 = primintrinsic(0, "transform", @ptnum);
    scale(xform4, {1,2,3});
    rotate(xform4, radians(-45), {1,0,0});
    setprimintrinsic(0, "transform", 1, xform4, "set");
    
    // setting volume export precision to half float, which saves space when written to disk
    // 设置体积导出精度为半浮点数，写入磁盘时节省空间
    setprimintrinsic(0, "vdb_is_saved_as_half_float", @ptnum, 1, "set");
}
```

#### Volumes / 体积
```C
// float volumes can be accessed with volumesample(), vector volumes need
// volumesamplev() function, those functions expect sampling position, which
// does not need to match voxel's center, then the value will be tri-linearly
// interpolated from neighbouring voxels
// 浮点体积可以使用 volumesample() 访问，向量体积需要
// volumesamplev() 函数，这些函数需要采样位置，
// 不需要与体素中心匹配，然后值将从相邻体素中三线性插值
float den1 = volumesample(0, "density", v@P);

// sampling position can be offset and lots of cool tricks and magic can be
// achieved with that
// 采样位置可以偏移，可以实现很多很酷的技巧和魔法
vector offset = set( 2, sin(@Frame * .1)*2 , 0 );
float den2 = volumesample(1, "density", v@P + offset);

// writing to volumes has the same syntax as writing to attributes
// 写入体积与写入属性的语法相同
f@density = lerp(den1, den2, chf("blend") );

// volumes can be accessed with the same syntax as geometry attributes
// 体积可以使用与几何属性相同的语法访问
f@density = f@density * chf("scale");
```

#### VOPs / Using Snippets / VOPs / 使用片段
*Check Houdini project to get the best idea of how it works.*  
*查看 Houdini 项目以获得最佳工作方式的了解。*
```C
// in snippets we do not need to use any sign for variables, only
// their name is needed
// it is also possible to rename them for this node in
// Variable Name parameters below
// 在片段中，我们不需要为变量使用任何符号，只需要
// 它们的名称
// 还可以在下面的 Variable Name 参数中为这个节点重命名它们

// to output a new variable, we need to input a constant
// into the node which will generate output for it (N, color)
// even though in the UI it is called outN and outcolor, we only
// need to write to N and color
// 要输出一个新变量，我们需要输入一个常量
// 到节点中，它将为其生成输出 (N, color)
// 尽管在 UI 中它被称为 outN 和 outcolor，我们只需要
// 写入 N 和 color

N = normalize(P);
dir = normalize(dir);

float mix = dot(dir, N);
mix = clamp(mix, 0, 1);

noise = abs(noise);
noise = clamp(noise, 0, 1);

color = lerp(frontColor, noise, 1-mix);
```

#### VOPs / Using Inline Code / VOPs / 使用内联代码
*Check Houdini project to get the best idea of how it works.*  
*查看 Houdini 项目以获得最佳工作方式的了解。*
```C
// here we can create additional output variables
// however we cannot write to read_only variables (which
// are not exported), therefore for loading $dir I create
// direction variable and for loading $noise noise_in variable
// 这里我们可以创建额外的输出变量
// 但是我们不能写入只读变量（未导出），
// 因此为了加载 $dir 我创建了 direction 变量，
// 为了加载 $noise 创建了 noise_in 变量

$N = normalize(P);
vector direction = normalize(dir);

float mix = dot(direction, N);
mix = clamp(mix, 0, 1);

vector noise_in = abs(noise);
noise_in = clamp(noise_in, 0, 1);

$color = lerp($frontColor, noise_in, 1-mix);
```

#### DOPs / Volumes workflow / DOPs / 体积工作流程
Here I will show basic steps of creating a simple custom DOP solver operating on volumes.  
在这里，我将展示创建操作体积的简单自定义 DOP 求解器的基本步骤。

1. At first we need to create a *DOP Object*, which is a container that will contain all our fields (volumes in DOPs), geometry and any other data. Object name is important, because later we will use it to access our data.  
   首先，我们需要创建一个 *DOP Object*，这是一个容器，将包含我们所有的字段（DOPs 中的体积）、几何体和其他数据。对象名称很重要，因为稍后我们将使用它来访问我们的数据。
   ![DOP Object](./img/dop_object_volume.jpg)
2. In the second step we want to bring in a volume from SOPs. We can use *SOP Scalar Field* node. This node will create field *pig_in*, which you can see in *Geometry Spreadsheet*. *Use SOP Dimensions* option is handy as we do not need to set resolution, size and other parameters by hand. *Border Type* might be useful to have set to *Constant* as it will not introduce infinite streaks when voxels are touching boundaries. *SOP Path* points to the SOP we want to get volume from and *Primitive Number* will identify which volume primitive to import. *Default Operation* when set to *Set Initial* will import the field only at first simulated frame, if you want to import animated volume, set it to *Set Always*. *Data Name* is important as it will be unique identifier for our volume.  
   在第二步中，我们希望从 SOPs 中引入一个体积。我们可以使用 *SOP Scalar Field* 节点。这个节点将创建字段 *pig_in*，你可以在 *Geometry Spreadsheet* 中看到。*Use SOP Dimensions* 选项很方便，因为我们不需要手动设置分辨率、大小和其他参数。*Border Type* 设置为 *Constant* 可能有用，因为当体素接触边界时不会引入无限条纹。*SOP Path* 指向我们想要从中获取体积的 SOP，*Primitive Number* 将标识要导入哪个体积基本元素。*Default Operation* 设置为 *Set Initial* 时，只会在第一个模拟帧导入字段，如果要导入动画体积，请设置为 *Set Always*。*Data Name* 很重要，因为它将是我们的体积的唯一标识符。
   ![SOP Scalar Field](./img/sop_scalar_field.jpg)
3. DOPs can contain lots of fields and therefore they are not visible by default. To display them in viewport, we can use *Scalar Field Visualization* node.  
   DOPs 可以包含很多字段，因此默认情况下它们不可见。要在视口中显示它们，我们可以使用 *Scalar Field Visualization* 节点。
   ![Scalar Field Visualization](./img/scalar_field_vis.jpg)
4. If we want to sample different volume, or sample a volume at different location, we need to set up *Inputs* properly. This is needed for [*Gas Field Wrangle*](#dops--gas-field-wrangle) and *Gas Field VOP*.  
   如果我们想采样不同的体积，或者在不同位置采样体积，我们需要正确设置 *Inputs*。这对于 [*Gas Field Wrangle*](#dops--gas-field-wrangle) 和 *Gas Field VOP* 是必要的。
   ![Gas Field Wrangle Inputs](./img/gas_field_wrangle_inputs.jpg)
   ![Gas Field VOP Inputs](./img/gas_field_vop_inputs.jpg)
5. We can also use arbitrary SOP operators to process our DOP fields. We can do so by using *SOP Solver*. We just need to set *Data Name* to our field which we want to process.  
   我们还可以使用任意 SOP 运算符来处理我们的 DOP 字段。我们可以通过使用 *SOP Solver* 来实现。我们只需要将 *Data Name* 设置为我们想要处理的字段。
   ![Sop Solver volume](./img/sop_solver_volume.jpg)
<br>


#### DOPs / Gas Field Wrangle / DOPs / 气体场操作
*Check Houdini project to get the best idea of how it works.*  
*查看 Houdini 项目以获得最佳工作方式的了解。*
```C
// we can access fields as in the SOPs, pig_in name
// corresponds to "Data Name" in sopscalarfield_init_pig_in node
// 我们可以像在 SOPs 中一样访问字段，pig_in 名称
// 对应于 sopscalarfield_init_pig_in 节点中的“Data Name”
f@pig_in *= .9;

// by default this line will not work, even though it should
// be the same as the previous line
// to make it work, we need to point "Input 1" in the "Inputs" tab
// to the field we want to fetch, in our case "volume/pig_in"
// this way we can access also fields from another DOP objects
// ("volume" is our DOP object in this case)
// 默认情况下，这行代码不起作用，尽管它应该
// 与前一行相同
// 要使其工作，我们需要在“Inputs”选项卡中将“Input 1”指向
// 我们想要获取的字段，在我们的例子中是“volume/pig_in”
// 这样我们还可以访问来自另一个 DOP 对象的字段
// (“volume”在这种情况下是我们的 DOP 对象)
// f@pig_in = volumesample(0, "pig_in", v@P)  *.9;

// if we want to sample from another position, we also need
// to set up "Input 1" properly
// note that you can also sample from volumes in SOPs if you
// specify path to it: set "Input 1" to *SOP* and point "SOP Path" 
// to the volume you want to access
// 如果我们想从另一个位置采样，我们还需要
// 正确设置“Input 1”
// 注意，如果你指定路径，你还可以从 SOPs 中的体积采样：
// 将“Input 1”设置为 *SOP* 并将“SOP Path”指向
// 你想要访问的体积
// f@pig_in = volumesample(0, "pig_in", v@P - {0.01});
```

#### DOPs / Gas Field Wrangle - accessing DOPs and SOPs data / DOPs / 气体场操作 访问 DOPs 和 SOPs 数据
```C
// it is also possible to access DOP fields using this syntax
// we can sample "pig_mask" without setting the field "Inputs"
// 还可以使用这种语法访问 DOP 字段
// 我们可以采样“pig_mask”而无需设置字段“Inputs”

float pig_mask = 0;
// the following lines below are identical, the second and third ones are more flexible as they use relative path:
// it will work even if we renamed this DOP network, the first line would not work after that
// the second argument is either an int representing primitive number, or string representing primitive name
// the syntax for accessing DOP data is: op:/DOP_node_path:dop_object_name/field_name
// 下面的几行是相同的，第二和第三行更灵活，因为它们使用相对路径：
// 即使我们重命名了这个 DOP 网络，它仍然有效，第一行在之后将不起作用
// 第二个参数可以是表示基本元素编号的整数，也可以是表示基本元素名称的字符串
// 访问 DOP 数据的语法是：op:/DOP_node_path:dop_object_name/field_name

pig_mask = volumesample("op:/obj/examples/dopnet_vex_vops_volume:volume/pig_mask", 0, v@P);
// pig_mask = volumesample("op:" + opfullpath("../") + ":volume/pig_mask", "pig_mask", v@P);
// pig_mask = volumesample("op:../" + ":volume/pig_mask", 0, v@P); // op: syntax also accepts relative paths
// pig_mask = volumesample("op:../" + ":volume/pig_mask", 0, v@P); // op: 语法也接受相对路径

// we can also directly access SOP volumes using this syntax
// 我们还可以使用这种语法直接访问 SOP 体积
// pig_mask = volumesample("op:../../IN_VOLUMES", 1, v@P);

f@pig_in *= 1-pig_mask;
```
![Gas Field Wrangle - DOPs and SOPs data](./img/gas_field_wrangle_dop_sop_data.jpg)

#### DOPs / Geometry workflow / DOPs / 几何体工作流程
Here I will show basic steps of creating a simple custom DOP solver operating on volumes.  
在这里，我将展示创建操作体积的简单自定义 DOP 求解器的基本步骤。

1. At first we need to create a *DOP Object*, which is a container that will contain all our fields (volumes in DOPs), geometry and any other data. Object name is important, because later we will use it to access our data.  
   首先，我们需要创建一个 *DOP Object*，这是一个容器，将包含我们所有的字段（DOPs 中的体积）、几何体和其他数据。对象名称很重要，因为稍后我们将使用它来访问我们的数据。
   ![DOP Object](./img/dop_object_box.jpg)
2. We can import a geometry from SOPs using *SOP Geometry* node. By enabling *Use External SOP* we can select a SOP we want to import. *Data Name* is usually set to *Geometry*.  
   我们可以使用 *SOP Geometry* 节点从 SOPs 导入几何体。通过启用 *Use External SOP*，我们可以选择要导入的 SOP。*Data Name* 通常设置为 *Geometry*。
   ![SOP Geometry](./img/sop_geometry.jpg)
3. If we want to use functions which take an input as an argument (looking up points, importing point attributes...) in [*Geometry Wrangle*](#dops--geometry-wrangle) or *Geometry VOP*, we need to set up our *Inputs* properly.  
   如果我们想使用将输入作为参数的函数（查找点、导入点属性...）在 [*Geometry Wrangle*](#dops--geometry-wrangle) 或 *Geometry VOP* 中，我们需要正确设置我们的 *Inputs*。
   ![Geometry Wrangle](./img/geo_wrangle_inputs.jpg)
   ![Geometry VOP](./img/geo_vop_inputs.jpg)
   Also note, that *Geometry Wrangle* and *Geometry VOP* have an option to use *Myself* in *Inputs* which is equivalent to previous settings.  
   另请注意，*Geometry Wrangle* 和 *Geometry VOP* 在 *Inputs* 中有一个选项使用 *Myself*，这与之前的设置等效。
   ![Geometry VOP Myself](./img/geo_vop_inputs_myself.jpg)
4. We can as well use *SOP Solver* to process our geometry in a SOP network.  
   我们还可以使用 *SOP Solver* 在 SOP 网络中处理我们的几何体。
   ![SOP Solver geo](./img/sop_solver_geo.jpg)

#### DOPs / Geometry Wrangle / DOPs / 几何体操作
*Check Houdini project to get the best idea of how it works.*  
*查看 Houdini 项目以获得最佳工作方式的了解。*
```C
// we can access attributes from "Geometry" data in our "box"
// object with this syntax
// however if we want to access other point's attributes, we need
// to properly set "Input 1" in "Inputs" tab of this node
// 我们可以使用这种语法从我们的“box”对象中的“Geometry”数据访问属性
// 但是如果我们想访问其他点的属性，我们需要
// 在这个节点的“Inputs”选项卡中正确设置“Input 1”
v@P *= 1.1;
```

#### DOPs / Geometry Wrangle - accessing fields / DOPs / 几何体操作 访问字段
[link to explanation](#dops--gas-field-wrangle---accessing-dops-and-sops-data)  
[链接到解释](#dops--gas-field-wrangle---accessing-dops-and-sops-data)
```C
// we can also access DOP fields from Geometry Wrangle, it is explained in:
// /obj/examples/dopnet_vex_vops_volume/gasfieldwrangle_accessing_DOPs_and_SOPs_data
// 我们还可以从 Geometry Wrangle 访问 DOP 字段，这在以下位置有解释：
// /obj/examples/dopnet_vex_vops_volume/gasfieldwrangle_accessing_DOPs_and_SOPs_data

// all following lines will produce the same result
// 以下所有行都会产生相同的结果
float mask = 0;
mask = volumesample("op:../" + ":box/pig_mask", 0, v@P);
// mask = volumesample("op:" + opfullpath("../") + ":box/pig_mask", "pig_mask", v@P);
// mask = volumesample("op:../../IN_VOLUMES", 1, v@P);

// visualize what points sampled non-zero density in the volume
// 可视化在体积中采样非零密度的点
if (mask != 0) v@Cd = {1,0,0};
```


#### Conditions / 条件
```C
// if there is only one statement after if condition, it
// can be written in the same line
// 如果 if 条件后只有一条语句，它
// 可以写在同一行
if (v@P.y < 0) v@Cd = {1,0,0};
// or in any other line, since VEX is not indented language,
// but this works only for one operation, else-if block will end with the first semicolon
// 或者在任何其他行，因为 VEX 不是缩进语言，
// 但这仅适用于一个操作，else-if 块将在第一个分号处结束
else if (v@P.x < 0) 
                    v@Cd = {0,1,0};
// to execute more operations, we need to use a block of code in {} brackets
// 要执行更多操作，我们需要在 {} 括号中使用代码块
else {
    v@Cd = {0,0,1};
    v@P += v@N;
}

// it is also possible to use conditional (ternary) operator with the following syntax
// (condition) ? true : false
// 还可以使用以下语法的条件（三元）运算符
// (条件) ? 真 : 假
v@P.x *= v@P.x > 0 ? 0.5 : 1.5;

// and use of logical AND: &&, OR: || is also possible
// 还可以使用逻辑与：&&，或：||
if (v@P.y < 0 && v@P.x > 0) v@P -= v@N * .3;
if (v@Cd == {0,0,1} || v@Cd == {1,0,0}) v@P += v@N * .4;
```

#### Loops / 循环
*Check Houdini project to get the best idea of how it works.*  
*查看 Houdini 项目以获得最佳工作方式的了解。*
```C
// VEX uses C-like syntax for for-loops
// VEX 对 for 循环使用类似 C 的语法
int valA = 2;
for (int i=0; i<11; i++) {
    valA *= 2;
}
i@valA = valA;

// for convenient iterating over elements of an array we
// can use foreach loop
// 为了方便遍历数组元素，我们
// 可以使用 foreach 循环
int nbs[] = nearpoints(0, v@P, .5);

vector P_avg = {0};
foreach(int nb_ptnum; nbs) {
    P_avg += point(0, "P", nb_ptnum);
}
P_avg /= len(nbs);

v@P = P_avg;

// we can also stop the loop at any point by using "break" keyword
// 我们还可以使用“break”关键字在任何点停止循环
int valB = 5;
for (int i=0; i<13; i++) {
    valB *= 5;
    if (valB > 10000000) break;
}

i@valB = valB;

// we can also use "continue" keyword to jump to the next loop iteration
// in this example we average point position with positions of neighbours
// which are above it in world space (their Y coordinate is larger)
// 我们还可以使用“continue”关键字跳到下一个循环迭代
// 在这个例子中，我们将点位置与世界空间中位于其上方的邻居位置平均
// （它们的 Y 坐标较大）
int pts[] = neighbours(0, @ptnum);

vector P_avg_upper = {0};
int count = 0;

foreach(int nb_ptnum; pts) {
    vector pos = point(0, "P", nb_ptnum);
    if (pos.y <= v@P.y) continue;
    P_avg_upper += pos;
    count++;
}

P_avg_upper /= count;
v@P = P_avg_upper;
```

#### Stopping For-Each SOP from VEX / 从 VEX 停止 For-Each SOP
```C
// in this example we are offsetting our points along X axis in each iteration
// 
// it is also possible to control For-Each SOP loop from VEX
// "Iterations" count in this loop is set to 300, however we want to stop the loop
// when our X coordinate is higher than 30
// to do so, we can use "Stop Condition" in the loop, when it equals to 1, the loop will end
// in this parameter we can use hscript expression checking for detail attribute
// and we can set this detail attribute from VEX
// hscript expression: detail("../attribwrangle_move_a_bit", "repeat", "0") == 0
// 在这个例子中，我们在每次迭代中沿 X 轴偏移我们的点
// 
// 还可以从 VEX 控制 For-Each SOP 循环
// 这个循环中的“Iterations”计数设置为 300，但是我们希望在 X 坐标大于 30 时停止循环
// 为此，我们可以在循环中使用“Stop Condition”，当它等于 1 时，循环将结束
// 在这个参数中，我们可以使用检查细节属性的 hscript 表达式
// 并且我们可以从 VEX 设置这个细节属性
// hscript 表达式：detail("../attribwrangle_move_a_bit", "repeat", "0") == 0

v@P.x += .3;

// if we comment out the line below, the loop will execute 300 times, otherwise it will execute
// only until our condition is met
// 如果我们注释掉下面的行，循环将执行 300 次，否则它将执行
// 直到我们的条件满足为止
if (v@P.x > 30) setdetailattrib(0, "repeat", 0, "set");
```

#### Printing and formatting / 打印和格式化
```C
// Windows - check console window which 
// should pop up automatically
// Linux - run Houdini from command line with 
// the -foreground flag to see the output
// Windows - 检查控制台窗口，
// 应该会自动弹出
// Linux - 从命令行运行 Houdini，
// 使用 -foreground 标志查看输出

// manipulating with strings is useful, not only for doing console outputs,
// but also for generating and stylizing strings, use sprintf() to return a string
// type instead of printing to console
// 操作字符串很有用，不仅用于控制台输出，
// 还用于生成和样式化字符串，使用 sprintf() 返回字符串
// 类型而不是打印到控制台

string var_string = "abcdef";
float var_float = 1.23456789;
int var_int = 256;

printf("string: %+10s, float: %10.3f, integer: %-6d \n", var_string, var_float, var_int);
// string = abcdef
// %[+-][length]s

// %10s -> ____abcdef
// %-10s -> abcdef____
// %+10s -> __"abcdef"
// %+-10s -> "abcdef"__

// float = 1.23456789
// %[+-][0][length][precision]f

// %8.3f -> ___1.235
// %-8.3f -> 1.235___
// %08.3f -> 0001.235
// %+8.3f -> __+1.235 (+ shows sign)

// integer = 256
// %[+-][0][length]d

// %6d -> ___256
// %+6d -> __+256
// %-6d -> 256___
// %06d -> 000256

printf("\n");

// escaping characters in string
// from my testing it requires 4 more backslashes to escape \n
// when using raw strings, they are automatically escaped, but @ symbol still
// needs to be escaped
// following lines will output the same thing
// 4 backslashes are needed probably because hscript is parsing this text field
// and sending to vop's field, see the node below
// 字符串中的转义字符
// 根据我的测试，转义 \n 需要额外的 4 个反斜杠
// 使用原始字符串时，它们会自动转义，但 @ 符号仍然
// 需要转义
// 以下行将输出相同的内容
// 可能需要 4 个反斜杠，因为 hscript 正在解析这个文本字段
// 并发送到 vop 的字段，参见下面的节点
string a = 'abc \\\\\n \\\\\t v\@P, %04.2f';
string b = "abc \\\\\n \\\\\t v\@P, %04.2f";
string c = r"abc \n \t v\@P, %04.2f";
string d = R"(abc \n \t v\@P, %04.2f)";

printf(a + "\n");
printf(b + "\n");
printf(c + "\n");
printf(d + "\n");

string multiLine = 
R"(It is possible to easily create multi
line strings with this syntax.
In some cases it might
be useful to do it this way,
rather than using \n
However as you have noticed it has weird
4 characters offset starting on the second line,
not sure if it is a bug or feature)";
// R"(可以使用这种语法轻松创建多
// 行字符串。
// 在某些情况下，这样做可能
// 很有用，
// 而不是使用 \n
// 然而，正如你所注意到的，从第二行开始有奇怪的
// 4 个字符偏移，
// 不确定是 bug 还是特性)";

printf(multiLine);

printf("\n\n");
```


#### Printing attributes / 打印属性
```C
printf("s\@shop_materialpath (string): %+s, v\@P (vector): %+-10.3f, \@ptnum (integer): %5d \n", s@shop_materialpath, v@P, @ptnum);

printf("\n\n");
```

#### Including external VEX files / 包含外部 VEX 文件
```C
#include "myLib.h"

// files located in $HIP/vex/include,
// $HOME/houdiniXX.X/vex/include,
// $HH/vex/include
// can be included in wrangles
// 位于 $HIP/vex/include,
// $HOME/houdiniXX.X/vex/include,
// $HH/vex/include
// 的文件可以包含在 wrangles 中

// to refresh updated header files, 
// promote the "Force Compile" button 
// from the attribvop1 node inside of this node, 
// or do a change (add a space somewhere) 
// in the code and press Ctrl+Enter
// 要刷新更新的头文件，
// 提升这个节点内的 attribvop1 节点的“Force Compile”按钮，
// 或者在代码中进行更改（在某处添加空格）
// 并按 Ctrl+Enter

myRemPoints(@ptnum);
```
*From myLib.h:*  
*来自 myLib.h：*
```C
// void functions do not return anything
// "function" keyword is not required
// void 函数不返回任何内容
// “function”关键字不是必需的
function void myRemPoints(int ptnum) {
    if (ptnum > 30)
        removepoint(0, ptnum);
}
```

#### Include math.h / 包含 math.h
```C
#include "math.h"

// This include file contains useful math constant macros
// and is available to every Houdini setup :)
// You can use couple of constants like
// e, pi, sqrt(2)...
//
// check the file at $HH/vex/include/math.h or end of this wrangle
// 这个包含文件包含有用的数学常数宏
// 并且对每个 Houdini 设置都可用 :)
// 你可以使用一些常数，如
// e, pi, sqrt(2)...
//
// 查看 $HH/vex/include/math.h 文件或这个 wrangle 的末尾

f@pi = M_PI;
f@e = M_E;
f@log2e = M_LOG2E;

// XFORM_SRT and XFORM_XYZ are also constants set to values that functions 
// maketransform() and cracktransform() expect, they define order of transformations
// and axes
// XFORM_SRT 和 XFORM_XYZ 也是设置为函数 maketransform() 和 cracktransform() 期望的值的常数，
// 它们定义变换和轴的顺序

vector tr = {3,4,5};
vector rot = {0,M_PI,0};
vector scale = {2,1,2};
matrix xform = maketransform(XFORM_SRT, XFORM_XYZ, tr, rot, scale);

// v@tr_check attribute will match original tr variable
// v@tr_check 属性将匹配原始 tr 变量
v@tr_check = cracktransform(XFORM_SRT, XFORM_XYZ, 0, {0}, xform);

v@P *= xform; // apply transformation
// v@P *= xform; // 应用变换

/*
part of the $HH/vex/include/math.h file:
// $HH/vex/include/math.h 文件的一部分：

#define M_E             2.7182818
#define M_LN10          2.3025850
#define M_LN2           0.6931471
#define M_LOG10E        0.4342944
#define M_LOG2E         1.4426950
#define M_PI            3.1415926
#define M_TWO_PI        6.2831852
#define M_PI_2          1.5707963
#define M_PI_4          0.7853981
#define M_SQRT1_2       0.7071067
#define M_SQRT2         1.4142135
#define M_TOLERANCE     0.0001

#define M_2SQRT6_3  1.6329931618554518  // 2 * sqrt(6) / 3
#define M_SQRT3     1.7320508075688772  // sqrt(3)
#define M_1_SQRT3   0.5773502691896257  // 1 / sqrt(3)
#define M_SQRT_2_3  0.816496580927726   // sqrt(2 / 3)

#define XFORM_SRT       0       // Scale, Rotate, Translate
#define XFORM_STR       1       // Scale, Translate, Rotate
#define XFORM_RST       2       // Rotate, Scale, Translate
#define XFORM_RTS       3       // Rotate, Translate, Scale
#define XFORM_TSR       4       // Translate, Scale, Rotate
#define XFORM_TRS       5       // Translate, Rotate, Scale

#define XFORM_XYZ       0       // Rotate order X, Y, Z
#define XFORM_XZY       1       // Rotate order X, Z, Y
#define XFORM_YXZ       2       // Rotate order Y, X, Z
#define XFORM_YZX       3       // Rotate order Y, Z, X
#define XFORM_ZXY       4       // Rotate order Z, X, Y
#define XFORM_ZYX       5       // Rotate order Z, Y, X
*/
```

#### Using macros / 使用宏
```C
#include "myLib.h"

// check attributes in Geometry Spreadsheet, 
// they will match values from myLib.h
// 在 Geometry Spreadsheet 中检查属性，
// 它们将与 myLib.h 中的值匹配

// use constants
// 使用常数
i@my_int = MY_INT;
f@my_float = MY_FLOAT;

// use function alias
// 使用函数别名
f@renamed_power = RENAMEDPOWER(2,2);

// use macro function
// 使用宏函数
i@add_ten = ADDTEN(10);
```
*From myLib.h:*  
*来自 myLib.h：*
```C
// you can use macros to define constants and use them in your code
// 你可以使用宏来定义常数并在代码中使用它们
#define MY_INT          123
#define MY_FLOAT        3.1415926

// you can also create alias to the function
// 你还可以为函数创建别名
#define RENAMEDPOWER    pow

// or use macros for defining new functions
// 或者使用宏来定义新函数
#define ADDTEN(val)     (val+10)
```


#### Functions / 函数
```C
#include "myLib.h"

// void does not return anything
// void 不返回任何内容
myRemPoints(@ptnum);

// arguments are passed by reference - function can modify their original value
// 参数按引用传递 - 函数可以修改它们的原始值
scaleByTen(v@P);

// you can prevent voids from modifying variable references
// just to be safe :)
// 你可以防止 void 修改变量引用
// 只是为了安全起见 :)
int a = 1;
int b = 1;
int c = 1;
changeA(a, b, c);
i@a = a;
i@b = b;
i@c = c;

// functions can also return different types - float, string, int, custom struct...
// they can also return an array of any of those types
// 函数还可以返回不同的类型 - float, string, int, 自定义 struct...
// 它们还可以返回这些类型的数组
vector4 seeds = {1.23,4,56.489,0.849};
f@superRandom = superRandom(seeds);

// function returning array of int(s)
// 返回 int 数组的函数
int items = 9;
i[]@items = range(items);
```
*From myLib.h:*  
*来自 myLib.h：*
```C
// void functions do not return anything
// "function" word is not required
// void 函数不返回任何内容
// “function”单词不是必需的
function void myRemPoints(int ptnum) {
    if (ptnum > 30)
        removepoint(0, ptnum);
}

// function parameters are passed by reference automatically, without additional syntax
// (function receive the original variable, not its copy)
// 函数参数自动按引用传递，不需要额外的语法
// （函数接收原始变量，而不是其副本）
void scaleByTen(vector P) {
    P *= 10;
}

// you can prevent changing input variable references
// 你可以防止更改输入变量引用
void changeA(int a; const int b; int c) {
    a += 10;
    // b += 10; // uncommenting this line will result in error
    // b += 10; // 取消注释这行将导致错误
    c = a;
    c += 4; // even though arguments are passed by reference, they are not true references, "c" is still independent from "a"
    // c += 4; // 尽管参数按引用传递，但它们不是真正的引用，“c”仍然独立于“a”
}

// a function returning float value
// 返回浮点值的函数
float superRandom(vector4 seeds) {
    float out = rand(seeds.x * seeds.y * seeds.z * seeds.w);
    return out;
}

// a function returning an array
// 返回数组的函数
int[] range(int max) {
    int out[];

    for(int i=0; i<max; i++) push(out, i);

    return out;
}
```

#### Functions overloading / 函数重载
```C
#include "myLib.h"

float rand = chf("randomness");

// visualize Normals in the viewport to see the effect
// 在视口中可视化法线以查看效果
// v@N = randomizeN(v@N, rand, @ptnum + @Frame); // randomizeN(vector, float, float)
// v@N = randomizeN(v@N, rand, @ptnum + @Frame); // randomizeN(vector, float, float)

// however we can overload our function to accept different set of arguments
// 但是我们可以重载我们的函数以接受不同的参数集
vector4 seed;
seed = set(v@P.x, v@P.y, v@P.z, @ptnum * @Frame);
// seed = set(v@P, @ptnum * @Frame); // this does not work as might be expected
// seed = set(v@P, @ptnum * @Frame); // 这不像预期的那样工作
v@N = randomizeN(v@N, rand, seed); // randomizeN(vector, float, vector4)
// v@N = randomizeN(v@N, rand, seed); // randomizeN(vector, float, vector4)

// we can also overload functions to return different type
// 我们还可以重载函数以返回不同的类型
float randVal;
randVal = float( randomizeN(v@N, rand, @ptnum) );
// randVal = randomizeN(v@N, rand, @ptnum); // this has the same result now, but sometimes VEX might choose another function
// randVal = randomizeN(v@N, rand, @ptnum); // 现在这有相同的结果，但有时 VEX 可能会选择另一个函数
v@Cd = randVal;
// v@Cd = set(randVal, randVal, randVal); // this is equivalent to the previous line
// v@Cd = set(randVal, randVal, randVal); // 这与前一行等效

p@a = set(v@P.x, v@P.y, v@P.z, 4);
// p@a = set(v@P, 4); // uncomment this line and see the difference in geometry spreadsheet
// p@a = set(v@P, 4); // 取消注释这行并查看几何电子表格中的差异
```
*From myLib.h:*  
*来自 myLib.h：*
```C
// normalize Normal vector by amount [0..1] with specified seed value
// 用指定的种子值按数量 [0..1] 归一化法线向量
vector randomizeN(vector N; float amount, seed) {
    vector randDir;
    
    // getting different random value for each axis, scaling to [-1..1] range
    // 为每个轴获取不同的随机值，缩放到 [-1..1] 范围
    randDir.x = rand(seed * 684.49848) * 2 - 1;
    randDir.y = rand(seed * 178.46548) * 2 - 1;
    randDir.z = rand(seed * 489.49856) * 2 - 1;
    
    randDir = normalize(randDir);

    N = lerp(N, randDir, amount);
    N = normalize(N);

    return N;
}

// function has different set of parameters, but the same name
// 函数具有不同的参数集，但名称相同
vector randomizeN(vector N; float amount; vector4 seed) {
    vector randDir;
    
    // getting different random value for each axis, scaling to [-1..1] range
    // 为每个轴获取不同的随机值，缩放到 [-1..1] 范围
    randDir.x = rand(seed.x * 684.49848 * seed.w) * 2 - 1;
    randDir.y = rand(seed.y * 178.46548 * seed.w) * 2 - 1;
    randDir.z = rand(seed.z * 489.49856 * seed.w) * 2 - 1;
    
    randDir = normalize(randDir);

    N = lerp(N, randDir, amount);
    N = normalize(N);

    return N;
}

// this function declaration returns different type
// the function name does not really match its functionality, it is just for the example
// 这个函数声明返回不同的类型
// 函数名称与其功能并不真正匹配，仅用于示例
float randomizeN(vector N; float amount; int seed) {
    float randDir;
    
    // getting different random value for each axis, scaling to [-1..1] range
    // 为每个轴获取不同的随机值，缩放到 [-1..1] 范围
    randDir = rand((float)seed * 684.49848) * 2 - 1;

    return randDir;
}
```


#### Variables casting / 变量转换
```C
#include "myLib.h"

int myPt = @ptnum;
int maxPts = @numpt-1;

float color;

// by casting to float, we can do float division, which is more helpful in our case
// 通过转换为 float，我们可以进行浮点除法，这对我们来说更有帮助
color = float(myPt) / (float)maxPts; // for variables both syntaxes are valid
// color = float(myPt) / maxPts; // it is also valid as the other variable (does not matter which one) will be upcasted to float
// color = float(myPt) / maxPts; // 这也是有效的，因为另一个变量（无论哪一个）将被提升为 float

// dividing integer by integer produces integer, it is not what we need
// 整数除以整数产生整数，这不是我们需要的
// color = myPt / maxPts;

color = pow(color, 3); // make color more contrasty
// color = pow(color, 3); // 使颜色更具对比度

// assigning a float to vector will assign uniform vector: { color, color, color }
// 将 float 赋值给 vector 将分配均匀向量：{ color, color, color }
v@Cd = color;
```

#### Vectors swizzling / 向量重组
```C
vector col = {.1, .3, .7};

col = col.zzy; // this syntax is equivalent to the following line
// col = col.zzy; // 这种语法等同于以下行
// col = set( col.z, col.z, col.y );
// col = set( col.z, col.z, col.y );

// reversing order of vector elements had never been easier :)
// 反转向量元素的顺序从未如此简单 :)
// col = {.1, .2, .3};
// col = col.zyx;

// swizzling is not however as powerful as in other graphics languages
// e.g. following lines do not work as expected, or at all
// 然而，重组在其他图形语言中并不那么强大
// 例如，以下行按预期不起作用，或者根本不起作用
// col.zyx = col.xyz;
// col.xy = col.yx;

v@Cd = col;
```

#### Functions casting / 函数转换
```C
#include "myLib.h"

// this line results in an error, because dot() is expecting two vectors
// and rand() is overloaded - it can return float, vector, vector2, vector4
// 这行导致错误，因为 dot() 期望两个向量
// 而 rand() 是重载的 - 它可以返回 float, vector, vector2, vector4
// v@Cd = dot(v@N, normalize( rand(@ptnum)  ) ) * 0.5 + 0.5;

// here we are explicitly asking for rand() function which is returning a vector
// 这里我们明确要求返回向量的 rand() 函数
v@Cd = dot(v@N, normalize( vector( rand(@ptnum) ) ) ) * 0.5 + 0.5;

// this will not work as length() is expecting a vector
// 这不起作用，因为 length() 期望一个向量
// v@Cd = length( rand(v@P) );

// this now works fine
// 这现在工作正常
// v@Cd = length( vector( rand(v@P) ) ) * .5;
```


#### Structs / 结构体
```C
#include "myLib.h"
// in this node I will show some examples of using structs, they will be defined in myLib.h
// for defining structs inside a wrangle, see node below
// 在这个节点中，我将展示一些使用结构体的例子，它们将在 myLib.h 中定义
// 要在 wrangle 内定义结构体，请参见下面的节点

// declare struct variable, member variables will have default values
// 声明结构体变量，成员变量将具有默认值
myCustomMatrix A;
myCustomMatrix B;

// change values of member variables in A
// 更改 A 中成员变量的值
A.uniformScale = 2.5;
A.comment = "a very useful struct";
pop(A.myArray);
pop(A.myArray);
push(A.myArray, 7);

// check Geometry Spreadsheet for values of variables in A and B
// 在 Geometry Spreadsheet 中检查 A 和 B 中变量的值
f@myPiA = A.myPi; // 3.14
f@myPiB = B.myPi; // 3.14
f@uniformScaleA = A.uniformScale; // 2.5
f@uniformScaleB = B.uniformScale; // 1.0
s@commentA = A.comment; // a very useful struct
s@commentB = B.comment; // default comment
f[]@myArrayA = A.myArray; // [ 1.0, 7.0 ]
f[]@myArrayB = B.myArray; // [ 1.0, 3.0, 3.0 ]
v@xA = A.x; // {0,0,0}
v@xB = B.x; // {0,0,0}

// one way of initializing a struct (as explicit struct)
// 初始化结构体的一种方式（作为显式结构体）
hipFile myProjectA = {"project_A", "hipnc", 1};
s@baseA = myProjectA.base; // project_A
s@extA = myProjectA.ext; // hipnc
i@verA = myProjectA.version; // 1

// another way (initialize using constructor)
// 另一种方式（使用构造函数初始化）
hipFile myProjectB = hipFile("project_B", "hip", 1);
s@baseB = myProjectB.base; // project_B
s@extB = myProjectB.ext; // hip
i@verB = myProjectB.version; // 1

// you can call methods (member functions) in structs with -> operator
// 你可以使用 -> 运算符调用结构体中的方法（成员函数）
int versionA = myProjectA->incVersion();
versionA = myProjectA->incVersion();
versionA = myProjectA->incVersion();

int versionB = myProjectB->incVersion();

// printName is our another struct method,
// check your terminal output
// printName 是我们的另一个结构体方法，
// 检查你的终端输出
myProjectA->printName(); // this file has name: project_A_004.hipnc
myProjectB->printName(); // this file has name: project_B_002.hip

// we can use functions operating on our structs and accessing their data
// 我们可以使用操作我们的结构体并访问其数据的函数
i@match1 = compareHipFiles(myProjectA, myProjectB); // 0

// now let's make them identical
// 现在让我们使它们相同
myProjectB.base = "project_A";
myProjectB.ext = "hipnc";
myProjectB.version = 4;

// and check if they really are :)
// 并检查它们是否真的相同 :)
i@match2 = compareHipFiles(myProjectA, myProjectB); // 1

// we can also create functions which return hipFile type
// this function expects comma separated list of files and will return
// first occurrence of a hip file (with .hip or .hipnc extension)
// 我们还可以创建返回 hipFile 类型的函数
// 这个函数期望逗号分隔的文件列表，并将返回
// 第一个 hip 文件的出现（具有 .hip 或 .hipnc 扩展名）
string files1 = "image1.jpg,image2.png,text.pdf,awesome_tutorial_jtomori_003.hipnc,tutorial.h";

hipFile first = findFirstHipFile(files1);
s@first = first->getFullName();

// in VEX we can also output error with custom message, uncomment the line below and check
// node's error message
// 在 VEX 中，我们还可以输出带有自定义消息的错误，取消下面行的注释并检查
// 节点的错误消息
string files2 = "image1.jpg,image2.png";
// hipFile second = findFirstHipFile(files2); // No houdini project found in this file list: "image1.jpg,image2.png".
// hipFile second = findFirstHipFile(files2); // 在此文件列表中未找到 houdini 项目：“image1.jpg,image2.png”。

// we can also output an array of hipFiles
// this function will find all Houdini project files and will return array of hipFile(s)
// 我们还可以输出 hipFiles 数组
// 这个函数将找到所有 Houdini 项目文件并返回 hipFile(s) 数组
string files3 = "dust_024.hip,img7.tif,odforce_file_001.hipnc,render1.exr,blood_123.hip,notes.txt";
hipFile allHips[] = findAllHipFiles(files3);

// let's check it by adding it into a string array attribute
// 让我们通过将其添加到字符串数组属性中来检查它
s[]@allHips;
foreach(hipFile i;allHips) {
    push(s[]@allHips, i->getFullName());
}
// result: [ dust_024.hip, odforce_file_001.hipnc, blood_123.hip ]
// 结果：[dust_024.hip, odforce_file_001.hipnc, blood_123.hip]
```


*From myLib.h:*  
*来自 myLib.h：*
```C
// vex also supports structs and methods associated with them
// vex 还支持结构体及其相关方法
struct myCustomMatrix {
    // uninitialized variables
    // 未初始化的变量
    vector x, y, z;
    
    // variables with default values
    // 具有默认值的变量
    vector translate = {0,0,0};
    string comment = 'default comment';
    float myPi = 3.14159265;
    float uniformScale = 1.0;
    float myArray[] = {1,2,3};
}

// struct for carrying information about our project file
// 用于携带我们项目文件信息的结构体
struct hipFile {
    string base, ext;
    int version = 1;

    // you can create methods that operate on structs
    // this method increases version by 1 and returns new version number
    // 你可以创建操作结构体的方法
    // 此方法将版本增加 1 并返回新版本号
    int incVersion() {
        this.version++;
        return this.version;
    }

    // inside of a struct function, you can refer to struct fields by name as if they 
    // were variables (for example, base is a shortcut for this.base).
    // this method writes to console window / terminal
    // 在结构体函数内部，你可以按名称引用结构体字段，就像它们是变量一样（例如，base 是 this.base 的快捷方式）。
    // 此方法写入控制台窗口/终端
    void printName() {
        printf("this file has name: %s_%03d.%s\n", base, version, ext);
    }

    // returns a string with full file name
    // 返回带有完整文件名的字符串
    string getFullName() {
        return sprintf("%s_%03d.%s", this.base, this.version, this.ext);
    }
}

// we can create functions that operate on our structs and use their methods
// 我们可以创建操作我们的结构体并使用其方法的函数
int compareHipFiles(hipFile A, B) {
    int match = 0;
    if (A->getFullName() == B->getFullName()) match = 1;

    return match;
}

// func returning hipFile type
// this function expects comma separated list of filenames and will 
// return the first occurrence of a hip file
// 返回 hipFile 类型的函数
// 此函数期望逗号分隔的文件名列表，并将
// 返回第一个 hip 文件的出现
hipFile findFirstHipFile(string text) {
    string inFiles[] = split(text, ",");
    string hipParts[];

    foreach(string file; inFiles) {
        string parts[] = split(file, ".");
        if (parts[-1] == "hip" || parts[-1] == "hipnc") {
            hipParts = parts;
            break;
        }
    }

    // we can also return error state, warning() function is also available
    // 我们还可以返回错误状态，warning() 函数也可用
    if (len(hipParts) == 0) error("No houdini project found in this file list: %+s.", text);

    string prefix[] = split(hipParts[0], "_");
    int ver = atoi( prefix[-1] );
    string base = join( prefix[:-1], "_");
    string ext = hipParts[1];

    hipFile out = hipFile(base, ext, ver);
    return out;
}

// we can as well return an array of structs
// 我们还可以返回结构体的数组
hipFile[] findAllHipFiles(string text) {
    string inFiles[] = split(text, ",");
    hipFile hips[];

    foreach(string file; inFiles) {
        string parts[] = split(file, ".");
        if (parts[-1] == "hip" || parts[-1] == "hipnc") {
            string prefix[] = split(parts[0], "_");
            int ver = atoi( prefix[-1] );
            string base = join( prefix[:-1], "_");
            string ext = parts[1];

            hipFile out = hipFile(base, ext, ver);
            push(hips, out);
        }
    }

    // output a warning when no Houdini projects were found
    // 当未找到 Houdini 项目时输出警告
    if (len(hips) == 0) warning("No Houdini projects found.");

    return hips;
}
```


#### Structs in Attribute Wrangle / 属性操作中的结构体
```C
// VEX does not allow defining structs inside this field, they need to be defined
// externally, either in a .h file, or in "Outer Code" string parameter of "snippet1"
// which is inside of every Wrangle node (this > attribvop1 > snippet1)
// in this case I unlocked the wrangle and promoted "Outer Code" parameter from 
// the inside of snippet1 to this wrangle
// VEX 不允许在这个字段内定义结构体，它们需要
// 在外部定义，可以在 .h 文件中，也可以在每个 Wrangle 节点内的“snippet1”的“Outer Code”字符串参数中
// （this > attribvop1 > snippet1）
// 在这种情况下，我解锁了 wrangle 并从 snippet1 内部提升了“Outer Code”参数到这个 wrangle

hipFile A = hipFile("awesome_vex_examples_file","hipnc",3);
s@A = A.base;

// uncommenting of the following lines will result in an error
// 取消注释以下行将导致错误
/*
struct hipFileB {
        string base, ext;
        int version = 1;
}
*/

// Outer Code behaves just like a .h file included
// Outer Code 的行为就像包含的 .h 文件一样
i@my_int = MY_INT;
```
*Outer Code*  
*外部代码*
```C
struct hipFile {
        string base, ext;
        int version = 1;
}

#define MY_INT  123456
```

#### Groups / 组
```C
// it is also possible to manipulate group membership through VEX, group names
// are bound by default with i@group_name syntax (int value: 0 - not member, 1 - member)
// you can disable it in "Bindings" tab of Wrangle node with "Autobind Groups by Name"
// 还可以通过 VEX 操作组成员资格，组名称
// 默认情况下与 i@group_name 语法绑定（整数值：0 - 不是成员，1 - 是成员）
// 你可以在 Wrangle 节点的“Bindings”选项卡中通过“Autobind Groups by Name”禁用它

// it is also possible to create new groups, they are created automatically like attributes
// in the following line we assign all points that belong to "selected" group to "red" group
// 还可以创建新组，它们像属性一样自动创建
// 在以下行中，我们将属于“selected”组的所有点分配到“red”组
i@group_red = i@group_selected;

// all points, that have positive X coordinate will belong to "green" group
// 所有具有正 X 坐标的点将属于“green”组
i@group_green = v@P.x > 0 ? 1 : 0;
// except those, which are already in "red" group
// 除了那些已经在“red”组中的点
i@group_green = i@group_green && !i@group_red ? 1 : 0;
// i@group_name can have two values and can be treated as a boolean, the following line
// has the same effect as the previous one
// i@group_name 可以有两个值，可以视为布尔值，以下行
// 与前一行有相同的效果
// i@group_green = i@group_green == 1 && i@group_red == 0 ? 1 : 0;
```
Group mirror  
组镜像
```C
// groups in VEX are very helpful as we can use VEX functions to do our own group logic
// in this example we mirror red group along X axis and will assign it to "blue" group
// VEX 中的组非常有用，因为我们可以使用 VEX 函数来实现自己的组逻辑
// 在这个例子中，我们沿 X 轴镜像 red 组，并将其分配到“blue”组

int pt_reflected = nearpoint(0, set(-v@P.x, v@P.y, v@P.z) );
int pt_group_red = inpointgroup(0, "red", pt_reflected);

i@group_blue = pt_group_red;
```


#### Attribute typeinfo / 属性类型信息
```C
/*
It is possible to assign a meaning to attributes. Houdini will understand this meaning and
will treat attributes in a specific way based on it. For example a Transform SOP operates
on P attribute, but will also modify N attribute accordingly. For modifying this behavior 
we can use setattribtypeinfo() function which can set typeinfo to attributes.
You can check which typeinfo an attribute has by middle-clicking on a node and checking value
in brackets, e.g. P (pos) - this means point typeinfo

You can check list of available typeinfos in the docs, or below:
none - No transformations should be applied.
point - Scales, rotations and translations should be applied.
hpoint - A four-vector with scales, rotations and translations applied.
vector - Scales and rotations should be applied.
normal - Scales and rotations should be applied. Scales are applied with inverse-transpose.
color - No transformations.
matrix - A 4×4 matrix with scale, rotations, and translations applied.
quaternion - A four-vector with rotations applied.
indexpair - No transformations.
integer - Integer values that do not blend when points are averaged.
integer-blend - Integer values that blend when points are averaged.
*/
/*
可以为属性赋予意义。Houdini 将理解这种意义并
根据它以特定方式处理属性。例如，Transform SOP 操作
P 属性，但也会相应地修改 N 属性。为了修改这种行为
我们可以使用 setattribtypeinfo() 函数，它可以为属性设置 typeinfo。
你可以通过中键单击节点并检查括号中的值来查看属性具有的 typeinfo，
例如 P (pos) - 这意味着 point typeinfo

你可以在文档中查看可用 typeinfo 的列表，或在下面查看：
none - 不应应用任何变换。
point - 应应用缩放、旋转和平移。
hpoint - 一个四向量，应用了缩放、旋转和平移。
vector - 应应用缩放和旋转。
normal - 应应用缩放和旋转。缩放应用逆转置。
color - 无变换。
matrix - 一个 4×4 矩阵，应用了缩放、旋转和平移。
quaternion - 一个四向量，应用了旋转。
indexpair - 无变换。
integer - 整数值，在点平均时不混合。
integer-blend - 整数值，在点平均时混合。
*/

// set color to green
// 将颜色设置为绿色
v@Cd = {0,1,0};

// initialize N attribute, which will get automatically get values
// 初始化 N 属性，它将自动获取值
v@N;

// change typeinfos of Cd and N to see funky results after modifying geometry with Transform SOP
// 更改 Cd 和 N 的 typeinfo，以在用 Transform SOP 修改几何体后看到有趣的结果
setattribtypeinfo(0, "point", "Cd", "point");
setattribtypeinfo(0, "point", "N", "color");
```

#### Attributes to create / 要创建的属性
```C
// when dealing with more code you might often run into
// errors caused by typos, when you mistype an attribute
// name, VEX will automatically initialize a new one
// like in the following example
// 在处理更多代码时，你可能经常会遇到
// 由拼写错误引起的错误，当你拼错属性
// 名称时，VEX 将自动初始化一个新的
// 就像在下面的例子中一样
v@Cd = {1,0,1};

// to avoid this kind of errors, we can specify which attributes
// to create, in "Attributes to Create" parameter of a Wrangle
// e.g. the following line will result in a node error, because
// we did not specify to create a "n" attribute
// 为了避免这类错误，我们可以指定要创建的属性
// 在 Wrangle 的“Attributes to Create”参数中
// 例如，以下行将导致节点错误，因为
// 我们没有指定创建“n”属性
// v@n = {0,1,0};
```

#### Enforce prototypes / 强制原型
```C
// If we want to be even more organized, we can use "Enforce Prototypes" option 
// in Wrangles, it is handy with larger code projects as it helps with 
// managing attributes and simplifies syntax for accessing them (especially with arrays)
// 如果我们想更有条理，我们可以使用 Wrangles 中的“Enforce Prototypes”选项
// 在大型代码项目中很方便，因为它有助于
// 管理属性并简化访问它们的语法（特别是数组）

// initialize attribute "Prototypes" - here we need to specify all attributes
// that we want to use/create, it also applies to default/global attributes 
// like v@P, @Frame, @ptnum
// 初始化属性“Prototypes” - 这里我们需要指定所有
// 我们想要使用/创建的属性，它也适用于默认/全局属性
// 如 v@P, @Frame, @ptnum
vector @P;
vector @Cd;
int @ptnum;
float @Frame;
float @new_attrib = 4; // we can also set initial value, but without any expressions
// float @new_attrib = 4; // 我们还可以设置初始值，但不带任何表达式
int @new_int_array_attrib[];

// we can still use local variables in a standard way
// 我们仍然可以以标准方式使用局部变量
float A = @Frame * .5;
int B = 4;

// now we can use attributes without their signature before @ sign
// 现在我们可以在 @ 符号前使用属性，而不需要它们的签名
@P += set(0, B, 0);
@Cd *= rand(@ptnum);
@new_attrib *= A;
@new_int_array_attrib = {1,2,3,4};
```


#### Attribute default values / 属性默认值
```C
// It is also possible to set default values for attributes from VEX.
// It replicates behavior of "Default" parameter in Attribute Create SOP,
// it means that when we create a new geometry (without passing current ptnum
// to addpoint() function to copy all attributes), it will have those default
// values. Otherwise it will be usually set to 0, or 1 in case of Cd.
// The same applies for merging in a geometry, which does not have the attribute,
// the attribute will be added with default values which we specified.
// Note that defaults do not work with string attributes, it is a known limitation.
// 还可以从 VEX 为属性设置默认值。
// 它复制了 Attribute Create SOP 中“Default”参数的行为，
// 这意味着当我们创建新几何体时（不将当前 ptnum 传递给 addpoint() 函数以复制所有属性），
// 它将具有这些默认值。否则通常会设置为 0，或者在 Cd 的情况下设置为 1。
// 对于合并不具有该属性的几何体也是如此，
// 该属性将以我们指定的默认值添加。
// 请注意，默认值不适用于字符串属性，这是一个已知的限制。

// Default values can be set with Attribute Prototypes which were mentioned in
// the previous node. Any new geometry will have those default values.
// 默认值可以使用之前节点中提到的 Attribute Prototypes 设置。
// 任何新几何体都将具有这些默认值。
vector @Cd = {1,0,0};
int @id = 4; //@Frame or other expressions will not work
// int @id = 4; //@Frame 或其他表达式将不起作用

string @default = "abc"; // defaults for strings are not supported yet
// string @default = "abc"; // 字符串的默认值尚不受支持

// Let's create couple of copies of our points
// 让我们创建我们的点的几个副本
vector offset = {0,8,0};
for (int i = 0; i < 3; i++)
    addpoint(0, v@P + offset * (i + 1));

// Original sphere will have this value set to 7, while new points will have
// default value 0
// 原始球体将此值设置为 7，而新点将具有
// 默认值 0
f@pscale = 7.0;

// This will set id attribute to zero only on input geometry, new geometry will 
// have default value 4
// 这将仅在输入几何体上将 id 属性设置为零，新几何体将
// 具有默认值 4
i@id = 0;
```

### Todo / 待办事项
* any suggestions? :)  
* 有任何建议吗？ :)

### Resources & More / 资源与更多内容
In this tutorial I am focusing on VEX syntax, capabilities and integration in Houdini.  
For more practical and visual VEX examples check [Matt Estela's awesome wiki](http://www.tokeru.com/cgwiki/?title=HoudiniVex)  
Another good source is *$HH/vex/include* folder which is full of VEX include files with many useful functions. *( $HH expands to /houdini_install_dir/houdini/ )*  
Make sure to watch this very cool [VEX Masterclass](https://vimeo.com/173658697) by Jeff Wagner.  
VEX is well documented, [language reference](http://www.sidefx.com/docs/houdini/vex/lang) and [functions](http://www.sidefx.com/docs/houdini/vex/functions/index.html) pages are very helpful too.  
在本教程中，我专注于 VEX 语法、能力和在 Houdini 中的集成。  
要获取更多实用和视觉化的 VEX 示例，请查看 [Matt Estela 的精彩 wiki](http://www.tokeru.com/cgwiki/?title=HoudiniVex)  
另一个很好的资源是 *$HH/vex/include* 文件夹，其中包含了许多有用的函数的 VEX 包含文件。*($HH 扩展为 /houdini_install_dir/houdini/ )*  
一定要观看 Jeff Wagner 的这个非常酷的 [VEX 大师班](https://vimeo.com/173658697)。  
VEX 文档齐全，[语言参考](http://www.sidefx.com/docs/houdini/vex/lang) 和 [函数](http://www.sidefx.com/docs/houdini/vex/functions/index.html) 页面也非常有帮助。

### Feedback & Suggestions / 反馈与建议
Please let me know if you find any mistakes or have ideas for improvements. I will fix it and push it to this repo :)  
如果您发现任何错误或有改进的想法，请告诉我。我会修复它并推送到这个仓库 :)

### Contributing / 贡献
Feel free to contribute to this project by creating pull requests or by [buying me a beer :)](https://www.paypal.me/jtomori)  
欢迎通过创建拉取请求或[请我喝杯啤酒 :)](https://www.paypal.me/jtomori) 来为这个项目做出贡献