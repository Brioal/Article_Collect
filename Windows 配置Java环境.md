# Java环境配置代码
## 如何配置环境等就不在叙述，只记录环境代码
```

1.
  JAVA_HOME
  jdk路径（不包含bin），例如：C:\Program Files\Java\jdk1.8.0_111

2.
  PATH（一般情况下已经存在）
  %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
  （添加到开始）

3.
  CLASSPATH
  .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
```

## 测试是否成功
#### cmd内分别输入`java` , `javac` ，如果输出help信息则环境变量配置正确

#### 完毕
