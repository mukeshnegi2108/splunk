FROM ubuntu:16.04

RUN apt-get update

RUN apt-get install wget -y

RUN wget -O splunk-8.0.2-a7f645ddaf91-Linux-x86_64.tgz 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=linux&version=8.0.2&product=splunk&filename=splunk-8.0.2-a7f645ddaf91-Linux-x86_64.tgz&wget=true'

RUN tar xvzf splunk-8.0.2-a7f645ddaf91-Linux-x86_64.tgz -C /opt

COPY conf/*.conf /opt/splunk/etc/system/local/

RUN echo "OPTIMISTIC_ABOUT_FILE_LOCKING = 1" >> /opt/splunk//etc/splunk-launch.conf

COPY conf/startup.sh /opt/splunk/

RUN chmod 777 /opt/splunk/startup.sh

RUN apt-get install -y tzdata vim-tiny iputils-ping net-tools

ENV TZ 'Asia/Kolkata'

RUN echo $TZ > /etc/timezone && \
    rm /etc/localtime && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    apt-get clean

EXPOSE 8000 8089 9997 997

#CMD ["tail","-f","/dev/null"]
#CMD ["/opt/splunk/bin/splunk", "start", "--accept-license", "--no-prompt"]
CMD ["bin/bash","/opt/splunk/startup.sh"]