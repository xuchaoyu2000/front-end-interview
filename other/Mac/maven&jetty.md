# Maven
下载好后配置环境
打开终端，输入:vi ~/.bash_profile
写入： export MAVEN_HOME=/Users/localadmin/tools/apache-maven-3.6.0
      export PATH=$MAVEN_HOME/bin:$PATH
退出保存.(/Users/localadmin/tools是maven文件夹路径)
输入：source ~/.bash_profile 让配置生效。
最后输入：mvn -v 查看是否成功。

# Jetty
下载好后配置环境
打开终端，输入：vi ~/.bash_profile
写入：  export JETTY_HOME=/Users/localadmin/tools/jetty-distribution-9.4.13
       export PATH=$PATH:$JETTY_HOME
退出保存.(/Users/localadmin/tools是jetty文件夹路径)
输入：source ~/.bash_profile 让配置生效。
输入：java -jar $JETTY_HOME/start.jar --add-to-startd=http,deploy
cp $JETTY_HOME/demo-base/webapps/async-rest.war webapps/ROOT.war
java -jar $JETTY_HOME/start.jar
然后打开浏览器输入localhost:8080即可验证是否成功。
以后打开只需在终端中输入：java -jar $JETTY_HOME/start.jar