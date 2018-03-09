Tomcat 在第一次启动时很快，但是在第二次及以后启动时都会卡在 **...Deploying web application directory... ** 这里很久，有 2 种解决办法:

1. 全局: 修改 **$JAVA\_HOME/jre/lib/security/java.security**:

   ```
    securerandom.source=file:/dev/urandom
   ```

2. 局部: Tomcat 的启动文件中 JAVA\_OPTS 加上 **-Djava.security.egd=file:/dev/./urandom**

   ```
    JAVA_OPTS="$JAVA_OPTS -Djava.security.egd=file:/dev/./urandom ..."
   ```

原因：

Linux 或者部分 Unix 系统提供随机数设备是 /dev/random 和 /dev/urandom ，urandom 安全性没有 random 高，但 random 需要时间间隔生成随机数，JDK 默认调用 random，所以在启动时就卡住了。

