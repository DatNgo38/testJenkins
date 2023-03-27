Update JENKINS messages and add a json file



docker exec -it ea009d1aa030e0c395bb4846f425ce5d46a0b1510711572f7e1ea43d0c629ec0 /bin/bash
jenkins-plugin-cli --plugin-file /your/path/to/plugins.txt --plugins delivery-pipeline-plugin:1.3.2 deployit-plugin

version: '3.8'
services:
  jenkins:
    container_name: jenkins
    image: jenkins/jenkins:lts
    ports:
      - "8080:8080"
      - "50000:50000"
    volumes:
      - jenkins_home:/var/jenkins_home
    networks:
      - jenkins_network
  ngrok:
    container_name: ngrok
    image: wernight/ngrok
    environment:
      - NGROK_AUTHTOKEN=2Na9Y28cQd1kiL35x4fZO3rXmS8_7NobbAVfCo4M189n9CnNs
      - NGROK_PROTOCOL=http
      - NGROK_PORT=8080
    ports:
      - "4040:4040"
    networks:
      - jenkins_network
volumes:
  jenkins_home:
networks:
  jenkins_network: