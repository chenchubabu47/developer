# developer
- hosts: tomcat
  become: yes
  remote_user: ec2-user
  tasks:
    - name: going to update yum package
      yum:
        name: "*"
        state: present

    - name: install java 8
      yum:
        name: java-1.8.0-openjdk
        state: present
    
    - name: download tomcat
      get_url:
        url: https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.53/bin/apache-tomcat-9.0.53.tar.gz
        dest: /usr/local
        mode: '0777'

    - name: Unzip the binaries
      unarchive:
        src: /usr/local/apache-tomcat-9.0.53.tar.gz
        dest: /usr/local
        remote_src: yes
        mode: '0777'
