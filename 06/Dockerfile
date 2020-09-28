#
# ДЗ-06
#

# используем готовый образ tomcat8
FROM tomcat:8.0

# обновим список пакетов
RUN apt-get update
# ставим всё что необходимо для сборки, гит мавен и яву
RUN apt-get install default-jdk -y
RUN apt-get install git -y
RUN apt-get install maven -y

