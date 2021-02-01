**Monitoring of Spring Boot application logs using ELK stack .

First  run an spring Boot application .

**#mvn clean install .

it will run an application and create "app.log" file.

**#java -jar springbootapp-0.0.1-SNAPSHOT.jar

::for check is application running or not::
2021-02-01 18:19:44.064  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:45.067  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:46.067  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:47.068  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:48.068  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:49.070  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:50.071  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:51.072  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:52.072  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:53.073  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:54.073  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01
2021-02-01 18:19:55.074  INFO 18944 --- [           main] org.eduami.sbapp.Application             : App log Current tile is 2021-02-01

**creating another "app.log" file for using as reference for logstash


 **#java -jar springbootapp-0.0.1-SNAPSHOT.jar > /var/log/elasticsearch/app.log
 
 **installation of elasticsearch, logstash, kibana , filebeat.
  
   #sudo apt install elasticsearch
   
   #sudo apt install kibana
   
   #sudo apt install logstash
   
   #sudo apt install filebeat
   
   #systemctl start elasticsearch kibana logstash filebeat
   
   #systemctl status elasticsearch kibana logstash filebeat
   
   **Next We have to configure elaticsearch , logstash, kibana
   
   **nano /etc/elasticsearch/elasticsearch.yml ::"we have to uncomment following things"
   
        cluster.name: my-application
        
        node.name: node-1
   **nano /etc/kibana/kibana.yml ::"we have to uncomment following things"
   
     server.port: 5601
     server.host: "localhost"     
     elasticsearch.hosts: ["http://localhost:9200"
 
   **nano /etc/kibana/kibana.yml ::"we have to uncomment following things"
   
    path.logs: /var/log/logstash
    pipeline.ordered: auto
    path.data: /var/lib/logstash
    
    
   **Next we Have to create a file called logstash.conf -:file is available above
    In this file we will create pipeline for collecting logs from input and send it to the elasticsearch on "localhost:9200"
    To Run This file:-
                     #/usr/share/logstash/bin/logstash -f /etc/logstash/logstash.conf
                     
[INFO ] 2021-02-01 18:42:42.177 [Api Webserver] agent - Successfully started Logstash API endpoint {:port=>9600}
                     
   
   **Inside Kibana:-
                      on browser "localhost:5601" for kibana
                      
                      Management -> stack Management -> kibana -> Index Pattern 
                      
                      you will find privious index pattern here
                      
   **To create new index Pattern
      click on "create index pattern -> 
      
      Step 1 of 2: Define an index pattern
      
      Index pattern name :- "search for spring_boot_demo"
  
  **Then you will find all your data inside  kibana -> Discover
  
  **To make visualization click on visualization 
  :- i uploaded all screen shots of visualization above
