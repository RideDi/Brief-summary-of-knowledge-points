# Smali语法

Smali修改APP逻辑时需要用

### 文件结构

一个Smali对应一个Java类(.class)文件，如果内部类，需要写ClassName$InnerClassA\ClassName$InnerNameB

### 基本类型

| 关键字 | 对应Java类型 |
| ------ | ------------ |
| V      | void         |
| Z      | boolean      |
| B      | Byte         |
| S      | String       |
| C      | Char         |
| I      | int          |
| J      | long         |
| F      | float        |
| D      | Double       |

### 对象

Object类型，引用类型的对象，引用时L开头，跟完整包名java.lang.String->Ljava/lang/string

### 数组

一维数组在类型的左边加一个方括号，比如：`[I`等同于Java的`int[]`，每多一维就加一个方括号

### 方法声明调用

```Smali
Lpacket/name/ObjectName;->MethodName(III)Z
```

Lpacket/name/ObjectName;声明具体类型

MethodName(III)Z具体的名字()表示参数数量和类型，III位三个int型

### 寄存器

存储变量先声明寄存器，1个寄存器存储32位长度的类型Eg：int  2个寄存器64位Eg：Double/Long

声明寄存器数量方式：.register N N代表数量，还有个关键字  .locals用于声明非寄存器的个数(包含在Register声明的个数中)也叫本地寄存器，只在一个方法内有效

```
.method private test(I)V
	.register 4 //声明总共需要4个寄存器
	
	const-string v0, "LOG" //将v0寄存器赋值为"LOG"
	
	move v1,p1. //int型参数的值赋值给v1寄存器
	
	return-void
.end method
```

#### 如何确定需要的寄存器个数？

由于非static方法需要占用一恶搞寄存器保存this指针，这类方法最少一个寄存器，如果需要处理传入的参数，需要再次叠加，还要考虑double或者long

java方法

```java
myMethod(int p1, float p2, boolean p2)
```

对应的Smali方法

```smali
method LMyObject;->myMethod(IJZ)V
```

寄存器状况

| 寄存器 | 引用    |
| ------ | ------- |
| p0     | this    |
| p1     | int p1  |
| p2,3   | float   |
| p4     | Boolean |

最少5个

## Dalvik指令集

一般的指令格式为：`[op]-[type](可选)/[位宽，默认4位] [目标寄存器],[源寄存器](可选)`，比如：`move v1,v2`，`move-wide/from16 v1,v2`

- 移位操作：

此类操作常用于赋值

| 指令              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| move v1,v2        | 将v2中的值移入到v1寄存器中（4位，支持int型）                 |
| Move/from16 v1,v2 | 将16位的v2寄存器中的值移入到8位的v1寄存器中                  |
| Move/16 v1,v2     | 将16位的v2寄存器中的值移入到16位的v1寄存器中                 |
| move-wide v1,v2   | 将寄存器对（一组，用于支持双字型）v2中的值移入到v1寄存器对中（4位，猜测支持float、double型） |
| move-object v1,v2 | 将v2中的对象指针移入到v1寄存器中                             |
| move-result v1    | 将这个指令的上一条指令计算结果，移入到v1寄存器中（需要配合invoke-static、invoke-virtual等指令使用） |

- 返回

| 指令             | 说明             |
| ---------------- | ---------------- |
| Return-void      | 返回void         |
| return v1        | 返回v1寄存器的值 |
| return-object v1 | 返回v1寄存器指针 |
| return-wide v1   | 返回双字结果给v1 |

- 判断

| If-eq v1,v2 | ==             |
| ----------- | -------------- |
| If-ne v1,v2 | !=             |
| if-lt v1,v2 | < less than    |
| if-le v1,v2 | <= less equal  |
| If-gt v1,v2 | >              |
| If-ge v1,v2 | >= great equal |

```java
	private void test() {
        int a = 0;
        int b = 1;
        String result;
        if (a > b) {
            result = "a great than b";
        } else {
            result = "a less than or equals b";
        }
    }

```

转为Smali

```
.method private test()V
    .registers 4

    .line 24
    const/4 v0, 0x0

    .line 25
    .local v0, "a":I
    const/4 v1, 0x1

    .line 27
    .local v1, "b":I
    if-le v0, v1, :cond_7

    .line 28
    const-string v2, "a great than b"

    .line 28
    .local v2, "result":Ljava/lang/String;
    goto :goto_9

    .line 30
    .end local v2    # "result":Ljava/lang/String;
    :cond_7
    const-string v2, "a less than or equals b"

    .line 32
    .restart local v2    # "result":Ljava/lang/String;
    :goto_9
    return-void
.end method
```

