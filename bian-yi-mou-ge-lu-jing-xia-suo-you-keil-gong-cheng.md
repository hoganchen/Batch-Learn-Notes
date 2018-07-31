### For语句的用法

    @echo off
    set PATH=%PATH%;C:\Keil_v5\UV4;C:\Keil_v5\ARM\ARMCC\Bin;

    if not exist build_log (
        mkdir build_log
    ) else (
        del /s /q build_log
    )

    set curpwd=%cd%
    cd /d ..\..\new_app\projects\peripheral

    for /f %%i in ('dir *.uvprojx /s /b') do (
        for /f %%j in ("%%i\..") do (
            cd /d %%~fj
            echo %%~nxi

            for /f "delims=<> tokens=3" %%k in ('findstr "<TargetName>" %%~nxi') do (
                echo Command: "UV4 -j0 -r %%~nxi -t %%k -o %curpwd%\build_log\%%~ni.txt"

                UV4 -j0 -r %%~nxi -t %%k -o %curpwd%\build_log\%%~ni.txt
                type %curpwd%\build_log\%%~ni.txt
            )
        )
    )

    cd /d %curpwd%

    for /f %%i in ('dir build_log\*.txt /s /b') do (
        echo;
        echo;
        echo ################################################################################
        echo For %%~ni project, build result:
        echo ################################################################################
        findstr "Warning(s)" %%i
    )

    pause

    D:\BALBOA_SW\00_SW\00_SW_DEV\misc\compile_test>for /?
    对一组文件中的每一个文件执行某个特定命令。

    FOR %variable IN (set) DO command [command-parameters]

      %variable  指定一个单一字母可替换的参数。
      (set)      指定一个或一组文件。可以使用通配符。
      command    指定对每个文件执行的命令。
      command-parameters
                 为特定命令指定参数或命令行开关。

    在批处理程序中使用 FOR 命令时，指定变量请使用 %%variable
    而不要用 %variable。变量名称是区分大小写的，所以 %i 不同于 %I.

    如果启用命令扩展，则会支持下列 FOR 命令的其他格式:

    FOR /D %variable IN (set) DO command [command-parameters]

        如果集中包含通配符，则指定与目录名匹配，而不与文件名匹配。

    FOR /R [[drive:]path] %variable IN (set) DO command [command-parameters]

        检查以 [drive:]path 为根的目录树，指向每个目录中的 FOR 语句。
        如果在 /R 后没有指定目录规范，则使用当前目录。如果集仅为一个单点(.)字符，
        则枚举该目录树。

    FOR /L %variable IN (start,step,end) DO command [command-parameters]

        该集表示以增量形式从开始到结束的一个数字序列。因此，(1,1,5)将产生序列
        1 2 3 4 5，(5,-1,1)将产生序列(5 4 3 2 1)

    FOR /F ["options"] %variable IN (file-set) DO command [command-parameters]
    FOR /F ["options"] %variable IN ("string") DO command [command-parameters]
    FOR /F ["options"] %variable IN ('command') DO command [command-parameters]

        或者，如果有 usebackq 选项:

    FOR /F ["options"] %variable IN (file-set) DO command [command-parameters]
    FOR /F ["options"] %variable IN ("string") DO command [command-parameters]
    FOR /F ["options"] %variable IN ('command') DO command [command-parameters]

        fileset 为一个或多个文件名。继续到 fileset 中的下一个文件之前，
        每份文件都被打开、读取并经过处理。处理包括读取文件，将其分成一行行的文字，
        然后将每行解析成零或更多的符号。然后用已找到的符号字符串变量值调用 For 循环。
        以默认方式，/F 通过每个文件的每一行中分开的第一个空白符号。跳过空白行。
        您可通过指定可选 "options" 参数替代默认解析操作。这个带引号的字符串包括一个
        或多个指定不同解析选项的关键字。这些关键字为:

            eol=c           - 指一个行注释字符的结尾(就一个)
            skip=n          - 指在文件开始时忽略的行数。
            delims=xxx      - 指分隔符集。这个替换了空格和跳格键的
                              默认分隔符集。
            tokens=x,y,m-n  - 指每行的哪一个符号被传递到每个迭代
                              的 for 本身。这会导致额外变量名称的分配。m-n
                              格式为一个范围。通过 nth 符号指定 mth。如果
                              符号字符串中的最后一个字符星号，
                              那么额外的变量将在最后一个符号解析之后
                              分配并接受行的保留文本。
            usebackq        - 指定新语法已在下类情况中使用:
                              在作为命令执行一个后引号的字符串并且一个单
                              引号字符为文字字符串命令并允许在 file-set
                              中使用双引号扩起文件名称。

        某些范例可能有助:

    FOR /F "eol=; tokens=2,3* delims=, " %i in (myfile.txt) do @echo %i %j %k

        会分析 myfile.txt 中的每一行，忽略以分号打头的那些行，将
        每行中的第二个和第三个符号传递给 for 函数体，用逗号和/或
        空格分隔符号。请注意，此 for 函数体的语句引用 %i 来
        获得第二个符号，引用 %j 来获得第三个符号，引用 %k
        来获得第三个符号后的所有剩余符号。对于带有空格的文件
        名，您需要用双引号将文件名括起来。为了用这种方式来使
        用双引号，还需要使用 usebackq 选项，否则，双引号会
        被理解成是用作定义某个要分析的字符串的。

        %i 在 for 语句中显式声明，%j 和 %k 是通过
        tokens= 选项隐式声明的。可以通过 tokens= 一行
        指定最多 26 个符号，只要不试图声明一个高于字母 "z" 或
        "Z" 的变量。请记住，FOR 变量是单一字母、分大小写和全局的变量；
        而且，不能同时使用超过 52 个。

        还可以在相邻字符串上使用 FOR /F 分析逻辑，方法是，
        用单引号将括号之间的 file-set 括起来。这样，该字符
        串会被当作一个文件中的一个单一输入行进行解析。

        最后，可以用 FOR /F 命令来分析命令的输出。方法是，将
        括号之间的 file-set 变成一个反括字符串。该字符串会
        被当作命令行，传递到一个子 CMD.EXE，其输出会被捕获到
        内存中，并被当作文件分析。如以下例子所示:

          FOR /F "usebackq delims==" %i IN (`set`) DO @echo %i

        会枚举当前环境中的环境变量名称。

    另外，FOR 变量参照的替换已被增强。您现在可以使用下列
    选项语法:

         %~I          - 删除任何引号(")，扩展 %I
         %~fI        - 将 %I 扩展到一个完全合格的路径名
         %~dI        - 仅将 %I 扩展到一个驱动器号
         %~pI        - 仅将 %I 扩展到一个路径
         %~nI        - 仅将 %I 扩展到一个文件名
         %~xI        - 仅将 %I 扩展到一个文件扩展名
         %~sI        - 扩展的路径只含有短名
         %~aI        - 将 %I 扩展到文件的文件属性
         %~tI        - 将 %I 扩展到文件的日期/时间
         %~zI        - 将 %I 扩展到文件的大小
         %~$PATH:I   - 查找列在路径环境变量的目录，并将 %I 扩展
                       到找到的第一个完全合格的名称。如果环境变量名
                       未被定义，或者没有找到文件，此组合键会扩展到
                       空字符串

    可以组合修饰符来得到多重结果:

         %~dpI       - 仅将 %I 扩展到一个驱动器号和路径
         %~nxI       - 仅将 %I 扩展到一个文件名和扩展名
         %~fsI       - 仅将 %I 扩展到一个带有短名的完整路径名
         %~dp$PATH:I - 搜索列在路径环境变量的目录，并将 %I 扩展
                       到找到的第一个驱动器号和路径。
         %~ftzaI     - 将 %I 扩展到类似输出线路的 DIR

    在以上例子中，%I 和 PATH 可用其他有效数值代替。%~ 语法
    用一个有效的 FOR 变量名终止。选取类似 %I 的大写变量名
    比较易读，而且避免与不分大小写的组合键混淆。

    D:\BALBOA_SW\00_SW\00_SW_DEV\misc\compile_test>set /?
    显示、设置或删除 cmd.exe 环境变量。

    SET [variable=[string]]

      variable  指定环境变量名。
      string    指定要指派给变量的一系列字符串。

    要显示当前环境变量，键入不带参数的 SET。

    如果命令扩展被启用，SET 会如下改变:

    可仅用一个变量激活 SET 命令，等号或值不显示所有前缀匹配
    SET 命令已使用的名称的所有变量的值。例如:

        SET P

    会显示所有以字母 P 打头的变量

    如果在当前环境中找不到该变量名称，SET 命令将把 ERRORLEVEL
    设置成 1。

    SET 命令不允许变量名含有等号。

    在 SET 命令中添加了两个新命令行开关:

        SET /A expression
        SET /P variable=[promptString]

    /A 命令行开关指定等号右边的字符串为被评估的数字表达式。该表达式
    评估器很简单并以递减的优先权顺序支持下列操作:

        ()                  - 分组
        ! ~ -               - 一元运算符
        * / %               - 算数运算符
        + -                 - 算数运算符
        << >>               - 逻辑移位
                           - 按位“与”
        ^                   - 按位“异”
        |                   - 按位“或”
        = *= /= %= += -=    - 赋值
          &= ^= |= <<= >>=
        ,                   - 表达式分隔符

    如果您使用任何逻辑或取余操作符， 您需要将表达式字符串用
    引号扩起来。在表达式中的任何非数字字符串键作为环境变量
    名称，这些环境变量名称的值已在使用前转换成数字。如果指定
    了一个环境变量名称，但未在当前环境中定义，那么值将被定为
    零。这使您可以使用环境变量值做计算而不用键入那些 % 符号
    来得到它们的值。如果 SET /A 在命令脚本外的命令行执行的，
    那么它显示该表达式的最后值。该分配的操作符在分配的操作符
    左边需要一个环境变量名称。除十六进制有 0x 前缀，八进制
    有 0 前缀的，数字值为十进位数字。因此，0x12 与 18 和 022
    相同。请注意八进制公式可能很容易搞混: 08 和 09 是无效的数字，
    因为 8 和 9 不是有效的八进制位数。(& )

    /P 命令行开关允许将变量数值设成用户输入的一行输入。读取输入
    行之前，显示指定的 promptString。promptString 可以是空的。

    环境变量替换已如下增强:

        %PATH:str1=str2%

    会扩展 PATH 环境变量，用 "str2" 代替扩展结果中的每个 "str1"。
    要有效地从扩展结果中删除所有的 "str1"，"str2" 可以是空的。
    "str1" 可以以星号打头；在这种情况下，"str1" 会从扩展结果的
    开始到 str1 剩余部分第一次出现的地方，都一直保持相配。

    也可以为扩展名指定子字符串。

        %PATH:~10,5%

    会扩展 PATH 环境变量，然后只使用在扩展结果中从第 11 个(偏
    移量 10)字符开始的五个字符。如果没有指定长度，则采用默认
    值，即变量数值的余数。如果两个数字(偏移量和长度)都是负数，
    使用的数字则是环境变量数值长度加上指定的偏移量或长度。

        %PATH:~-10%

    会提取 PATH 变量的最后十个字符。

        %PATH:~0,-2%

    会提取 PATH 变量的所有字符，除了最后两个。

    终于添加了延迟环境变量扩充的支持。该支持总是按默认值被
    停用，但也可以通过 CMD.EXE 的 /V 命令行开关而被启用/停用。
    请参阅 CMD /?

    考虑到读取一行文本时所遇到的目前扩充的限制时，延迟环境
    变量扩充是很有用的，而不是执行的时候。以下例子说明直接
    变量扩充的问题:

        set VAR=before
        if "%VAR%" == "before" (
            set VAR=after
            if "%VAR%" == "after" @echo If you see this, it worked
        )

    不会显示消息，因为在读到第一个 IF 语句时，BOTH IF 语句中
    的 %VAR% 会被代替；原因是: 它包含 IF 的文体，IF 是一个
    复合语句。所以，复合语句中的 IF 实际上是在比较 "before" 和
    "after"，这两者永远不会相等。同样，以下这个例子也不会达到
    预期效果:

        set LIST=
        for %i in (*) do set LIST=%LIST% %i
        echo %LIST%

    原因是，它不会在目前的目录中建立一个文件列表，而只是将
    LIST 变量设成找到的最后一个文件。这也是因为 %LIST% 在
    FOR 语句被读取时，只被扩充了一次；而且，那时的 LIST 变量
    是空的。因此，我们真正执行的 FOR 循环是:

        for %i in (*) do set LIST= %i

    这个循环继续将 LIST 设成找到的最后一个文件。

    延迟环境变量扩充允许您使用一个不同的字符(惊叹号)在执行
    时间扩充环境变量。如果延迟的变量扩充被启用，可以将上面
    例子写成以下所示，以达到预期效果:

        set VAR=before
        if "%VAR%" == "before" (
            set VAR=after
            if "!VAR!" == "after" @echo If you see this, it worked
        )

        set LIST=
        for %i in (*) do set LIST=!LIST! %i
        echo %LIST%

    如果命令扩展被启用，有几个动态环境变量可以被扩展，但不会出现在 SET 显示的变
    量列表中。每次变量数值被扩展时，这些变量数值都会被动态计算。如果用户用这些
    名称中任何一个明确定义变量，那个定义会替代下面描述的动态定义:

    %CD% - 扩展到当前目录字符串。

    %DATE% - 用跟 DATE 命令同样的格式扩展到当前日期。

    %TIME% - 用跟 TIME 命令同样的格式扩展到当前时间。

    %RANDOM% - 扩展到 0 和 32767 之间的任意十进制数字。

    %ERRORLEVEL% - 扩展到当前 ERRORLEVEL 数值。

    %CMDEXTVERSION% - 扩展到当前命令处理器扩展版本号。

    %CMDCMDLINE% - 扩展到调用命令处理器的原始命令行。

    %HIGHESTNUMANODENUMBER% - 扩展到此计算机上的最高 NUMA 节点号。



