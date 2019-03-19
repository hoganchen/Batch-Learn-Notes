### Jenkins批处理运行

```
set JENKINS_HOME=D:\Jenkins

ping -n 60 127.0.0.1 > nul

cd /d %JENKINS_HOME%

REM java -jar jenkins.war
java -jar agent.jar -jnlpUrl http://xxx.xxx.xxx.xxx:8080/computer/Slave-xxx.xxx.xxx.xxx/slave-agent.jnlp -secret xxxxxx -workDir "D:\Jenkins"

pause

```



