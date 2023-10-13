[root@vm-linux-x86 ~]# ps -ef|grep java

root      4834     1  2 Jun10 pts/6    03:10:50 /opt/JDK/jdk1.6.0_21/bin/java -classpath /opt/JReport/Server_B201106081302/derby/lib/*:/opt/JReport/Server_B201106081302/lib/JREngine.jar:/opt/JReport/Server_B201106081302/lib/JRESServlets.jar:/opt/JReport/Server_B201106081302/lib/JRStructuredEngine.jar:/opt/JReport/Server_B201106081302/lib/JRStructuredClient.jar:/opt/JReport/Server_B201106081302/lib/JREntServer.jar:/opt/JReport/Server_B201106081302/lib/JRWebDesign.jar:/opt/JReport/Server_B201106081302/lib/*:/opt/JDK/jdk1.6.0_21/lib/tools.jar:/opt/JReport/MyReports/Data/DBdrivers/classes12.jar:/opt/JReport/MyReports/Data/DBdrivers/dbdrivers2.zip:/opt/JReport/MyReports/Data/DBdrivers/dbdrivers3.zip: -Dinstall.root=/opt/JReport/Server_B201106081302/ -Djava.net.preferIPv4Stack=true -Djreport.url.encoding=UTF-8 -Xmx1600m -XX:PermSize=64m -XX:MaxPermSize=128m -Dreporthome=/opt/JReport/Server_B201106081302 jet.server.JREntServer

root      5857  5804  0 10:11 pts/7    00:00:00 grep java

[root@vm-linux-x86 ~]# kill -9 4834



通过 ps -ef | grep java  得到如上线程将某线程终止时用 

kill -9 XXXXX     XXXXX为上述查出的序号  如： 19979线程终止为： kill -9 4834 



kill一个线程时需注意不要误停止了不应该停止的线程造成不必要的麻烦。 

在相当确信时才可用此方法停止线程。