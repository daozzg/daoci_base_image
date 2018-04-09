FROM daocloud.io/ubuntu:16.04

# install python3.6 
RUN apt-get update && apt-get install -y software-properties-common vim && \
 add-apt-repository ppa:jonathonf/python-3.6 && \
 apt-get update && apt-get -y install build-essential python3.6 python3.6-dev python3-pip python3.6-venv libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev && \
 python3.6 -m pip install pip --upgrade 

# install mysql 5.6 
ARG PACKAGE_URL=https://repo.mysql.com/yum/mysql-5.6-community/docker/x86_64/mysql-community-server-minimal-5.6.39-2.el7.x86_64.rpm
ARG PACKAGE_URL_SHELL=""

# Install server
RUN rpmkeys --import https://repo.mysql.com/RPM-GPG-KEY-mysql \
  && yum install -y $PACKAGE_URL $PACKAGE_URL_SHELL libpwquality \
  && yum clean all \
  && mkdir /docker-entrypoint-initdb.d

VOLUME /var/lib/mysql


#config mysql
RUN sed -i 's/^\(bind-address\s.*\)/# \1/' /etc/mysql/my.cnf && \
  sed -i 's/^\(log_error\s.*\)/# \1/' /etc/mysql/my.cnf && \
  mkdir -p /var/run/mysqld && chown -R mysql:mysql /var/lib/mysql /var/run/mysqld && \
  echo "mysqld_safe &" > /tmp/config && \
  echo "mysqladmin --silent --wait=30 ping || exit 1" >> /tmp/config && \
#  echo "mysql -e 'GRANT ALL PRIVILEGES ON *.* TO \"root\"@\"%\" WITH GRANT OPTION;'" >> /tmp/config && \
  bash /tmp/config && \
  rm -f /tmp/config

WORKDIR /usr/src/app



