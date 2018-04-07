---
layout: post
title:  "Enable JSON Logging in Tomcat 8 with Log4j2"
date:   2018-04-06 20:00:00
categories: java8 tomcat8 log4j2 
---

Recently I needed to get Tomcat 8 to output all logs in JSON format. To accomplish this I needed to do the following:

1) Copy the following dependencies into my Tomcat lib directory:

- jackson-core-2.4.3
- jackson-databind-2.4.3
- jackson-annotations-2.4.3
- log4j-core-2.10.0
- log4j-api-2.10.0
- log4j-jul-2.10.0.jar

2) Create the a log4j2.xml file in the tomcat lib directory:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="info">
    <Appenders>
        <Console name="Console" target="SYSTEM_OUT">
            <JSONLayout compact="true" eventEol="true" properties="true"/>
        </Console>
    </Appenders>
    <Loggers>
        <Logger name="*" level="trace">
            <AppenderRef ref="Console"/>
        </Logger>
        <Root level="trace">
            <AppenderRef ref="Console"/>
        </Root>
    </Loggers>
</Configuration>
```

3) Create a setenv.sh script in the tomcat bin directory. I needed to add all of these jars manually to the classpath at startup. Additionally, setting the JUL logging manager to the log4j logging manager is needed.

```bash
CLASSPATH=/usr/local/tomcat/lib/log4j-jul-2.10.0.jar:/usr/local/tomcat/lib/log4j-api-2.10.0.jar:/usr/local/tomcat/lib/log4j-core-2.10.0.jar:/usr/local/tomcat/lib/log4j2-dev.xml:/usr/local/tomcat/lib/log4j2.xml:/usr/local/tomcat/lib/jackson-core-2.4.3.jar:/usr/local/tomcat/lib/jackson-databind-2.4.3.jar:/usr/local/tomcat/lib/jackson-annotations-2.4.3.jar:/usr/local/tomcat/lib/:/usr/local/tomcat/lib/log4j2-dev.xml:/usr/local/tomcat/lib/disruptor-3.3.8.jar
JAVA_OPTS="$JAVA_OPTS -Djava.util.logging.manager=org.apache.logging.log4j.jul.LogManager"
```

This configuration uses log4j JUL bridge to pipe all the JUL to log4j2. From there we use log4j2 to write all output in JSON format. This works even for Tomcat's localhost log which I had trouble getting to work with any other configuration.
