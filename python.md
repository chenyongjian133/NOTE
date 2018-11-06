## 开发环境搭建
    1.下载安装包(官方解释器)
        -3.x
        -2.x
    2.安装
    3.打开命令行输入python，出现如下内容
        Python 3.6.5 (v3.6.5:f59c0932b4, Mar 28 2018, 16:07:46) [MSC v.1900 32 bit (Intel)] on win32
            Type "help", "copyright", "credits" or "license" for more information.
            >>> 
    4.立即执行文件python xxx.py
    5.安装Python的同时，会自动安装一个Python的开发工具IDLE，通过IDLE也可以进入到交互模式
        但是不同的是，在IDLE中可以通过TAB键来查看语句的提示。
        IDLE实际上就是一个交互界面，但是他可以有一些简单的提示，并且可以将代码保存

## Python与sublime整合
    1.在Sublime中执行Python代码，ctrl + b 自动在Sublime内置的控制台中执行  
        这种执行方式，在某些版本的Sublime中对中文支持不好，并且不能使用input()函数

    2.使用SublimeREPL来运行python代码    
        安装完成，设置快捷键，希望按f5则自动执行当前的Python代码
        { "keys": ["f5"], "caption": "SublimeREPL:Python","command": "run_existing_window_command", "args":{"id": "repl_python_run","file": "config/Python/Main.sublime-menu"}},

## 基本语法
    1.在Python中严格区分大小写
    2.Python中的每一行就是一条语句，每条语句以换行结束
    3.Python中每一行语句不要过长（规范中建议每行不要超过80个字符）
        "rulers":[80],
    4.一条语句可以分多行编写，多行编写时语句后边以\结尾  

        例：
        print('A\
        B\
        C')
        控制台输出效果ABC

    5.Python是缩进严格的语言，所以在Python中不要随便写缩进  
    6.在Python中使用#来表示注释，#后的内容都属于注释，注释的内容将会被解释器所忽略

## 定义变量和命名规范
    -直接定义变量，不需要关键词。会根据赋值类型判断变量类型。python是强类型语言
    -下划线命名法
        max_length
    -帕斯卡命名法（大驼峰命名法）
        首字母大写，每个单词开头字母大写，其余字母小写
        XxxYyyZzz

## 数据类型
    数值
        整型  int
        浮点型 float
        复数
    布尔值  True False
    字符串
    空值    None
    对象

## 对象的结构
    - 每个对象中都要保存三种数据
        - id（标识）
            > id用来标识对象的唯一性，每一个对象都有唯一的id
            > 对象的id就相当于人的身份证号一样
            > 可以通过id()函数来查看对象的id
            > id是由解析器生成的，在CPython中，id就是对象的内存地址
            > 对象一旦创建，则它的id永远不能再改变

        - type（类型）
            > 类型用来标识当前对象所属的类型
            > 比如：int str float bool 。。。
            > 类型决定了对象有哪些功能
            > 通过type()函数来查看对象的类型
            > Python是一门强类型的语言，对象一旦创建类型便不能修改


        - value（值）
            > 值就是对象中存储的具体的数据
            > 对于有些对象值是可以改变的
            > 对象分成两大类，可变对象 不可变对象
                可变对象的值可以改变
                不可变对象的值不能改变，之前学习的对象都是不可变对象
        - 参考 图2

## 整型
    Python中的整数的大小没有限制，可以是一个无限大的整数
        a=10
        b=9999999999999*1000000000
    如果数字的长度过大，可以使用下划线作为分隔符
        c = 123_456_789
    二进制 0b开头
        c = 0b10 # 二进制的10
    八进制 0o开头
        c = 0o10
    十六进制 0x开头
        c = 0x10

## 浮点型
    在Python中所有的小数都是float类型
    对浮点数进行运算时，可能会得到一个不精确的结果
        c = 0.1 + 0.2 # 0.30000000000000004

## 字符串
    s = 'hello'
    s = '锄禾日当午，\
        汗滴禾下土，\
        谁知盘中餐，\
        粒粒皆辛苦'           使用\换行不保留格式
    - 长字符串
        使用三重引号来表示一个长字符串 ''' """
        三重引号可以换行，并且会保留字符串中的格式
            s = '''锄禾日当午，
                    汗滴禾下土，
                    谁知盘中餐，
                    粒粒皆辛苦'''
    - 转义字符\
        \' 表示'
        \" 表示"
        \t 表示制表符
        \n 表示换行符
        \\ 表示反斜杠
        \uxxxx 表示Unicode编码
            s = '\u2250'
            print(s)
    - 格式化字符串
        a = '123'
        print('a =',a)  # a = 123
        print("a = "+a) # 报错
    - 在创建字符串时，可以在字符串中指定占位符
        %s 在字符串中表示任意字符
            b = 'Hello %s'%'孙悟空'
            b = 'hello %s 你好 %s'%('tom','孙悟空')
            b = 'hello %s'%123.456       hello 123.456
            b = 'hello %.2f'%123.456     hello 123.46
            b = 'hello %d'%123.95        hello 123
        %f 浮点数占位符
        %d 整数占位符
    - 格式化字符串
        在字符串前添加一个f来创建一个格式化字符串
        在格式化字符串中可以直接嵌入变量
            c = f'hello {a} {b}'
    - 字符串的复制
        如果将字符串和数字相乘，则解释器会将字符串重复指定的次数并返回
        a = 'abc' * 20

## 类型检查
    type()
        该函数会将检查的结果作为返回值返回，可以通过变量来接收函数的返回值
        print(type(1)) # <class 'int'>
        print(type(1.5)) # <class 'float'>
        print(type(True)) # <class 'bool'>
        print(type('hello'))  # <class 'str'>
        print(type(None)) # <class 'NoneType'>
    
    - 类型转换四个函数 int() float() str() bool() 都不影响原数据
        int()
            布尔值：True -> 1   False -> 0
            浮点数：直接取整，省略小数点后的内容
            字符串：合法的整数字符串，直接转换为对应的数字
            其他所有情况：直接抛出异常 ValueError
        float() 
            和 int()基本一致，不同的是它会将对象转换为浮点数
        str()
            True -> 'True'
            False -> 'False'
            123 -> '123'
        bool()  
            对于所有表示空性的对象都会转换为False，其余的转换为True
            哪些表示的空性：0 、 None 、 ''

## 算术运算符
    # + 加法运算符（如果是两个字符串之间进行加法运算，则会进行拼串操作）
    - 减法运算符
    * 乘法运算符（如果将字符串和数字相乘，则会对字符串进行复制操作，将字符串重复指定次数）
    / 除法运算符，运算时结果总会返回一个浮点类型
    // 整除，只会保留计算后的整数位，总会返回一个整型
    ** 幂运算，求一个值的几次幂
    % 取模，求两个数相除的余数

## 赋值运算符
    = 可以将等号右侧的值赋值给等号左侧的变量
    +=  a += 5 相当于 a = a + 5 
    -=  a -= 5 相当于 a = a - 5 
    *=  a *= 5 相当于 a = a * 5 
    **= a **= 5 相当于 a = a ** 5 
    /=  a /= 5 相当于 a = a / 5 
    //= a //= 5 相当于 a = a // 5 
    %=  a %= 5 相当于 a = a % 5 

## 关系运算符
    关系运算符用来比较两个值之间的关系，总会返回一个布尔值
    如果关系成立，返回True，否则返回False
    > 比较左侧值是否大于右侧值
    >= 比较左侧的值是否大于或等于右侧的值
    < 比较左侧值是否小于右侧值
    <= 比较左侧的值是否小于或等于右侧的值
    == 比较两个对象的值是否相等
    != 比较两个对象的值是否不相等
    相等和不等比较的是对象的值，而不是id
    is 比较两个对象是否是同一个对象，比较的是对象的id
    is not 比较两个对象是否不是同一个对象，比较的是对象的id

## 逻辑运算符
    not 逻辑非
    and 逻辑与
        Python中的与运算是短路的与，如果第一个值为False，则不再看第二个值
    or 逻辑或
        Python中的或运算是短路的或，如果第一个值为True，则不再看第二个值
    当我们对非布尔值进行与或运算时，Python会将其当做布尔值运算，最终会返回原值
        result = 0 or None 
        print(result)       # None

## 条件运算符（三元运算符） 
    语法： 语句1 if 条件表达式 else 语句2
        条件运算符在执行时，会先对条件表达式进行求值判断
        如果判断结果为True，则执行语句1，并返回执行结果
        如果判断结果为False，则执行语句2，并返回执行结果
        print('你好') if False else print('Hello')

        获取a和b之间的较大值
        max = a if a > b else b

## 运算符优先级
    与比或高

## 逻辑运算符（补充）
    逻辑运算符可以连着使用
    result = 1 < 2 < 3 # 相当于 1 < 2 and 2 < 3
    result = 10 < 20 > 15
    print(result)    # True

## 条件判断语句（if语句）
    语法：if 条件表达式 : 
              代码块
    执行的流程：if语句在执行时，会先对条件表达式进行求值判断，
        如果为True，则执行if后的语句
        如果为False，则不执行
        默认情况下，if语句只会控制紧随其后的那条语句，如果希望if可以控制多条语句，
        则可以在if后跟着一个代码块

    - 代码块
        代码块中保存着一组代码，同一个代码块中的代码，要么都执行要么都不执行
        代码块就是一种为代码分组的机制
    如果要编写代码块，语句就不能紧随在:后边，而是要写在下一行
    代码块以缩进开始，直到代码恢复到之前的缩进级别时结束
    鲁迅说过：
        世上本来没有路，走的人多了自然就有了！
        xxxx
    yyyy....

    缩进有两种方式，一种是使用tab键，一种是使用空格（四个）
    Python的官方文档中推荐我们使用空格来缩进
    Python代码中使用的缩进方式必须统一
    "translate_tabs_to_spaces": true,  

    例：   
    if False : print('你猜我出来么？')
    num = 10
    if num > 10 : print('num比10大！')

## input()函数
    该函数用来获取用户的输入
    input()调用后，程序会立即暂停，等待用户输入
    用户输入完内容以后，点击回车程序才会继续向下执行
    用户输入完成以后，其所输入的的内容会以返回值得形式返回
    注意：input()的返回值是一个字符串
    input()函数中可以设置一个字符串作为参数，这个字符串将会作为提示文字显示

    例：
    a = input('请输入任意内容：')
    print('用户输入的内容是:',a)

    input()也可以用于暂时阻止程序结束

    获取用户输入的用户名
    username = input('请输入你的用户名:')
    判断用户名是否是admin
    if username == 'admin' :
        print('欢迎管理员光临！')

## if-elif-else语句
    语法：
        if 条件表达式 :
            代码块
        elif 条件表达式 :
            代码块
        elif 条件表达式 :
            代码块
        elif 条件表达式 :
            代码块
        else :
            代码块

    练习1：
     编写一个程序，获取一个用户输入的整数。然后通过程序显示这个数是奇数还是偶数。
     num = input('请输入一个整数：')
     if num % 2:
        print('你输入的是偶数')
     else:
        print('你输入的是奇数')

    练习2：
     编写一个程序，检查任意一个年份是否是闰年。
     如果一个年份可以被4整除不能被100整除，或者可以被400整除，这个年份就是闰年
     year = input('请输入一个年份：')
     if year % 4 == 0 and year % 100 != 0 or year % 400 ==0 :
        print(year,'是闰年')
     else :
        print(year,'是平年')

## 循环语句
    循环语句分成两种，while循环 和 for循环
    while循环
        语法：
            while 条件表达式 :
                代码块
            else :
                代码块
        执行流程：
        while语句在执行时，会先对while后的条件表达式进行求值判断，
        如果判断结果为True，则执行循环体（代码块），
        循环体执行完毕，继续对条件表达式进行求值判断，以此类推，
        直到判断结果为False，则循环终止，如果循环有对应的else，则执行else后的代码块
        
        例：
            创建一个执行十次的循环
            i = 0
            while i < 10 :
                i += 1
                print(i,'hello')
            else :
                print('else中的代码块')
        练习
            水仙花数是指一个 n 位数（n≥3 ），它的每个位上的数字的 n 次幂之和等于它本身（例如：1**3 + 5**3 + 3**3 = 153）。
            求1000以内所有的水仙花数
            i = 100
            while i < 1000 :
                # 假设，i的百位数是a，十位数b，个位数c
                # a = int(i / 100)
                a = i // 100
                b = (i - a * 100) // 10
                c = i % 10
                if a**3 + b**3 + c**3 == i :
                    print(i)
                i += 1

        # *****
        # ****
        # ***
        # **
        # *
            i = 0
            while i < 5:
                j = 0
                while j < i + 1:
                    print("* ",end='')      # 第二个参数end='',表示不换行打印
                    j += 1
                print()
                i += 1

        练习2：
            打印99乘法表
            i = 0
            while i < 8:
                i+=1
                j = 0
                while j<i :
                    j+=1
                    print(f'{j}*{i}={j*i} ',end='')
            print()

# break&&continue
    break和continue都是只对离他最近的循环起作用

    break可以用来立即退出循环语句（包括else）
    continue
        continue可以用来跳过当次循环
    
    pass
        pass是用来在判断或循环语句中占位的

    例：   创建一个5次的循环
        i = 0
        while i < 5:
        if i == 3:
            break
        print(i)
        i += 1
        else :
            print('循环结束')

## 模块
    通过模块可以对python进行扩展
    引入time模块，统计时间
    from time import *
        time()可以获取当前时间，返回秒

    例：求10万以内的质数
    begin = time()

    i = 2
    while i < 100000:
        flag = True     #默认是质数
        j = 2
        while j <= i ** 0.5 :    #开方是因为因子都是一对一对的，所以只需要找到开方的位置就够了，没必要全部找
            if i % j == 0 :
                flag = False
                break   #一旦i能被j整除，直接break，说明i不是质数
            j+=1
        if flag :
            print(i)
            # pass
        i+=1
    
    end = time()
    print(end-begin,'秒')

## 大战游戏
    player = '超级玛丽'
    boss = '蘑菇怪'
    print('-'*20,f'欢迎光临《{player}大战{boss}》','-'*20)
    # 身份
    print('请选择你的身份：')
    print(f'\t1.{player}')
    print(f'\t2.{boss}')
    # 用户选择身份
    player_choose = input('请选择[1-2]:')
    # 分割线
    print('-'*66)
    # 判断用户选择
    if player_choose == '1' :
        print(f'你选择了1，你将以->{player}<-的身份进行游戏!')
    elif player_choose == '2' :
        print(f'你竟然选择{boss}，太不要脸了，你将以->{player}<-的身份进行游戏!')
    else :
        print(f'你的输入有误，系统自动给你分配角色，你将以->{player}<-的身份进行游戏!')
    # 分割线
    print('-'*66)
    # 进入游戏，定义角色生命值和攻击力
    player_life = 2
    player_attack = 2
    boss_life = 10
    boss_attack = 10
    print(f'{player}你的生命值是{player_life}，你的攻击力是{player_attack}')
    # 游戏界面和选项
    while True:
        # 分割线
        print('-'*66)
        print('请选择你要进行的操作：')
        print('\t1.练级')
        print('\t2.打boss')
        print('\t3.逃跑')
        player_choose = input('请选择要做的操作[1-3]：')
        if player_choose == '1' :
            player_life += 2
            player_attack += 2
            print('-'*66)
            print(f'恭喜你升级了！你现在的生命值是{player_life}，攻击力是{player_attack}')
        elif player_choose == '2' :
            boss_life -= player_attack
            # 打印一条分割线
            print('-'*66)
            print(f'->{player}<- 攻击了 ->{boss}<-')
            if boss_life <= 0 :
                print(f'{boss}受到了{player_attack}的伤害,重伤不治，游戏结束，->{player}<-取的胜利！')
                break
            player_life -= boss_attack 
            print(f'->{boss}<- 攻击了 ->{player}<-')
            if player_life<=0:
                print(f'你受到了{boss_attack}的伤害,重伤不治，游戏结束，->{boss}<-取的胜利！')
                break
        elif player_choose == '3' :
            print('-'*66)
            print(f'你逃跑了，游戏结束！')
            break
        else :
            print('-'*66)
            print('输入有误，请重新选择！')

## 列表（list）
    - 列表是Python中的一个对象
    - 对象（object）就是内存中专门用来存储数据的一块区域
    - 列表中可以保存多个有序的数据
    - 列表是用来存储对象的对象
    - 列表的使用：
        1.列表的创建
        2.操作列表中的数据
    - 创建列表，通过[]创建
        my_list = []
        print(my_list , type(my_list))      #  [] <class 'list'>

        my_list = [10] # 创建一个只包含一个元素的列表
        my_list = [10,'hello',True,None,[1,2,3],print]      # 列表中可以保存任意的对象
        print(my_list[4])       #读取列表元素
        len(my_list)            #返回列表长度
        print(my_list[-2])      #索引是负数，则从后向前获取元素，-1表示倒数第一个，-2表示倒数第二个 以此类推
    - 切片
        切片指从现有列表中，获取一个子列表（返回新列表）
        语法：列表[起始:结束]           #包含起始，不含结束
        如果起始位置和结束位置全部省略，则相当于创建了一个列表的副本
            print(stus[1:])
            print(stus[:3])
            print(stus[:])
            print(stus)

        语法：列表[起始:结束:步长] 
            步长表示，每次获取元素的间隔，默认值是1，步长不能是0，但是可以是负数，负数，则会从列表的后部向前边取元素
            print(stus[::0]) ValueError: slice step cannot be zero
            print(stus[0:5:3])
            print(stus[::-1])
    - + 和 *
        my_list = [1,2,3] + [4,5,6]     # [1,2,3,4,5,6]
        my_list = [1,2] * 3             # [1,2,1,2,1,2]
    - in 和 not in
        arrs = [1,2,3]
        print(1 not in arrs)      #False
        print(2 in arrs)           #True
    - min() 获取列表中的最小值    min(arrs)
    - max() 获取列表中的最大值    max(arrs)
    - index() 
        获取指定元素在列表中的第一次出现时索引
        index()的第二个参数，表示查找的起始位置 ， 第三个参数，表示查找的结束位置
        如果要获取列表中没有的元素，会抛出异常
        [1,2,3].index(1)         # 0
    - count()
        统计指定元素在列表中出现的次数
        [1,2,3,3,3,3].count(3)  # 4

## 序列（sequence）
    - 序列是Python中最基本的一种数据结构
    - 数据结构指计算机中数据存储的方式
    - 序列用于保存一组有序的数据，所有的数据在序列当中都有一个唯一的位置（索引）
        并且序列中的数据会按照添加的顺序来分配索引
    - 序列的分类：
        可变序列（序列中的元素可以改变）：
            > 列表（list）
        不可变序列（序列中的元素不能改变）：
            > 字符串（str）    
            > 元组（tuple）
        - 刚刚我们所讲所有操作都是序列的通用操作01 02 03 三个文件中的操作（以上操作适用所有列表）

## 可变序列(list)才能用的方法
    - 修改元素(直接通过索引修改)
        stus = ['孙悟空','猪八戒','沙和尚','唐僧','蜘蛛精','白骨精']
        stus[0] = 'hahaha'
    - del
        通过del来删除元素
        del stus[2]         # 删除索引为2的元素
    - 通过切片修改列表
        在给切片进行赋值时，只能使用序列(可变或不可变都行)，number和None和boolen都不行
        stus[0:2] = ['牛魔王','红孩儿']     #使用新的元素替换旧元素
        stus[0:2] = 'ab'                #['a','b','沙和尚','唐僧','蜘蛛精','白骨精']
        stus[0:2] = 12                  #报错
        stus[0:0] = ['牛魔王']          # 向索引为0的位置插入元素
        stus[0:2] = ['牛魔王','红孩儿','二郎神']    #['牛魔王','红孩儿','二郎神','沙和尚','唐僧','蜘蛛精','白骨精']
        当设置了步长时，序列中元素的个数必须和切片中元素的个数一致
        stus[::2] = ['牛魔王','红孩儿','二郎神']    #['牛魔王', '猪八戒', '红孩儿', '唐僧', '二郎神', '白骨精']
    - 通过切片来删除元素
        del stus[0:2]     #删除第一第二个元素
        del stus[::2]     #删除步长为2的元素['猪八戒','唐僧','白骨精']
        stus[1:3] = []     #删除第二第三个元素
    - append()
        向列表的最后添加一个元素
        [1,2,3].append('hello world')
    - insert()
        向列表的指定位置插入一个元素
        参数：
            1.要插入的位置
            2.要插入的元素
        ['a','b','c'].insert(1,'d')         #['a','d','b','c']
    - extend()
        使用新的序列来扩展当前序列
        需要一个序列作为参数，它会将该序列中的元素添加到当前列表中
        stus.extend(['唐僧','白骨精'])
        相当于
        stus += ['唐僧','白骨精']
    - clear()
        清空序列
        stus.clear()
    - pop()
        根据索引删除并返回被删除的元素
        result = [1,2,3].pop(1)     # 删除索引为2的元素
        result = [1,2,3].pop()     # 不传参数默认删除最后一个
    - remove()
        删除指定值得元素，如果相同值得元素有多个，只会删除第一个
        stus.remove('猪八戒')
    - reverse()
        反转列表
        stus.reverse()
    - sort()
        用来对列表中的元素进行排序，默认是升序排列
        如果需要降序排列，则需要传递一个reverse=True作为参数
        my_list = list('asnbdnbasdabd')         #list()函数可以将一个不可变序列转成可变序列
        print(my_list.sort())
        my_list = [10,1,20,3,4,5,0,-2]
        print(my_list.sort(reverse=True))

## 遍历
    for
        语法：
            for 变量 in 序列 :
                代码块
        例：
            for s in stus :
                print(s)

## EMS系统练习
    # 显示系统的欢迎信息
    print('-'*20 , '欢迎使用员工管理系统', '-'*20)
    # 创建一个默认用户列表
    emps = ['小hong\t18\t女\t上海','小bai\t19\t男\t北京']
    while True:
        # 显示用户的选项
        print('请选择要做的操作：')
        print('\t1.查询员工')
        print('\t2.添加员工')
        print('\t3.删除员工')
        print('\t4.退出系统')
        user_choose = input('请选择[1-4]:')
        print('-'*62)
        if user_choose == '1' :
            print('\t序号\t姓名\t年龄\t性别\t住址')
            n = 1
            for s in emps :
                print(f'\t{n}\t{s}')
                n+=1
        elif user_choose == '2' :
            # 获取要添加员工的信息，姓名、年龄、性别、住址
            emp_name = input('请输入员工的姓名：')
            emp_age = input('请输入员工的年龄：')
            emp_gender = input('请输入员工的性别：')
            emp_address = input('请输入员工的住址：')
            emp = f'{emp_name}\t{emp_age}\t{emp_gender}\t{emp_address}'
            print('以下员工将被添加到系统中')
            print('-'*62)
            print('\t姓名\t年龄\t性别\t住址')
            print(f'\t{emp}')
            print('-'*62)
            confirm = input('是否确定该操作[Y/N]：')
            if confirm == 'y' or confirm == 'yes' :
                emps.append(emp)
                print('操作成功！')
            else :
                print('操作已取消！')
        elif user_choose == '3' :
            num = int(input('请输入要删除的员工序号：'))
            if num > 0 and num <= len(emps) :
                index = num - 1
                print('以下员工将要被删除')
                print('-'*62)
                print('\t序号\t姓名\t年龄\t性别\t住址')
                print(f'\t{num}\t{emps[index]}')
                user_confirm = input('该操作不可恢复，是否确认[Y/N]：')
                if user_confirm == 'y' or user_confirm == 'yes' :
                    print('操作成功！')
                    emps.pop(index)
                else :
                    print('操作已取消！')
            else :
                print('没有你要删除的员工序号！')
        elif user_choose == '4' :
            print('欢迎使用，再见！')
            input('按回车键退出！')
            break
        else :
            print('你的输入有误，请重新选择')
        print('-'*62)

## range()是一个函数，可以用来生成一个自然数的序列
    该函数需要三个参数
        1.起始位置（可以省略，默认是0）
        2.结束位置
        3.步长（可以省略，默认是1）
    r = range(5)        
    print(r)            #range(0,5)
    print(list(r))      #[0,1,2,3,4]

    r = range(0,10,2)
    print(r)            #range(0, 10, 2)
    print(list(r))      #[0, 2, 4, 6, 8]

    r = range(10,0,-1)
    print(r)            #range(10, 0, -1)
    print(list(r))      #[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

## for()循环
    包括else、包括break continue都可以在for循环中使用
    for i in range(30) :
        print(i)

    for s in 'hello' :
        print(s)

## 元组 tuple
    元组是一个不可变的序列
    它的操作的方式基本上和列表是一致的
    所以你在操作元组时，就把元组当成是一个不可变的列表就ok了
    一般当我们希望数据不改变时，就使用元组，其余情况都使用列表

    使用()来创建元组
        my_tuple = ()       # 创建了一个空元组
        print(my_tuple,type(my_tuple)) # <class 'tuple'>
        my_tuple = (1,2,3,4,5) # 创建了一个5个元素的元组

    元组是不可变对象，不能尝试为元组中的元素重新赋值
        my_tuple[3] = 10 TypeError: 'tuple' object does not support item assignment
    
    当元组不是空元组时，括号可以省略
        my_tuple = 10,20,30,40
    如果元组不是空元组，它里边至少要有一个,
        my_tuple = 40,

    元组的解包（解构）
        解包指就是将元组当中每一个元素都赋值给一个变量
        my_tuple = 10 , 20 , 30 , 40
        a,b,c,d = my_tuple
        print(a,b,c,d)

        a = 100
        b = 300
        a , b = b , a           # 交互a 和 b的值，这时我们就可以利用元组的解包
    
    在对一个元组进行解包时，变量的数量必须和元组中的元素的数量一致
    也可以在变量前边添加一个*，这样变量将会获取元组中所有剩余的元素
    不能同时出现两个或以上的*变量
    a , b , *c = my_tuple
    a , *b , c = my_tuple
    *a , b , c = my_tuple
    a , b , *c = [1,2,3,4,5,6,7]
    a , b , *c = 'hello world'
    print('a =',a)      a = h
    print('b =',b)      b = e
    print('c =',c)      c = ['l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd']

## 可变对象
    - 每个对象中都保存了三个数据：
        id（标识）
        type（类型）
        value（值）    

    - 列表就是一个可变对象
        a = [1,2,3]

    - a[0] = 10 （改对象）
        - 这个操作是在通过变量去修改对象的值
        - 这种操作不会改变变量所指向的对象    
        - 当我们去修改对象时，如果有其他变量也指向了该对象，则修改也会在其他的变量中体现

    - a = [4,5,6] （改变量）
        - 这个操作是在给变量重新赋值
        - 这种操作会改变变量所指向的对象
        - 为一个变量重新赋值时，不会影响其他的变量
    
    - == !=  is is not
        == != 比较的是对象的值是否相等 
        is is not 比较的是对象的id是否相等（比较两个对象是否是同一个对象）

            a = [1,2,3]
            b = [1,2,3]
            print(a,b)
            print(id(a),id(b))
            print(a == b) # a和b的值相等，使用==会返回True
            print(a is b) # a和b不是同一个对象，内存地址不同，使用is会返回False

## 字典（dict）
    - 字典属于一种新的数据结构，称为映射（mapping）
    - 字典的作用和列表类似，都是用来存储对象的容器
    - 列表存储数据的性能很好，但是查询数据的性能的很差
    - 在字典中每一个元素都有一个唯一的名字，通过这个唯一的名字可以快速的查找到指定的元素
    - 在查询元素时，字典的效率是非常快的
    - 在字典中可以保存多个对象，每个对象都会有一个唯一的名字
        这个唯一的名字，我们称其为键（key），通过key可以快速的查询value
        这个对象，我们称其为值（value）
        所以字典，我们也称为叫做键值对（key-value）结构
        每个字典中都可以有多个键值对，而每一个键值对我们称其为一项（item）

## 使用 {} 来创建字典
    d = {}      # 创建了一个空字典

    创建一个有数据的字典
        # 语法：
        #   {key:value,key:value,key:value}
        #   字典的值可以是任意对象
        #   字典的键可以是任意的不可变对象（int、str、bool、tuple ...），但是一般我们都会使用str
        #       字典的键是不能重复的，如果出现重复的后边的会替换到前边的
        # d = {'name':'孙悟空' , 'age':18 , 'gender':'男' , 'name':'sunwukong'}

        d = {
        'name':'孙悟空' , 
        'age':18 , 
        'gender':'男' , 
        'name':'sunwukong'
        }

        print(d , type(d))      {'name': 'sunwukong', 'age': 18, 'gender': '男'} <class 'dict'>
        print(d['hello'])       KeyError: 'hello'
    
## 使用 dict()函数来创建字典
    d = dict(name='孙悟空',age=18,gender='男')

    也可以将一个包含有双值子序列的序列转换为字典
    双值序列，序列中只有两个值，[1,2] ('a',3) 'ab'
    子序列，如果序列中的元素也是序列，那么我们就称这个元素为子序列
        d = dict([('name','孙悟饭'),('age',18)])        
        print(d , type(d))                  {'name': '孙悟饭', 'age': 18} <class 'dict'>

    len() 获取字典中键值对的个数

    in 检查字典中是否包含指定的键
    not in 检查字典中是否不包含指定的键
        print('hello' in d)

    获取字典中的值，根据键来获取值
        语法：d[key]
            print(d['age'])

    通过[]来获取值时，如果键不存在，会抛出异常 KeyError
    get(key[, default]) 该方法用来根据键来获取字典中的值
        如果获取的键在字典中不存在，会返回None
        也可以指定一个默认值，来作为第二个参数，这样获取不到值时将会返回默认值
            print(d.get('name'))
            print(d.get('hello','默认值'))
    
    修改字典
        d[key] = value 如果key存在则覆盖，不存在则添加

    setdefault(key[, default]) 可以用来向字典中添加key-value
        如果key已经存在于字典中，则返回key的值，不会对字典做任何操作
        如果key不存在，则向字典中添加这个key，并设置value
        result = d.setdefault('name','猪八戒')     result = 孙悟饭  因为原字典有name,所以返回原字典中的name
        result = d.setdefault('hello','猪八戒')     result = 猪八戒 修改成功，原字典没有hello，返回修改成功的内容

    update([other])
        将其他的字典中的key-value添加到当前字典中
        如果有重复的key，则后边的会替换到当前的
            d = {'a':1,'b':2,'c':3}
            d2 = {'d':4,'e':5,'f':6, 'a':7}
            d.update(d2)
    删除，可以使用 del 来删除字典中的 key-value
        del d['a']

    popitem()
        随机删除字典中的一个键值对，一般都会删除最后一个键值对
        删除之后，它会将删除的key-value作为返回值返回
        返回的是一个元组，元组中有两个元素，第一个元素是删除的key，第二个是删除的value
        当使用popitem()删除一个空字典时，会抛出异常 KeyError: 'popitem(): dictionary is empty'
        d.popitem()
        result = d.popitem()

    pop(key[, default])
        根据key删除字典中的key-value
        会将被删除的value返回！
        如果删除不存在的key，会抛出异常
        如果指定了默认值，再删除不存在的key时，不会报错，而是直接返回默认值
        result = d.pop('d')
        result = d.pop('z','这是默认值')

    clear()用来清空字典
        d.clear()

    copy()
        该方法用于对字典进行浅复制
        复制以后的对象，和原对象是独立，修改一个不会影响另一个
        注意，浅复制会简单复制对象内部的值，如果值也是一个可变对象，这个可变对象不会被复制
        d = {'a':1,'b':2,'c':3}
        d2 = d.copy()

    keys() 该方法会返回字典的所有的key
        该方法会返回一个序列，序列中保存有字典的所有的键
        d = {'name':'孙悟空','age':18,'gender':'男'}
        for k in d.keys() :
            print(k,d[k])
    values()
        该方法会返回一个序列，序列中保存有字典的左右的值
        for v in d.values() :
            print(v)
    items()
        该方法会返回字典中所有的项
        它会返回一个序列，序列中包含有双值子序列
        双值分别是，字典中的key和value
        for k,v in d.items() :
            print(k,'=',v)

## 集合（set）
    - 集合和列表非常相似
    - 不同点：
        1.集合中只能存储不可变对象
        2.集合中存储的对象是无序（不是按照元素的插入顺序保存）
        3.集合中不能出现重复的元素

## 使用 {} 来创建集合
    s = {10,3,5,1,2,1,2,3,1,1,1,1} # <class 'set'>
    s = {[1,2,3],[4,6,7]}       TypeError: unhashable type: 'list'

## 使用 set() 函数来创建集合
    s = set() # 空集合
    通过set()来将序列和字典转换为集合
        s = set([1,2,3,4,5,1,1,2,3,4,5])
        s = set('hello')
        s = set({'a':1,'b':2,'c':3}) # 使用set()将字典转换为集合时，只会包含字典中的键
    使用in和not in来检查集合中的元素
        print('c' in s)
    len()来获取集合中元素的数量
    add() 向集合中添加元素
        s.add(10)
        s.add(30)
    update() 将一个集合中的元素添加到当前集合中
        update()可以传递序列或字典作为参数，字典只会使用键
        s2 = set('hello')
        s.update(s2)
        s.update((10,20,30,40,50))
        s.update({10:'ab',20:'bc',100:'cd',1000:'ef'})
    pop()随机删除并返回一个集合中的元素
        result = s.pop()
    remove()删除集合中的指定元素
        s.remove(100)
        s.remove(1000)
    clear()清空集合
        s.clear()
    copy()对集合进行浅复制

## 集合运算
    在对集合做运算时，不会影响原来的集合，而是返回一个运算结果
    s = {1,2,3,4,5}
    s2 = {3,4,5,6,7}

    & 交集运算
        result = s & s2     # {3, 4, 5}
    | 并集运算
        result = s | s2     # {1,2,3,4,5,6,7}
    - 差集
        result = s - s2     # {1, 2}
    ^ 异或集 获取只在一个集合中出现的元素
        result = s ^ s2     # {1, 2, 6, 7}
    <= 检查一个集合是否是另一个集合的子集
        如果a集合中的元素全部都在b集合中出现，那么a集合就是b集合的子集，b集合是a集合超集
        a = {1,2,3}
        b = {1,2,3,4,5}
        result = a <= b     # True
    < 检查一个集合是否是另一个集合的真子集
    >= 检查一个集合是否是另一个的超集
    > 检查一个集合是否是另一个的真超集

## 函数简介（function）
    - 创建函数：
        def 函数名([形参1,形参2,...形参n]) :
            代码块
        - 函数名必须要符号标识符的规范
            （可以包含字母、数字、下划线、但是不能以数字开头）    
    - 调用函数：
        函数对象()

## 函数的参数
    - 在定义函数时，可以在函数名后的()中定义数量不等的形参，
        多个形参之间使用,隔开
    - 形参（形式参数），定义形参就相当于在函数内部声明了变量，但是并不赋值
    - 实参（实际参数）
        - 如果函数定义时，指定了形参，那么在调用函数时也必须传递实参，
            实参将会赋值给对应的形参，简单来说，有几个形参就得传几个实参

## 函数式编程
    - 在Python中，函数是一等对象
    - 一等对象一般都会具有如下特点：
        ① 对象是在运行时创建的
        ② 能赋值给变量或作为数据结构中的元素
        ③ 能作为参数传递
        ④ 能作为返回值返回
        
    - 高阶函数
        - 高阶函数至少要符合以下两个特点中的一个
          ① 接收一个或多个函数作为参数
          ② 将函数作为返回值返回 

        def fn2(a , b) :
            print('a =',a)
            print('b =',b)
            print(a,"+",b,"=",a + b)

    指定默认参数
        def fn(a = 5 , b = 10 , c = 20):
            print('a =',a)
            print('b =',b)
            print('c =',c)

        fn()        默认调用
        fn(1,2,3)   修改参数调用


    关键字参数
        关键字参数，可以不按照形参定义的顺序去传递，而直接根据参数名去传递参数
        def fn(a = 5 , b = 10 , c = 20):
            print(a+b+c)

        fn(b=1 , c=2 , a=3)     关键字参数调用
    
    位置参数和关键字参数可以混合使用
        混合使用关键字和位置参数时，必须将位置参数写到前面
        位置参数就是将对应位置的实参复制给对应位置的形参
        def fn(a = 5 , b = 10 , c = 20):
            print(a+b+c)
        fn(1 , c=2 )     1+10+2 关键字参数与位置参数混用

    不定长的参数
        def sum(*nums):
            result=0
            for n in nums :
                result+=n
            print(result)
        sum(123,456,789,10,20,30,40)    调用

    普通参数和不定长参数混合使用
        def fn(a,b,*c):
            print('a =',a)
            print('b =',b)
            print('c =',c)
        fn(1,2,3,4,5)    # a = 1 b = 2 c = (3, 4, 5)

    可变参数不是必须写在最后，但是注意，带*的参数后的所有参数，必须以关键字参数的形式传递
        def fn2(a,*b,c):        c必须使用关键字参数
            print('a =',a)
            print('b =',b)
            print('c =',c)

    如果在形参的开头直接写一个*,则要求我们的所有的参数必须以关键字参数的形式传递
        def fn2(*,a,b,c):
            print('a =',a)
            print('b =',b)
            print('c =',c)
        fn2(a=1,b=2,c=3)

    *形参只能接收位置参数，而不能接收关键字参数
        def fn3(*a) :
            print('a =',a)
        fn3(a='str')    got an unexpected keyword argument 'a'

    **形参可以接收其他的关键字参数，它会将这些参数统一保存到一个字典中
        字典的key就是参数的名字，字典的value就是参数的值
        **形参只能有一个，并且必须写在所有参数的最后
        def fn3(*d,b,c,**a) :
            print('a =',a,type(a))
            print('b =',b)
            print('c =',c)
            print('d =',d)
        fn3(22,b=1,d=2,c=3,e=10,f=20)
            a = {'d': 2, 'e': 10, 'f': 20} <class 'dict'>
            b = 1
            c = 3
            d = (22, 33)
            a = 100
            b = 200
            c = 300
        
    参数的解包（拆包）
        def fn4(a,b,c):
            print('a =',a)
            print('b =',b)
            print('c =',c)

        # 创建一个元组
        t = (10,20,30)

        # 传递实参时，也可以在序列类型的参数前添加星号，这样他会自动将序列中的元素依次作为参数传递
        # 这里要求序列中元素的个数必须和形参的个数的一致
        # fn4(*t)    

        # 创建一个字典
        d = {'a':100,'b':200,'c':300}
        # 通过 **来对一个字典进行解包操作
        fn4(**d)

## help()是Python中的内置函数
        # 通过help()函数可以查询python中的函数的用法
        # 语法：help(函数对象)
        # help(print) # 获取print()函数的使用说明

        # 文档字符串（doc str）
        # 在定义函数时，可以在函数内部编写文档字符串，文档字符串就是函数的说明
        #   当我们编写了文档字符串时，就可以通过help()函数来查看函数的说明
        #   文档字符串非常简单，其实直接在函数的第一行写一个字符串就是文档字符串
        def fn(a:int,b:bool,c:str='hello') -> int:
            '''
            这是一个文档字符串的示例

            函数的作用：。。。。。
            函数的参数：
                a，作用，类型，默认值。。。。
                b，作用，类型，默认值。。。。
                c，作用，类型，默认值。。。。
            '''
            return 10

        help(fn)

## 作用域（scope）
    a = 20
    def fn3():
        # a = 10 # 在函数中为变量赋值时，默认都是为局部变量赋值
        # 如果希望在函数内部修改全局变量，则需要使用global关键字，来声明变量
        global a # 声明在函数内部的使用a是全局变量，此时再去修改a时，就是在修改全局的a
        a = 10 # 修改全局变量
        print('函数内部：','a =',a)

## 命名空间（namespace）
        # 命名空间指的是变量存储的位置，每一个变量都需要存储到指定的命名空间当中
        # 每一个作用域都会有一个它对应的命名空间
        # 全局命名空间，用来保存全局变量。函数命名空间用来保存函数中的变量
        # 命名空间实际上就是一个字典，是一个专门用来存储变量的字典

        locals()用来获取当前作用域的命名空间
        # 如果在全局作用域中调用locals()则获取全局命名空间，如果在函数作用域中调用locals()则获取函数命名空间
        # 返回的是一个字典
        scope = locals() # 当前命名空间
        print(type(scope))
        # print(a)
        # print(scope['a'])
        # 向scope中添加一个key-value
        scope['c'] = 1000       # 向字典中添加key-value就相当于在全局中创建了一个变量（一般不建议这么做）
        # print(c)

        def fn4():
            a = 10
            # scope = locals() # 在函数内部调用locals()会获取到函数的命名空间
            # scope['b'] = 20 # 可以通过scope来操作函数的命名空间，但是也是不建议这么做

            # globals() 函数可以用来在任意位置获取全局命名空间
            global_scope = globals()
            # print(global_scope['a'])
            global_scope['a'] = 30
            # print(scope)

        fn4()    

## 递归
    求阶乘
    def factorial(n) :
        return 1 if n == 1 else n * factorial(n-1)
    任意数字做任意次幂运算
    def power(n,i) :
        return n if i == 1 else n * power(n,i-1)
    检查回文
        abcdefgfedcba这就是回文
    def hui_wen(s) :
        return True if len(s)<2 else s[0] == s[1] and hui_wen(s[1:-1])

    def hui_wen(s):
    '''
        该函数用来检查指定的字符串是否回文字符串，如果是返回True，否则返回False

        参数：
            s：就是要检查的字符串
    '''
    # 基线条件
    if len(s) < 2 :
        # 字符串的长度小于2，则字符串一定是回文
        return True
    elif s[0] != s[-1]:
        # 第一个字符和最后一个字符不相等，不是回文字符串
        return False    
    # 递归条件    
    return hui_wen(s[1:-1])

## 匿名函数 lambda 函数表达式 （语法糖）
    lambda函数表达式专门用来创建一些简单的函数
        语法：lambda 参数列表 : 返回值
        匿名函数一般都是作为参数使用，其他地方一般不会使用

        例：
            lambda a,b : a+b
        lambda自调用
            (lambda a,b : a+b)(10,20)

## 高阶函数
    filter()   内置函数(高阶)
        filter()可以从序列中过滤出符合条件的元素，保存到一个新的序列中
        参数：
            1.函数，根据该函数来过滤序列（可迭代的结构）
            2.需要过滤的序列（可迭代的结构）
        返回值：
            过滤后的新序列（可迭代的结构）
        例：
            l = [1,2,3,4,5,6,7,8,9,10]
            r = fliter(lambda i : i>5, l)
            print(list(r))
    map()
        map()函数可以对可迭代对象中的所有元素做指定的操作，然后将其添加到一个新的对象中返回
        r = map(lambda i : i ** 2 , l)
        print(list(r))

    sort()
        该方法用来对列表中的元素进行排序
        sort()方法默认是直接比较列表中的元素的大小
        在sort()可以接收一个关键字参数 ， key
        key需要一个函数作为参数，当设置了函数作为参数
        每次都会以列表中的一个元素作为参数来调用函数，并且使用函数的返回值来比较元素的大小
        l = ['bb','aaaa','c','ddddddddd','fff']
        l.sort(key=len)
        print(l)            ['c', 'bb', 'fff', 'aaaa', 'ddddddddd']

        l = [2,5,'1',3,'6','4']
        l.sort(key=int)
        print(l)            ['1', 2, 3, '4', 5, '6']

    sorted()
        这个函数和sort()的用法基本一致，但是sorted()可以对任意的序列进行排序
        并且使用sorted()排序不会影响原来的对象，而是返回一个新对象
            l = "123765816742634781"
            print('排序前:',l)              排序前: 123765816742634781
            print(sorted(l,key=int))        ['1', '1', '1', '2', '2', '3', '3', '4', '4', '5', '6', '6', '6', '7', '7', '7', '8', '8']
            print('排序后:',l)              排序前: 123765816742634781

            l = [2,5,'1',3,'6','4']
            print('排序前:',l)              排序前: [2, 5, '1', 3, '6', '4']
            print(sorted(l,key=int))        ['1', 2, 3, '4', 5, '6']
            print('排序后:',l)              排序前: [2, 5, '1', 3, '6', '4']

## 闭包
    将函数作为返回值返回，也是一种高阶函数
    这种高阶函数我们也称为叫做闭包，通过闭包可以创建一些只有当前函数能访问的变量
    可以将一些私有的数据藏到的闭包中

    形成闭包的要件
        ① 函数嵌套
        ② 将内部函数作为返回值返回
        ③ 内部函数必须要使用到外部函数的变量

        def make_averager():
            # 创建一个列表，用来保存数值
            nums = []
            # 创建一个函数，用来计算平均值
            def averager(n) :
                # 将n添加到列表中
                nums.append(n)
                # 求平均值
                return sum(nums)/len(nums)          sum()是python内置函数，可以求和

            return averager

        averager = make_averager()

        print(averager(10))
        print(averager(20))
        print(averager(30))
        print(averager(40))

## 装饰器
    通过装饰器，可以在不修改原来函数的情况下来对函数进行扩展
    在定义函数时，可以通过@装饰器，来使用指定的装饰器，来装饰当前的函数
    可以同时为一个函数指定多个装饰器，这样函数将会按照从内向外的顺序被装饰 
    定义2个装饰器
    def begin_end(old) :
        def new_function(*args,**kwargs) :
            print('begin装饰执行')
            result = old(*args,**kwargs)
            print('begin装饰结束')
            return result
        return new_function

    def fn3(old) :
        def new_function(*args,**kwargs) :
            print('fn3装饰执行')
            result = old(*args,**kwargs)
            print('fn3装饰结束')
            return result
        return new_function

    使用例子
    @fn3
    @begin_end
    def say_hello() :
        print('我是old函数')
    say_hello()
    fn3装饰执行
    begin装饰执行
    我是old函数
    begin装饰结束
    fn3装饰结束

## 对象（Object）

## 什么是对象？
    - 对象是内存中专门用来存储数据的一块区域。
    - 对象中可以存放各种数据（比如：数字、布尔值、代码）
    - 对象由三部分组成：
        1.对象的标识（id）
        2.对象的类型（type）
        3.对象的值（value）

## 面向对象（oop）
    - Python是一门面向对象的编程语言
    - 所谓的面向对象的语言，简单理解就是语言中的所有操作都是通过对象来进行的
    - 面向过程的编程的语言
        - 面向过程指将我们的程序的逻辑分解为一个一个的步骤，
            通过对每个步骤的抽象，来完成程序
        - 例子：
            - 孩子上学
                1.妈妈起床
                2.妈妈上厕所
                3.妈妈洗漱
                4.妈妈做早饭
                5.妈妈叫孩子起床
                6.孩子上厕所
                7.孩子要洗漱
                8.孩子吃饭
                9.孩子背着书包上学校

        - 面向过程的编程思想将一个功能分解为一个一个小的步骤，
            我们通过完成一个一个的小的步骤来完成一个程序
        - 这种编程方式，符合我们人类的思维，编写起来相对比较简单
        - 但是这种方式编写代码的往往只适用于一个功能，
            如果要在实现别的功能，即使功能相差极小，也往往要重新编写代码，
            所以它可复用性比较低，并且难于维护 

    - 面向对象的编程语言
        - 面向对象的编程语言，关注的是对象，而不关注过程 
        - 对于面向对象的语言来说，一切都是对象       
        - 例子：
            1.孩他妈起床叫孩子上学

        - 面向对象的编程思想，将所有的功能统一保存到对应的对象中
            比如，妈妈功能保存到妈妈的对象中，孩子的功能保存到孩子对象中
            要使用某个功能，直接找到对应的对象即可
        - 这种方式编写的代码，比较容易阅读，并且比较易于维护，容易复用。
        - 但是这种方式编写，不太符合常规的思维，编写起来稍微麻烦一点 
    
    - 简单归纳一下，面向对象的思想
        1.找对象
        2.搞对象

## 类(class) 
    - 我们目前所学习的对象都是Python内置的对象
    - 但是内置对象并不能满足所有的需求，所以我们在开发中经常需要自定义一些对象
    - 类，简单理解它就相当于一个图纸。在程序中我们需要根据类来创建对象
    - 类就是对象的图纸！
    - 我们也称对象是类的实例（instance）
    - 如果多个对象是通过一个类创建的，我们称这些对象是一类对象
    - 像 int() float() bool() str() list() dict() .... 这些都是类
    - a = int(10) # 创建一个int类的实例 等价于 a = 10
    - 我们自定义的类都需要使用大写字母开头，使用大驼峰命名法（帕斯卡命名法）来对类命名

    - 类也是一个对象！
    - 类就是一个用来创建对象的对象！
    - 类是type类型的对象，定义类实际上就是定义了一个type类型的对象

    a = int(10)         创建一个int实例
    b= str('hello')     创建一个str实例

    定义类
        使用class关键字来定义类，语法和函数很像！
            class 类名([父类]):
                代码块
        class MyClass():
            pass
        print(MyClass,type(MyClass))      <class '__main__.MyClass'>    <class 'type'>
    
    使用类来创建对象，就像调用一个函数一样
        mc = MyClass()
        print(mc,type(mc))              <__main__.MyClass object at 0x00000203224A6860>  <class '__main__.MyClass'>
    isinstance()用来检查一个对象是否是一个类的实例
        result = isinstance(mc,MyClass)         true

    为类定义属性和方法
        class Person() :
            name = 'xiaoming'
            def say_hello(self):    定义方法时候必须定义一个形参self,创建实例时候python会自动传入这个参数
                #方法每次被调用时，解析器都会自动传递第一个实参
                # 第一个参数，就是调用方法的对象本身，
                #   如果是p1调的，则第一个参数就是p1对象
                #   如果是p2调的，则第一个参数就是p2对象
                # 一般我们都会将这个参数命名为self
                print('你好，我是%s'%self.name)
        p1 = Person()
        p2 = Person()
        p1.say_hello()          你好，我是xiaoming
        p2.say_hello()          你好，我是xiaoming
        print(p1.name,p2.name)  xiaoming,xiaoming

    在类中可以定义一些特殊方法（魔术方法）
        特殊方法都是以__开头，__结尾的方法
        特殊方法不需要我们自己调用，不要尝试去调用特殊方法
        __init__可以用来向新创建的对象中初始化属性
        __init__可以用来向新创建的对象中初始化属性
        调用类创建对象时，类后边的所有参数都会依次传递到__init__()中
        
        class Person:
            def __init__(self,name):
                self.name = name
            def say_hello(self):
                print('大家好，我是%s'%self.name)
        p1 = Person('xiaohong')         现在创建person实例必须传入一个值，否则会报错

## 面向对象三大特性之封装
    封装指的是隐藏对象中一些不希望被外部所访问到的属性或方法
    如何隐藏一个对象中的属性？
        - 将对象的属性名，修改为一个外部不知道的名字
    如何获取（修改）对象中的属性？
        - 需要提供一个getter和setter方法使外部可以访问到属性
        - getter 获取对象中的指定属性（get_属性名）
        - setter 用来设置对象的指定属性（set_属性名）

        class Rectangle:
            def __init__(self,width,height):
                self.hidden_width = width
                self.hidden_height = height
            def get_width(self):
                return self.hidden_width
            def get_height(self):
                return self.hidden_height
            def set_width(self,width):
                self.hidden_width = width
            def set_height(self,width):
                self.hidden_height = height
        以上定义类实质上是改变了属性名，如果修改者知道名字为hidden_width,仍然可以通过创建实例去改变
        例：
            r = Rectangle(1,2)
            r.hidden_width = 3
            r.get_width()

        可以为对象的属性使用双下划线开头，__xxx
            双下划线开头的属性，是对象的隐藏属性，隐藏属性只能在类的内部访问，无法通过对象访问
            其实隐藏属性只不过是Python自动为属性改了一个名字
                实际上是将名字修改为了，_类名__属性名 比如 __name -> _Person__name
            class Person:
                def __init__(self,name):
                    self.__name = name
                def get_name(self):
                    return self.__name
                def set_name(self,name):
                    self.__name = name
            p = Person('xiaohuang')
            p.__name = 'xiaohong'           会报错
        
        property装饰器，用来将一个get方法，转换为对象的属性
            添加为property装饰器以后，我们就可以像调用属性一样使用get方法
            使用property装饰的方法，必须和属性名是一样的
            class Person:
                def __init__(self,name,age):
                    self._name = name
                    self._age = age

                @property
                def name(self):
                    print('get方法')
                    return self._name
                # setter方法的装饰器：@属性名.setter
                @name.setter
                def name(self,name):
                    print('set方法')
                    self._name = name
                @property
                def age(self):
                    print('get方法')
                    return self._age
                # setter方法的装饰器：@属性名.setter
                @age.setter
                def age(self,age):
                    print('set方法')
                    self._age = age
            
            p = Person('wwwwww',18)
            pring(p.name)           读
            p.name = 'yyyyy'        写

## 面向对象三大特性之继承
    class Animal:
        def run(self):
            print('动物会跑~~~')

        def sleep(self):
            print('动物睡觉~~~')
    class Dog(Animal):
        def bark(self):
            print('汪汪汪~~~') 

        def run(self):
            print('狗跑~~~~')    

    class Hashiqi(Dog):
        def fan_sha(self):
            print('我是一只傻傻的哈士奇') 
    d = Dog()
    h = Hashiqi()
    d.run()
    d.bark()

    在创建类时，如果省略了父类，则默认父类为object
        object是所有类的父类，所有类都继承自object
        print(isinstance(print , object))
    
    issubclass() 检查一个类是否是另一个类的子类
         print(issubclass(Animal , Dog))     True
         print(issubclass(Animal , object))  True

    重写
        当我们调用一个对象的方法时，
        会优先去当前对象中寻找是否具有该方法，如果有则直接调用
        如果没有，则去当前对象的父类中寻找，如果父类中有则直接调用父类中的方法，
        如果没有，则去父类的父类中寻找，以此类推，直到找到object，如果依然没有找到，则报错

    父类中的所有方法都会被子类继承，包括特殊方法，也可以重写特殊方法
        class Animal:
            def __init__(self,name):
                self._name = name
            def run(self):
                print('run')
            @property
            def name(self)：
                return self._name
            @name.setter
            def name(self,name):
                self._name = name
            
        class Dog(Animal):
            def __init__(self,name,age):
                # 希望可以直接调用父类的__init__来初始化父类中定义的属性
                # super() 可以用来获取当前类的父类，
                #   并且通过super()返回对象调用父类方法时，不需要传递self
                super().__init__(name)
                self._age = age
            def bark(self):
                print('bark')
            @property
            def age(self)：
                return self._agee
            @name.setter
            def age(self,age):
                self._age = age

        在Python中是支持多重继承的，也就是我们可以为一个类同时指定多个父类
            可以在类名的()后边添加多个类，来实现多重继承
            多重继承，会使子类同时拥有多个父类，并且会获取到所有父类中的方法
            如果多个父类中有同名的方法，则会现在第一个父类中寻找，然后找第二个，然后找第三个。。。
            前边父类的方法会覆盖后边父类的方法
        class A(object):
            def test(self):
                print('aaa')
        class B(object):
            def test(self):
                print('bbb')
            def test2(self):
                print('test2')
        class C(A,B):
            pass
        c=C()
        C.test()

## 面向对象三大特性之多态
    多态指的是一个对象可以以不同的形态去呈现
        例
            狗（狼狗、藏獒、哈士奇、古牧 。。。）
    
    class A:
        def __init__(self,name):
            self._name = name
        @property
        def name(self):
            return self._name
        @name.setter
        def name(self,name):
            self._name = name
    
    class B：
        def __init__(self,name):
            self._name = name
        def __len__(self):
            return 10
        @property
        def name(self):
            return self._name
        @name.setter
        def name(self,name):
            self._name = name
    
    class C:
        def __len__(self):
            return 12
        pass
    
    定义一个函数
        对于say_hello()这个函数来说，只要对象中含有name属性，它就可以作为参数传递
        这个函数并不会考虑对象的类型，只要有name属性即可

    如果一个东西，走路像鸭子，叫声像鸭子，那么它就是鸭子

    len()就是多态
        之所以一个对象能通过len()来获取长度，是因为对象中具有一个特殊方法__len__
        换句话说，只要对象中具有__len__特殊方法，就可以通过len()来获取它的长度

        l = [1,2,3]
        s = 'hello'
        b = B('xiaoming')
        c = C()
        print(len(l))
        print(len(s))
        print(len(b))
        print(len(c))

## 类中的属性和方法
    分类
        # 类属性
        # 实例属性
        # 类方法
        # 实例方法
        # 静态方法
    class A(object):
        # 类属性，直接在类中定义的属性是类属性
        # 类属性可以通过类或类的实例访问到
        #  但是类属性只能通过类对象来修改，无法通过实例对象修改
        count = 0
        def __init__(self):
            # 实例属性，通过实例对象添加的属性属于实例属性
            # 实例属性只能通过实例对象来访问和修改，类对象无法访问修改
            self.name = 'xiaohong'
        # 实例方法
        # 在类中定义，以self为第一个参数的方法都是实例方法
        # 实例方法在调用时，Python会将调用对象作为self传入  
        # 实例方法可以通过实例和类去调用
        # 当通过实例调用时，会自动将当前调用对象作为self传入
        # 当通过类调用时，不会自动传递self，此时我们必须手动传递self
        def test(self):
            print('这是test方法~~~ ' , self)
        # 类方法    
        # 在类内部使用 @classmethod 来修饰的方法属于类方法
        # 类方法的第一个参数是cls，也会被自动传递，cls就是当前的类对象
        # 类方法和实例方法的区别，实例方法的第一个参数是self，而类方法的第一个参数是cls
        # 类方法可以通过类去调用，也可以通过实例调用，没有区别
        @classmethod
        def test_2(cls):
            print('这是test_2方法，他是一个类方法~~~ ',cls)
            print(cls.count)
        # 静态方法
        # 在类中使用 @staticmethod 来修饰的方法属于静态方法  
        # 静态方法不需要指定任何的默认参数，静态方法可以通过类和实例去调用  
        # 静态方法，基本上是一个和当前类无关的方法，它只是一个保存到当前类中的函数
        # 静态方法一般都是一些工具方法，和当前类无关
        @staticmethod
        def test_3():
            print('test_3执行了~~~')

    a = A()
    a.count = 10
    A.count = 100
    print('A ,',A.count)            A , 100
    print('a ,',a.count)            a , 10
    print('A ,',A.name)             AttributeError: type object 'A' has no attribute 'name'
    print('a ,',a.name)             a,xiaohong
    .test() 等价于 A.test(a)
    A.test_2() 等价于 a.test_2()

## 垃圾回收
    在Python中有自动的垃圾回收机制，它会自动将这些没有被引用的对象删除，
    class A:
        pass
    a = A()
    a = None        此时没有任何的变量对A()对象进行引用，它就是变成了垃圾

## 特殊方法
    也称为魔术方法
        特殊方法都是使用__开头和结尾的
        特殊方法一般不需要我们手动调用，需要在一些特殊情况下自动执行
    class Person(object):
        def __init__(self,name,age):
            self.name = name
            self.age = age
        # __str__（）这个特殊方法会在尝试将对象转换为字符串的时候调用
        # 它的作用可以用来指定对象转换为字符串的结果  （print函数） 
        def __str__(self):
            return 'Person [name=%s,age=%d]'%(self.name,self.age)
        # __repr__()这个特殊方法会在对当前对象使用repr()函数时调用
        # 它的作用是指定对象在 ‘交互模式’中直接输出的效果    
        def __repr__(self):
            return 'Hello'
        # __len__()获取对象的长度

        #继承自object的特殊方法
        # object.__add__(self, other)
        # object.__sub__(self, other)
        # object.__mul__(self, other)
        # object.__matmul__(self, other)
        # object.__truediv__(self, other)
        # object.__floordiv__(self, other)
        # object.__mod__(self, other)
        # object.__divmod__(self, other)
        # object.__pow__(self, other[, modulo])
        # object.__lshift__(self, other)
        # object.__rshift__(self, other)
        # object.__and__(self, other)
        # object.__xor__(self, other)
        # object.__or__(self, other)

        # object.__lt__(self, other) 小于 <
        # object.__le__(self, other) 小于等于 <=
        # object.__eq__(self, other) 等于 ==
        # object.__ne__(self, other) 不等于 !=
        # object.__gt__(self, other) 大于 >
        # object.__ge__(self, other) 大于等于 >= 

        # object.__bool__(self)
        # 可以通过bool来指定对象转换为布尔值的情况
        def __bool__(self):
            return self.age > 17
        # __gt__会在对象做大于比较的时候调用，该方法的返回值将会作为比较的结果
        # 他需要两个参数，一个self表示当前对象，other表示和当前对象比较的对象
        # self > other
        def __gt__(self , other):
            return self.age > other.age

## 模块（module）
    模块化的特点：
       ① 方便开发
       ② 方便维护
       ③ 模块可以复用！

    在Python中一个py文件就是一个模块，要想创建模块，实际上就是创建一个python文件
    注意：模块名要符号标识符的规范

    引入模块(2种方式)
        import 模块名       #模块名就是python文件的名字，不要.py
        import 模块名 as 模块别名
    - 可以引入同一个模块多次，但是模块的实例只会创建一个
    - import可以在程序的任意位置调用，但是一般情况下，import语句都会统一写在程序的开头
    - 在每一个模块内部都有一个__name__属性，通过这个属性可以获取到模块的名字
    - __name__属性值为 __main__的模块是主模块，一个程序中只会有一个主模块
    -  主模块就是我们直接通过 python 执行的模块
    例：在index.py中引入test_module.py模块
        import test_module as test
        print(test.__name__)        # test_module
        print(__name__)            #  __main__

    访问模块中的变量：模块名.变量名
        import m
        print(m.name,m.age,m.test())
        def test2():
            print('这是主模块中的test2')
        
    只引入模块中的部分内容
        语法
            from 模块名 import 变量,变量。。。
        例
            from m import Person        #引入单个
            from m import Person,test   #引入多个
            from m import *         #引入模块中所有内容，一般不会使用
            from m import test as new_test2  #用别名
        
            p1=Person()
            test()          #主模块的test方法
            new_test2()     #引入模块的test方法
    
    总结-引入模块的所有方式
        # import xxx
        # import xxx as yyy
        # from xxx import yyy , zzz , fff
        # from xxx import *
        # from xxx import yyy as zz

## 包 Package
    包也是一个模块
    当我们模块中代码过多时，或者一个模块需要被分解为多个模块时，这时就需要使用到包
    普通的模块就是一个py文件，而包是一个文件夹
    包中必须要一个一个 __init__.py 这个文件，这个文件中可以包含有包中的主要内容

    例：
        目录
        hello                       #包名
            - __pycache__           #模块的缓存文件-自动生成
            - __init__.py           #必须包含这个文件
            - a.py                  #包中的模块a
            - b.py

        from hello import a,b

        # __pycache__ 是模块的缓存文件
        # py代码在执行前，需要被解析器先转换为机器码，然后再执行
        #   所以我们在使用模块（包）时，也需要将模块的代码先转换为机器码然后再交由计算机执行
        #   而为了提高程序运行的性能，python会在编译过一次以后，将代码保存到一个缓存文件中
        #   这样在下次加载这个模块（包）时，就可以不再重新编译而是直接加载缓存中编译好的代码即可

## Python标准库
    # 在这个标准库中，有很多很强大的模块我们可以直接使用，
    #   并且标准库会随Python的安装一同安装
    # sys模块，它里面提供了一些变量和函数，使我们可以获取到Python解析器的信息
    #   或者通过函数来操作Python解析器
    # 引入sys模块
        import sys

    # pprint 模块它给我们提供了一个方法 pprint() 该方法可以用来对打印的数据做简单的格式化
        import pprint

    # sys.argv
    # 获取执行代码时，命令行中所包含的参数
    # 该属性是一个列表，列表中保存了当前命令的所有参数
    # print(sys.argv)

    # sys.modules
    # 获取当前程序中引入的所有模块
    # modules是一个字典，字典的key是模块的名字，字典的value是模块对象
    # pprint.pprint(sys.modules)

    # sys.path
    # 他是一个列表，列表中保存的是模块的搜索路径
    # ['C:\\Users\\lilichao\\Desktop\\resource\\course\\lesson_06\\code',
    # 'C:\\dev\\python\\python36\\python36.zip',
    # 'C:\\dev\\python\\python36\\DLLs',
    # 'C:\\dev\\python\\python36\\lib',
    # 'C:\\dev\\python\\python36',
    # 'C:\\dev\\python\\python36\\lib\\site-packages']
    # pprint.pprint(sys.path)

    # sys.platform
    # 表示当前Python运行的平台
    # print(sys.platform)

    # sys.exit()
    # 函数用来退出程序
    # sys.exit('程序出现异常，结束！')
    # print('hello')

    # os 模块让我们可以对操作系统进行访问
        import os

    # os.environ
    # 通过这个属性可以获取到系统的环境变量
    # pprint.pprint(os.environ['path'])

    # os.system()
    # 可以用来执行操作系统的名字
    # os.system('dir')
    os.system('notepad')

## 处理异常
    程序运行时出现异常，Hui   

    try语句
        try:
            代码块（可能出现错误的语句）
        except 异常类型 as 异常名:
            代码块（出现错误以后的处理方式）
        except 异常类型 as 异常名:
            代码块（出现错误以后的处理方式）
        except 异常类型 as 异常名:
            代码块（出现错误以后的处理方式）
        else：
            代码块（没出错时要执行的语句）    
        finally:
            代码块（该代码块总会执行）    

        try是必须的 else语句有没有都行
        except和finally至少有一个    

    可以将可能出错的代码放入到try语句，这样如果代码没有错误，则会正常执行，
        如果出现错误，则会执行expect子句中的代码，这样我们就可以通过代码来处理异常
        避免因为一个异常导致整个程序的终止     

    异常类
        try:
            print(10/0)
        except NameError:               # 如果except后不跟任何的内容，则此时它会捕获到所有的异常
            print('出现 NameError 异常')     
        except ZeroDivisionError:
            print('出现 ZeroDivisionError 异常')  
        except IndexError:
            print('出现 IndexError 异常')
        except Exception as e:          # Exception 是所有异常类的父类，所以如果except后跟的是Exception，他也会捕获到所有的异常 as ...是别名
            print('未知异常',e,type(e))
        finally:
            print('无论是否出现异常，该子句都会执行')

    自定义异常
        创建一个类继承Exception即可
        class  MyError(Exception):
            pass
        def add(a,b):
            if a<0 or b>0:
                raise MyError('自定义的异常')       # raise用于向外部抛出异常，后边可以跟一个异常类，或异常类的实例 raise Exception
            r = a+b
            return r
        print(add(-12,45))

## 异常的传播（抛出异常）
    当在函数中出现异常时，如果在函数中对异常进行了处理，则异常不会再继续传播,
        如果函数中没有对异常进行处理，则异常会继续向函数调用处传播,
        如果函数调用处处理了异常，则不再传播，如果没有处理则继续向调用处传播
        直到传递到全局作用域（主模块）如果依然没有处理，则程序终止，并且显示异常信息

    当程序运行过程中出现异常以后，所有的异常信息会被保存一个专门的异常对象中，
        而异常传播时，实际上就是异常对象抛给了调用处
        比如 ： ZeroDivisionError类的对象专门用来表示除0的异常
                NameError类的对象专门用来处理变量错误的异常
                ....

    在Python为我们提供了多个异常对象            

## 抛出异常
    - 可以使用 raise 语句来抛出异常，
        raise语句后需要跟一个异常类 或 异常的实例

## 文件（File）
    - 通过Python程序来对计算机中的各种文件进行增删改查的操作
    - I/O(Input / Output)
    - 操作文件的步骤：
        ① 打开文件
        ② 对文件进行各种操作（读、写），然后保存
        ③ 关闭文件

## 打开文件
    open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)

    使用open函数来打开一个文件
        参数：
            file 要打开的文件的名字（路径）
        返回值：
            返回一个对象，这个对象就代表了当前打开的文件
        
        file_name = 'demo.txt'  # 如果目标文件和当前文件在同一级目录下，则直接使用文件名即可
        file_name = 'hello\\demo.txt'       #\转义\
        file_name = 'hello/demo.txt'        #在window下可以使用/代替\
        file_name = r'hello\demo.txt'       #使用原始字符串r
        file_name = r'C:\Users\lilichao\Desktop\hello.txt'      #如果目标文件距离当前文件比较远，此时可以使用绝对路径

        例：
            # 使用open打开文件
            file_name = 'demo.txt'
            file_obj = open(file_name)
            # 使用read方法读取文件内容
            content = file_obj.read()
            # 关闭文件
            file_obj.close()
    
    使用with ... as语句自动关闭文件
        with open(file_name) as file_obj:
            print(file_obj.read())          # 一旦with结束则文件会自动close()
    
    捕获文件不存在异常
        try:
            with open(file_name) as file_obj:
                print(file_obj.read())
        except FileNotFoundError:
            print('文件不存在')

    open()函数补充-读取中文字符和mp3等二进制文件
        文件分类
            1.纯文本文件(使用utf-8编码)
            2.二进制文件(图片，视频，音频，ppt等)
        open打开文件默认是文本文件形式，默认编码类型是None
        例子
            file_name = 'demo2.txt'     #中文文件
            # 处理文本文件时，必须指定文件编码
            try:
                with open(file_name,encoding='utf-8') as file_obj:
                    help(file_obj.read)     #获取read函数帮助
                    #read接收一个size参数,默认-1，读取所有字符,修改size读取希望读取的长度
                    content = file_obj.read(6)
            except FileNotFoundError:
                pass

        读取大文件的正确方式
            file_name = 'demo2.txt'     #中文文件
            try:
                with open(file_name,encoding='utf-8') as file_obj：
                    file_content = ''       # 内容，用来叠加
                    chunk = 100             # 每次读取的长度
                    while True:
                        content = file_obj.read(chunk)
                        # 当读完的时候退出循环
                        if not content:
                            bread
                        file_content += content
            except FileNotFoundError:
                pass
            print(file_content)
    
    readline()以行来读取
        file_name = 'demo.txt'
        with open(file_name,encoding='utf-8') as file_obj:
            print(file_obj.readline(),end='')

    readlines()该方法用于一行一行的读取内容，它会一次性将读取到的内容封装到一个列表中返回
        import pprint
        import os
        file_name = 'demo.txt'
        with open(file_name,encoding='utf-8') as file_obj:
            r = file_obj.readlines()
            pprint.print(r[0])
            pprint.print(r[1])
            pprint.print(r[2])
    
    用for读取内容
        file_name = 'demo.txt'
        with open(file_name,encoding='utf-8') as file_obj:
            for t in file_obj:
                print(t)
            
    读二进制文件
        # 读取模式
        # r 读取文本文件（默认值）
        # b 读取二进制文件
        file_name = 'c:/Users/lilichao/Desktop/告白气球.flac'
        with open(file_name,'rb') as file_obj:
            # 读取文本文件时，size是以字符为单位的
            # 读取二进制文件时，size是以字节为单位
            <!-- print(file_obj.read(100)) -->
            # 把读到的内容写出来
            new_name = 'aa.flac'
            with open(new_name,'wb') as new_obj:
                chunk = 1024*100        #每次读的大小
                while True:
                    content = file_obj.read(chunk)      # 从已有的对象中读取数据
                    if not content:
                        break
                    new_obj.write(content)       # 将读取到的数据写入到新对象中


## 写文件
    使用open()打开文件时必须要指定打开文件所要做的操作（读、写、追加）
        如果不指定操作类型，则默认是 读取文件 ， 而读取文件时是不能向文件中写入的
    r   只读
    w   可写-文件不存在时创建，如果存在会覆盖原来的内容
    a   追加-文件不存在时创建，如果存在会追加内容
    x   新建文件，不存在时创建，存在则报错
    +   为操作符扩展功能
    r+  可读可写，文件不存在会报错
    w+
    a+

    file_name = 'demo5.txt'
    with open(file_name , 'w' , encoding='utf-8') as file_obj:
        # write()来向文件中写入内容，
        # 如果操作的是一个文本文件的话，则write()需要传递一个字符串作为参数
        # 该方法会可以分多次向文件中写入内容
        # 写入完成以后，该方法会返回写入的字符的个数
        file_obj.write('aaa\n')
        file_obj.write('bbb\n')
        file_obj.write('ccc\n')
        r = file_obj.write(str(123)+'123123\n')
        r = file_obj.write('今天天气真不错')
        print(r)                        # 7 只有最后一次的写入
    
## 读取文件位置
    seek()需要两个参数
        第一个 是要切换到的位置
        第二个 计算位置方式
            可选值：
            0 从头计算，默认值
            1 从当前位置计算
            2 从最后位置开始计算
    tell() 方法用来查看当前读取的位置
    with open('demo.txt','rb') as file_obj:
        print(file_obj.read(100))
        file_obj.seek(55)       # seek() 可以修改当前读取的位置

## 文件的其他操作
    import os
    from pprint import pprint
    # os.listdir() 获取指定目录的目录结构
    # 需要一个路径作为参数，会获取到该路径下的目录结构，默认路径为 . 当前目录
    # 该方法会返回一个列表，目录中的每一个文件（夹）的名字都是列表中的一个元素
    pprint(os.listdir())    #返回一个数组，包含该目录下的所有文件
    # os.getcwd() 获取当前所在的目录
    pprint(os.getcwd())     #'D:\\资料\\尚硅谷Python核心基础\\01-代码-笔记\\01-代码-笔记\\lesson_07_异常和文件\\code'
    # os.chdir() 切换当前所在的目录 作用相当于 cd
    # os.chdir('c:/')
    # 创建目录
    # os.mkdir("aaa") # 在当前目录下创建一个名字为 aaa 的目录
    # 删除目录
    # os.rmdir('abc')
    # 删除文件
    # os.remove('aa.txt')
    # os.rename('旧名字','新名字') 可以对一个文件进行重命名，也可以用来移动一个文件
    # os.rename('aa.txt','bb.txt')
