# Mifos X 18.03.01 - Docker

Build the images 
(Run in their corresponding directory)

1. Build the MIFOS X image

```bash
$ docker build -t com.mx.ecoglobalconsulting.tomcat.mifosx.18.03.01 .
```

2. Build the MySQL image 

```bash
$ docker build -t com.mx.ecoglobalconsulting.mysql.mifosx.18.03.01 .
```

3. Build the SMS Server image

```bash
$ docker build -t com.mx.ecoglobalconsulting.activemq.mifosx.18.03.01 .
```
4. Build the Web Server Nginx image

## Ensure you have 

   ```npm``` installed - goto http://nodejs.org/download/ to download installer for your OS.    
   ```ruby``` installed - goto https://www.ruby-lang.org/en/documentation/installation/ to download latest version of ruby.

<br/> Note: On Ubuntu Linux you can use 'sudo apt-get install npm nodejs-legacy' (nodejs-legacy is required to avoid the ""/usr/bin/env: node: No such file or directory" problem).
<br/> Tip: If you are using Ubuntu/Linux, then doing ```npm config set prefix ~``` prevents you from having to run npm as root.

```bash
$ docker build -t com.mx.ecoglobalconsulting.nginx.mifosx.18.03.01 .
```

5. Run the Docker images using Compose

```bash
$ docker-compose -f mifos-stack-DEV.yml up
```

6. Verify the running containers

```bash
$ docker ps | grep mifosx.18.03.01
588027cda597        ecoglobalconsulting/com.mx.fintecheando.mifosx.18.03.01            "/bin/sh -c /entrypo…"   41 minutes ago      Up 41 minutes       8080/tcp, 0.0.0.0:8443->8443/tcp                           ecoglobalconsultingmifosdockerubuntu_mifosx_1
0a4c69071ae0        ecoglobalconsulting/com.mx.fintecheando.mariadb.mifosx.18.03.01    "docker-entrypoint.s…"   41 minutes ago      Up 41 minutes       3306/tcp                                                   ecoglobalconsultingmifosdockerubuntu_db-server_1
3a4f14d027d2        ecoglobalconsulting/com.mx.fintecheando.activemq.mifosx.18.03.01   "/app/run.sh"            41 minutes ago      Up 41 minutes       1883/tcp, 5672/tcp, 8161/tcp, 61613-61614/tcp, 61616/tcp   ecoglobalconsultingmifosdockerubuntu_sms-server_1
```

7. Login to Mifos using the Web UI with these credentials:

username: fincore
password: password

https://localhost:8443/community-app/#/ (secure web access, but this is a self signed certificate and you will have a warning in your web explorer, just ignore it and continue)


8. As note if you have any issue with the volumes and entry points remove the volumes (be careful, with this we are removing all of them, because it is running in our local DEV, don't do this in Production)
```bash
$ docker stop $(docker ps -a -q)
$ docker rm $(docker ps -a -q)
$ docker volume rm $(docker volume ls -q)
```

Reference 

* http://mifos.org/take-action/get-mifos/#download
* https://mifosforge.jira.com/wiki/spaces/MDZ/pages/92504091/Prerequisite
* https://mifosforge.jira.com/wiki/spaces/docs/pages/74711072/Mifos+X+Installation+on+Linux+-+Ubuntu+Server 
* https://github.com/dmitryint/docker-mifosx
* https://github.com/docker-library/docs/tree/master/mariadb
* https://docs.docker.com/docker-cloud/builds/push-images/
* https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12340624&styleName=&projectId=12319420&Create=Create&atl_token=A5KQ-2QAV-T4JA-FDED%7C7616978f36b22cf7dc20a899a3cbf9f614960808%7Clin
* https://medium.com/viithiisys/mifos-x-installation-on-linux-ubuntu-server-3843e028ab90

Issues with the reports
* https://stackoverflow.com/questions/37066024/what-is-the-mariadb-dialect-class-name-for-hibernate
* http://sterl.org/2015/09/spring-boot-mariadb/
* http://in.relation.to/2017/02/16/mariadb-dialects/
