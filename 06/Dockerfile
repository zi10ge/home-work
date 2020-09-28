#
# ДЗ-06
#

# используем готовый образ tomcat8
FROM tomcat:8.0

#собирать будем в этой директории
ENV a_HOME /home/06e
RUN mkdir -p "$a_HOME"
WORKDIR $a_HOME

# обновим список пакетов
# ставим всё что необходимо для сборки, гит мавен и яву
# тянем приложение java собираем его и копируем WAR на место (автодеплой томкатом)
# делаем всё в одном слое, что бы потом подчистить и удалить лишнее
#
# jdk+git+maven??? 366 VS 666, как уменьшить размер полученного образа?
#test                latest              cad424ee8173        18 seconds ago      666MB
#tomcat              8.0                 ef6a7c98d192        2 years ago         356MB
#попробовать всё в одном слое делать, после сборки вычищать?
#итог
#test                latest              01e8da113a1c        4 minutes ago       453MB
# где то ещё ~100мб потерялось :)

RUN apt-get update && apt-get install -y \
    default-jdk \
    git \
    maven \
    && git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git \
    && cd "$a_HOME/boxfuse-sample-java-war-hello" \
    && mvn package \
    && cp /home/06e/boxfuse-sample-java-war-hello/target/hello-1.0.war /usr/local/tomcat/webapps \
    && rm -Rf $a_HOME \
    && apt-get remove -y \
    default-jdk \
    git \
    maven \
    && apt-get autoremove --purge -y \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean
# порт
EXPOSE 8080

#запускаем скрипт по ману томката
CMD ["catalina.sh", "run"]

# HOW TO RUN
# docker build -t test .
# docker run -d -it -p 80:8080 test