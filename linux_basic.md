# Linux command line cheat sheat 

## man - 获得帮助
```
man ls        # 许多Linux自带命令可以通过man查看使用帮助
ls --help     # 有些程序可以通过-h, --help查看使用帮助
```
## ls - 显示目录内容
```
ls                      # 显示目录内容
ls -l                   # 以列表显示形式显示目录内容，通常在~/.bashrc文件中增加一行：alias ll='ls -l'
                        # 以后就可以直接使用别名ll了，更方便
ll -h                   # 以人类可读的方式显示文件大小
ll -t                   # 以文件的修改时间排序，最新修改的在最前面
ll -tr                  # 以文件的修改时间排序，最新修改的在最后面
watch -n 3 -dc ls -l    # 追踪目录内容的变化，每3秒刷新一次
```
## pwd - 显示当前目录
```
pwd                 # 显示当前目录的绝对路径
ls `pwd`/file       # 显示文件的绝对路径
```

## cd - 切换目录
```
cd dir    # 切换到目录dir
cd        # 切换到用户的HOME目录
cd ~      # 同cd，~表示HOME目录
cd ..     # 切换到上一级目录；一个点.表示当前目录，两个点..表示上一级目录
cd -      # 切换到进入当前目录之前所在的目录
```

## mkdir - 创建目录
```
mkdir dir           # 创建dir目录
mkdir -p dir1/dir2  # 递归创建目录，如dir1不存在，会先创建dir1
```

## cat - 合并文件（按行）
```
cat file              # 合并一个或多个文件至标准输出，当只有一个文件时，相当于显示所有文件内容
cat file1 file2       # 合并file1和file2的内容，并在屏幕上输出
cat R1.fq.gz R2.fq.gz # 可以合并gzip压缩文件，如测序数据原始reads的合并
```

## paste - 合并文件（按列）
```
paste -d ' ' file1 file2    # 按列对列的方式一行一行合并文件。默认列中间加TAB键， -d参数可以改变列之间的分隔符
```

## split - 分割文件
```
split -d -l 10000 file chunk_   # 按行数分割文件，每个文件最多10000行，分割成的文件名为chunk_01, chunk_02。。。
split -d -b 100m file chunk_    # 按大小分割文件，每个文件最多100m，分割成的文件名为chunk_01, chunk_02。。。
```

## cut - 剪切文件
```
cut -f 1 file                   # 剪切文件的第1列
cut -f 1,2                      # 剪切文件的第1，2列
cut -f 3-                       # 剪切第3列及之后的所有列
cut -d ' ' -f 1 file            # 剪切第1列，但以空格作为列与列之间的分隔符。默认以TAB作为分隔符
grep '^>' test.fa | cut -c 2-   # 得到fasta文件中的序列名称（去掉了>符号）
```

## less, head, tail - 显示文件内容
```
less file       # 分屏显示文件内容，按空格键显示下一页，按下/后可以搜索内容
less -SN file   # 显示文件的行号，并且截断太长的行 
​
head file       # 默认显示文件前10行
head -n 20 file # 显示文件前20行
​
tail file       # 默认显示文件后10行
tail -n 20 file # 显示文件后20行
tail -n +2 file # 跳过第1行，显示从第2行开始的所有行，可用于跳过文件的标题行
tail -f file    # 当文件的内容还在增加时，实时显示末尾增加的内容，常用于查看日志文件的更新情况
```

## wc - 统计文件内容
```
wc -l file      # 统计文件行数
```

## touch - 创建文件
```
touch file                  # 创建一个空文件
touch {file1,file2,file3}   # 同时创建3个文件
```

## cp, mv, rm- 文件/目录的复制，移动，删除
```
scp file1 file2     # 将file1复制一份，命名为file2，复制目录要加-r参数：scp -r
mv file1 dir1/      # 将file1移动到dir1/目录下
mv file1 file2      # 重命名：即将file1移动成为file2
rm file             # 删除文件，删除目录要加-r参数：rm -r
rm -f file          # 文件若不存在，删除时会报错，加-f参数就不会报错
```

## tar - 文件打包/压缩
```
平时tar基本上就能完成打包、压缩、解压的任务了
tar czvf file.tar.gz files  # 打包并压缩
tar xvf file.tar.gz         # 解包，解压缩
​
gzip file                   # 压缩
gunzip file.gz              # 解压
```

## chmod - 改变文件/目录权限
```
chmod +x file   # 增加[本人]可执行权限
chmod -x file   # 取消[本人]可执行权限
chmod a+x file  # 增加[所有人]可执行权限
chmod a-x file  # 取消[所有人]可执行权限
```

## chown - 改变文件/目录归属
```
chown jianzuoyi:jianzuoyi file      # 将文件的所有权给jianzuoyi
chown -R jianzuoyi:jianzuoyi dirname    # 将目录以及目录内的文件的所有权给jianzuoyi
```

## sort, uniq - 排序，去重
```
sort file				# 默认按字典序对文件进行排序
sort -k2,2 -k3,3 file	# 先按第2列排序，第2列相同，再按第3列排序
sort -k2,2n file		# 按第2列排序，且第2列是数字，升序
sort -k2,2nr file		# 按第2列排序，且第2列是数字，降序
sort -u file			# 先排序文件，然后去除相邻的重复行，只保留一条记录
sort file | uniq		# 去除相信的重复行，只保留一条记录，相当于： sort -u file

# 利用sort, uniq取两个文件的交、并、补集
sort a b | uniq			# 并集
sort a b | uniq -d > c	# 交集
sort a c | uniq -u 		# 补集
```

## wget - 下载文件
```
wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh	# 下载文件到当前目录，文件名保持不变
```

## ssh - 远程登录
```
ssh username@host					 # ssh 远程连接至服务器
```

## scp - 远程文件传输
```
scp username@host:/path/to/file .	 # 将远程服务器上的文件传输到当前目录，文件名保持不变，复制目录加参数-r
scp file username@host:/path/to/dir/ # 将本地文件复制到远程服务器，文件名保持不变，复制目录加参数-r
```

## rsync - 远程文件拷贝
```
rsync与scp不同，它只是做增量更新且支持断点续传，也就是要复制的文件存在于目标文件夹且内容与当前要复制的相同，则不会复制。

rsync -azvP dir1 dir2					# 将dir1的内容同步至dir2
rsync -azvP --delete dir1 dir2			# 同步dir2与dir1，dir1中删除的文件，dir2中也要跟着删除
rsync -azvP --exclude 'file' dir1 dir2  # 同步dir2与dir2，且将file排除在外
```

## df, du, free - 查看磁盘/内存使用情况
```
df -h		# 查看磁盘使用情况，-h表示以人类可读的方式显示容量大小
du -sh		# 查看当前目录使用了多少磁盘空间
du -sh *	# 查看当前目录下各文件或文件夹使用的磁盘空间
free -h		# 查看内存使用情况
```

## top, htop, ps, kill - 任务管理
```
top -c		# 查看CPU，内存的使用情况
htop		# top的完美替代品，Linux系统不自带，需要安装， ubuntu系统：apt install htop
ps aut		# 查看后台任务运行情况，第2列是任务的PID号
kill -9 PID # 删除编号为PID的任务
```

## nohup，disown - 远程任务管理
```
nohup ./run.sh &> run.sh.o &	# 远程SSH登录服务器，在后台运行任务，断开远程连接后任务仍然在后台跑
如果运行任务时没有加nohup命令，但任务运行时间长，但又必须断开（比如快下班了），若不想让任务因为断开远程连接而中断，可以用disown命令补救
./run.sh	# 假如任务是直接这样开始跑的
ctrl + z	# 按ctrl + z，将任务放到后台
jobs		# 输入jobs命令，回车，可以看到任务是暂停的： [1]+  Stopped(SIGTSTP)        bash run.sh
bg			# 让后台暂停的任务开始运行
jobs		# 再次运行jobs，可以看到任务已经跑起来了：   [1]+  Running                 bash run.sh &
disown -r 	# 从当前shell中移除运行中的作业，至此，可以关掉终端回家了
```
## | - 管道
```
管道，将前一个命令的输出作为后一个命令的输入

command1 | command2
```
## >, >> - 输入输出重定向
Linux中常用重定向操作符有：

1. 标准输入（/dev/stdin）：代码为0， 使用<或<<
2. 标准输出（/dev/stdout）：代码为1，使用>（覆盖）或>>（追加）
3. 标准错误输出（/dev/stderr）：代码为2，使用2>或2>>
4. &> 标准输出和错误输出同时重定向
5. /dev/null 代表垃圾箱，不想要保存的东西都可以重定向到这里
* 输出重定向就是将命令的结果重定向到文件，而不是输出到屏幕，通常用于保存命令的结果
```
./run.sh > run.sh.o		# 标准输出到run.sh.o日志文件
./run.sh 2> run.sh.e	# 标准错误输出到run.sh.e错误日志文件
./run.sh &> run.sh.log	# 标准输出和标准错误都输出到定一个文件
./run.sh &> /dev/null	# 丢弃标准输出和标准错误信息
```
* 输入重定向是将文件作为输入的来源，而不是键盘
```
command < file			# 将file的内容作为command的输入 
command << END			# 从标准输入（键盘）中读取数据，直到遇到分界符END时停止（分界符用户可以自定义）
command <file1 > file2	# 将file1作为command的输入，并将处理结果输出到file2
```
* 综合运用
```
#!/bin/bash

while read line
do
    do something
done < file.txt > result.txt
```
逐行读入file.txt的内容，处理之后，将结果保存到result.txt文件中。

## find, locate, which - 文件查找
```
find -name file					# 在当前目录查找名为file的文件
find dir/ -name file			# 在dir/目录下查找名为file的文件
find dir/ -name '*file*'		# 在dir/目录下查找包含file关键词的文件，-name参数支持正则表达式
find dir/ -name file -delete	# 查找文件并删除

locate file						# 查找文件
which command					# 显示命令的绝对路径
```
## args - 命令组合工具
```
cat file | xargs		# 将file的内容显示成一行
cat file | xargs -n3	# 将file的内容每3列一行进行输出
find /ifs/result -name '*.fq.gz' | xargs -n1 -I{} cp {} /ifs/data/	# 查找fq.gz文件并复制到/ifs/data目录下
find /ifs/result -name '*.fq.gz' | xargs tar czvf all.fq.gz			# 查找fq.gz文件并打包在一起
find . -type f -name '*.log' -print0 | xargs -0 rm -f				# 当rm文件过多时，可以这样删除
find . -type f -name '*.py' -print0 | xargs -0 wc -l				# 统计一个目录中所有python文件的行数
```
## parallel - 并行工具
parallel是增强版的xargs。假如一个脚本文件中有4条命令：
```
# cat run.sh
echo a
echo b
echo c
echo d

# 同时执行4个任务，生信中常通过这种方式并行执行多个任务
cat run.sh | parallel -j 4	
find *.fq | parallel -j 12 "fastqc {} --outdir ."	# 同时执行12个Fastqc任务
find *.bam | parallel --dry-run 'samtools index {}' # 同时执行samtools index任务，--dry-run显示任务命令但不实际执行，用于命令检查
```

## useradd - 添加用户
```
useradd -m username	# 创建用户并为其在/home下创建一个以其名称命名的目录
```
## passwd - 更改密码
```
passwd	    	   # 更改当前用户的密码
passwd username	   # 更改指定用户的密码
```

## dos2unix - 文件格式转换
```
Linux很多工具都是针对纯文本文件的，并且需要是Unix-like格式的文本文件。但是很多时候文件是从Windows或Mac系统上传到Linux服务器上的，这可能导致文件格式不兼容，原因是不同平台生成的文本文件的换行符不一样。

操作系统	符号	正则表达式
cat -A file				# 查看文件换行符情况
dos2unix file			# Windows格式转换成Unix-like格式
```

## grep 用于查找文件里符合条件的字符串。
```
grep [-abcEFGhHilLnqrsvVwxy][-A<显示列数>][-B<显示列数>][-C<显示列数>][-d<进行动作>][-e<范本样式>][-f<范本文件>][--help][范本样式][文件或目录...]
grep pattern files			 # 搜索文件中包含pattern的行
grep -v pattern files		 # 搜索文件中不包含pattern的行

grep -f pattern.txt files	 # 搜索的pattern来自于文件中
grep -i pattern files		 # 不区分大小写。默认搜索是区分大小写的
grep -i pattern files		 # 只匹配整个单词，而不是字符串的一部分（如搜索hello，不会匹配到helloworld）
grep -n pattern files		 # 显示行号信息
grep -c pattern files		 # 显示匹配的行数
grep -l pattern files		 # 只显示匹配的文件名
grep -L pattern files		 # 显示不匹配的文件名
grep -C number pattern files # 额外显示匹配行的上下[number]行
grep pattern1 | grep pattern2 files # 显示既匹配pattern1，又匹配pattern2的行
grep -E "pattern1|pattern2" files	# 显示匹配pattern1或者pattern2的行, grep -E相当于egrep

# 用于搜索的特殊字符
^: 表示行前
$: 表示行尾

grep '^#' result.vcf		# 显示VCF文件的表头信息
grep '^hello$' files		# 显示只包含hello的行
grep -v '^\s*$' file		# 删除空白行
```

## sed

sed是stream editor的缩写，中文称之为“流编辑器”。
```
sed command file
```
* command部分，针对每行要进行的处理
* file，要处理的文件
### Actions
* d：删除该行
* p：打印该行
* i：在行的前面插入新行
* a：在行的后面插入新行
* r：读取指定文件的内容。
* w：写入指定文件。
```
sed -n '10p' file		# 显示第10行
sed -n '10,20p' file	# 显示第10到20之间的行
sed -n '/pattern/p' file# 显示含有pattern的行
sed -n '/pattern1/,/pattern2/p' file # 显示patter1与pattern2之间的行

sed '10d' file			# 删除第10行
sed '10,20d' file		# 删除第10到20之间的行
sed '/pattern/d'		# 删除匹配pattern的行
sed '/^\s*$/d' file		# 删除空白行
sed 's/^\s*//' file		# 删除行前的空白：空格，制表符
sed 's/\s*$//' file		# 删除行尾的空白：空格，制表符
sed 's/^\s*//;s/\s*$//' file # 删除行首和行尾的空白：空格，制表符

sed 's/AA/BB/' file		# 将文件中的AA替换成BB，只替换一行中第一次出现的AA，替换后的结果输出到屏幕
sed 's/AA/BB/g' file	# 将文件中的所有AA都替换成BB，替换后的结果输出到屏幕
sed -i 's/AA/BB/g' file # 将文件中的所有AA都替换成BB，直接更改文件的内容
sed '/CC/s/AA/BB/g' file# 只替换那些含有CC的行
sed 's/pattern/&XXXX/' file	# 在pattern之后加上XXXX。&表示之前被匹配的内容
sed 's/pattern.*/&XXXX' file# 在匹配pattern的行尾加上XXXX。pattern.*表示包含pattern的整行内容

sed -n '1~4s/^@/>/p;2~4p' file.fq > file.fa	# Fastq文件转Fasta文件
sed -n '2~4p' file.fq		# 提取Fastq文件的序列

sed 'y/ABC/XYZ/' file	# 将ABC逐字替换成XYZ

sed '1i\hello' file		# 在第1行前面插入一行，内容为hello，通常用来为文件增加标题
sed '1a\hello' file		# 在第1行后面插入一行，内容为hello
sed '1r file2' file1	# 在第1行后面读入file2的内容
sed '/pattern/w file2' file1 # 将匹配的行写入file2中
```
## awk
Awk是一个强大的文本分析工具，它每次读入一条记录，并把每条记录切分成字段后进行分析。Awk官方文档是非常好的学习材料，通过man awk查看。

awk 'BEGIN { action } pattern { action } END { action }'
### Awk程序通常是一系列 pattern {action}对：

`pattern`，表示模式匹配，只处理匹配的行。pattern可以省略，表示匹配所有行

`action`，表示对匹配行所做的动作。{actions}可以省略，表示{ print }。BEGIN和END的{action}不能省略



#### pattern可能是：

`BEGIN`， 执行初始化操作，程序开始时执行一次

`END`，执行收尾工作，程序结束时执行一次

`expression`，一个表达式，既可以是判断语句，也可以是正则表达式

#### 常用参数
* `-F value` 设置域分隔符，相当于给FS内置变量赋值
* `-v var=value` 将变量value的值赋给程序变量var，-v可以多次使用

#### 记录与字段
记录是一次读入的内容，通常是文件的一行，保存在字段变量$0中，记录可以被分割成字段，保存在变量$1，$2，...，$NF中。

#### 表达式与操作符
Awk表达式的符号与C语言的类似，基本的表达式有数字，字符串，变量，字段，数组以及函数调用。变量无需声明，它们在首次使用时被初始化为null。
```
assignment          =  +=  -=  *=  /=  %=  ^=
conditional         ?  :
logical and         &&
logical or          ||
logical not         !
array membership    in
matching       		~   !~
relational          <  >   <=  >=  ==  !=
concatenation       (no explicit operator)
add ops             +  -
mul ops             *  /  %
unary               +  -
exponentiation      ^
inc and dec         ++ -- (both post and pre)
field               $
```
#### 正则表达式
在Awk中语言中，通常测试一个记录、字段或字符串是否与一个正则表达式匹配，匹配返回1，不匹配返回0。正则表达式用两个反斜杠/包围。
```
expr ~ /r/							 # 评估expr是否与r匹配。匹配的意思是expr的一个子串是否在正则表达式r定义的字符串集中。

/r/ { action }, $0 ~ /r/ { action }	 # 两者相同， /r/ 等于 $0 ~ /r/
```
任何表达式都可以放到~和!~右边或者内建的需要正则表达式的地方。在必要的时候，该表达式会被转变成字符串，然后作为一个正则表达式来解释。以下三行awk命令完成同样的功能：输出第5列为10的的行。
```
seq 20 | xargs -n5 > file
# cat file
1 2 3 4 5
6 7 8 9 10
11 12 13 14 15
16 17 18 19 20

awk '$5 ~ /10/' file
awk '$5 ~ "10"' file
awk '$5 ~ 10' file
```

#### 数组
Awk支持一维数组。其表示方法为array[expr]，expr在内部被统一转换成字符串类型，因此A[1]，与A["1"]相同，事实上索引都是“1”。索引为字符串的数组被称为关联数组。expr in array用于判断数组元素array[expr]是否存在。
```
for ( var in array ) statement
```
#### 控制语句
···
if ( expr ) statement
if ( expr ) statement else statement
while ( expr ) statement
do statement while ( expr )
for ( opt_expr ; opt_expr ; opt_expr ) statement
for ( var in array ) statement
continue
break
···
#### 内置变量
* NR - 当前行数
* NF - 当前行的列数
* RS，行分隔符，默认是换行符
* FS，列分隔符，默认是空格和制表符
* ORS，输出行分隔符，默认为换行符
* OFS，输出列分隔符，默认为空格
* FILENAME，当前文件名
#### 内置函数
##### 字符串函数
sub()、substr()、gsub()，sprintf()，index()，length()， match()，split()，tolower(), toupper()

##### 数学函数
sin()，cos(), ...

##### 输入输出

有两个输出语句，print和printf
```
print							# 打印整条记录到标准输出，相当于print $0
print expr1, expr2, ..., exprn	# 打印指定字段到标准输出
printf format, expr-list		# C语言printf函数的重用
```
输入函数getline有以下几种形式：

```
getline							# 读取下一条记录到$0，更新NF，NR和FNR
getline var						# 读取下一条记录到var，更新NR和FNR
getline < file					# 从文件读取记录到$0，更新NF
getline var < file				# 从文件读取记录到var
command | getline				# 通过管道传递command的结果到$0，更新NF
command | getline var			# 通过管道传递command的结果到var
seq 10 | awk '{print $0;getline}'					  # 显示奇数行
seq 10 | awk '{getline; print $0}'					  # 显示偶数行
seq 10 | awk '{getline tmp; print tmp; print $0}'	  # 奇偶行对调

awk 'BEGIN {"date" | getline;close("date");print $0}' # 得到系统当前时间

# fastq转换成fasta
awk '{getline seq; getline comment; getline quality; sub("@", ">", $0); print $0"\n"seq}' file
```
#### 示例
```
awk '{print $0}' file	# 打印整行
awk '{print $1}' file	# 打印第一列
awk '{print $2}' file	# 打印第二列
awk '{print $NF}' file	# 打印最后一列
awk '{print $(NF-1)}' file#打印倒数第二列
awk -F ';' -v OFS='\t' '{print $1,$2,$NF}' file	# 读入的文件以逗号;分隔列，打印第1列，第2列和最后一列，并且打印时以制表符作为列的分隔符
number=10;awk -v n=$number '{print n}' file	# number的值被传给了程序变量n
awk '$2 > 100' file		# 打印第2列大于100的行
awk 'NR>1 && NR<4' file # 打印第2~3行

awk '/EGFR/' file		# 打印含有EGFR的行，相当于grep EGFR file
awk '$1 ~ /EGFR/' file	# 打印第1列含有EGFR的列

# 按指定列去除重复行
# cat file
1 2 3 4 5
6 2 8 9 10
11 12 13 14 15
16 17 18 19 20
awk '!a[$2]++' file		# 第二列出现两次2，只保留第一次出现的那一行，结果如下：
1 2 3 4 5
11 12 13 14 15
16 17 18 19 20

awk '{sum+=$1} END {print sum}' file	# 累加文件的第一列
awk '{sum+=$1} END {print sum/NR}' file	# 求第一列的平均数

# 从含有多条fasta序列的文件中提取指定序列
 awk -v RS=">" '/chr1/ {print $0}' hg19.fa	# 提取chr1的序列
 awk -v RS=">" '/chr1|chr2/ {print $0}' hg19.fa	# 提取chr1和chr2的序列
``` 

## Bash脚本模板
```
#!/bin/bash

command1
command2
...
```
chmod +x run.sh 给run.sh脚本增加可执行权限

执行脚本，以下三种方式都可以：
```
# 脚本在前台执行，标准输出和标准错误输出到屏幕
./run.sh
bash run.sh
sh run.sh		# 前提sh链接到了bash，如果没有，需要root权限执行命令：ln -sf /bin/bash /bin/sh

# 脚本在前台执行，标准输出和标准错误保存到文件
./run.sh &> run.sh.o

# 脚本在后台执行，在最后加上一个&符号
./run.sh &> run.sh.o &

# 脚本在后台执行，并且防断线（长时间运行任务时使用）
nohup ./run.sh &> run.sh.o &
```

## 其他命令
```
echo $PATH		# 显示环境变量
time command	# 显示命令执行时间
date			# 显示日期和时间
history			# 显示历史命令
export PATH=$PATH:/path/to/bin	# 将路径加入环境变量中
ln -s file file2# 为file文件创建软链接，名称为file2
exit			# 退出登录
Tab键自动补全	 # Tab键可以补全命令或文件路径，输入部分命令或路径时，尝试按Tab键补全
Ctrl + c		# 中止当前命令的执行
seq 10			# 产生1到10的整数
md5sum			# 生成，或验证文件的MD5值
```

## 终端快捷键
```
Ctrl – a ：移到行首
Ctrl – e ：移到行尾
Ctrl – b ：往回(左)移动一个字符
Ctrl – f ：往后(右)移动一个字符
Alt – b ：往回(左)移动一个单词
Alt – f ：往后(右)移动一个单词
Ctrl – xx ：在命令行尾和光标之间移动
M-b ：往回(左)移动一个单词
```

Copy from https://zhuanlan.zhihu.com/p/302596162?utm_source=wechat_session&utm_medium=social&utm_oi=1005880655431024640&utm_campaign=shareopn
