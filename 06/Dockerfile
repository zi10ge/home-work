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
RUN apt-get update
# ставим всё что необходимо для сборки, гит мавен и яву
RUN apt-get install default-jdk -y
RUN apt-get install git -y
RUN apt-get install maven -y

# тянем приложение java собираем его и копируем WAR на место (автодеплой томкатом)
RUN git clone https://github.com/boxfuse/boxfuse-sample-java-war-hello.git;
RUN cd "$a_HOME/boxfuse-sample-java-war-hello"; mvn package;
RUN cp /home/06e/boxfuse-sample-java-war-hello/target/hello-1.0.war /usr/local/tomcat/webapps

# jdk+git+maven??? 366 | 666
#test                latest              cad424ee8173        18 seconds ago      666MB
#tomcat              8.0                 ef6a7c98d192        2 years ago         356MB

# порт
EXPOSE 8080

#запускаем скрипт по ману томката
CMD ["catalina.sh", "run"]

