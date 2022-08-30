FROM postgres:14
ENV LANG ja_JP.utf8
COPY ./pg_hba.conf /var/lib/postgresql/data/pg_hba.conf
RUN chown -R postgres:postgres /var/lib/postgresql/data/
RUN apt update
RUN apt-get install -y sysv-rc-conf
RUN apt-get install -y procps
RUN apt-get install -y vim
