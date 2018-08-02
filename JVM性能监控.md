#### 分析Java程序CPU过高情况



1. 执行 top 命令 查看 Java进程占用CPU 情况，找到对应的 PID

   Shift + p  按照 CPU使用率排序   shift + m 按照内存使用率排序

2. 查看PID对应进程 里面线程的 占用CPU时间最高的 线程 PID

   top -Hp pid	

3. 查看 线程PID 的 16进制值 

   printf "%x\n" 2377

4. 使用 jstack 命令，导出 线程堆栈信息  -A 30 显示 含有949字符后面 30行

   jstack 2365 |grep 949 -A 30

   Jstack 2365 > log.txt

   

   

   

   

   

   

   

   

