FROM ubuntu:16.04

RUN apt-get update -y && apt-get install wget -y

RUN wget -O splunkforwarder-8.0.2-a7f645ddaf91-Linux-x86_64.tgz 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=linux&version=8.0.2&product=universalforwarder&filename=splunkforwarder-8.0.2-a7f645ddaf91-Linux-x86_64.tgz&wget=true'

RUN tar xvzf splunkforwarder-8.0.2-a7f645ddaf91-Linux-x86_64.tgz -C /opt

COPY conf/*.conf /opt/splunkforwarder/etc/system/local/

COPY conf/startup.sh /opt/splunkforwarder/

RUN chmod 777 /opt/splunkforwarder/startup.sh

RUN apt-get install -y tzdata vim-tiny iputils-ping net-tools

ENV TZ 'Asia/Kolkata'

EXPOSE 9997 8089 997

#CMD ["tail","-f","/dev/null"]
CMD ["bin/bash","/opt/splunkforwarder/startup.sh"]