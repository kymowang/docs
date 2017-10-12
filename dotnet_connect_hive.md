今天花了一天的时间研究了一下dot连接hive的问题，做下记录

1. 截止到目前（2017.10），Apache官方提供的hive ODBC驱动只支持HiveServer1，也就是说HiveServer2只有第三方的驱动。`There is no ODBC driver available for HiveServer2 as part of Apache Hive. There are third party ODBC drivers available from different vendors, and most of them seem to be free.`
2. Microsoft提供的ODBC驱动实际测试没有通过，猜测原因应该是这个驱动是为azure定制的。
3. `codeproject.com`上面有个c#连接hive的示例，估计是HiveServer1的，我测试没有通过。

然后测试了三个第三方的驱动，结果如下：
1. Hortonworks，失败
2. Cloudera，成功，但是没有提供用户名+密码的验证方式
3. MapR，成功

暂时决定选用MapR.

另外，开发的时候遇到一个问题，提示`在指定的 DSN 中，驱动程序和应用程序之间的体系结构不匹配`，解决办法是把系统32位和64位的数据源都配好。路径分别是`system32\odbcad32.exe`和`SysWOW64\odbcad32.exe`。


