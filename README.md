
    1.CentOS 설치
    
    2.Hadoop 설치
    
    3.OpenTSDB 설치



# CentOS Download

http://125.7.128.52:8001/wordpress/pub/inhatc/

http://centos.org/download


# Hadoop Download

    yum -y update
    yum install wget  # wget 설치가 되어있지 않은 경우에 실행
    systemctl stop firewalld  # 방화벽 해제가 필요한 경우에 실행
    
[ yum을 이용하여 Chrome 브라우저 설치 ] # 웹브라우저 설치가 필요한 경우에 실행

        vi /etc/yum.repos.d/google.repo 

        # 다음 내용 추가

        [google64]
        name=google-chrome - 64-bit
        baseurl=http://dl.google.com/linux/rpm/stable/x86_64
        enabled=1
        gpgcheck=1
        gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub
#
        # yum으로 Google Chrome 안정판 설치
        yum install google-chrome-stable

        #다음과 같은 에러가 발생하여 설치가 중단된다.

        # Error: Package: google-chrome-stable-30.0.1599.114-1.x86_64 (google64)
        #       Requires: libstdc++.so.6(GLIBCXX_3.4.15)(64bit)
        #       
        # Richard Lloyd가 만든 설치 스크립트를 이용하여 다시 설치

        wget http://chrome.richardlloyd.org.uk/install_chrome.sh
        chmod u+x install_chrome.sh
        ./install_chrome.sh
# Hadoop 설치하기
        [기존 java 삭제하기] # centos 경우에는 자바 설치가 되어 있지 않으므로 따로 실행할 필요 없음

        yum -y remove "java-*"
#
        
        1. jdk 다운로드
#
        arch명령어를 통해 비트수 확인 후 설치
#
        
        cd ~/Downloads

        (64비트인 경우)
        wget —no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"         http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz

        (32비트인 경우)
        wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-linux-i586.tar.gz"


        cd ~/Downloads/
        tar –zxvf jdk-8u5-linux-x64.tar.gz
        mkdir /usr/java
        mv jdk1.8.0_05 /usr/java/jdk1.8

        vi /etc/profile

        밑에 export 3줄만 추가

        export JAVA_HOME=/usr/java/jdk1.8
        export PATH=$JAVA_HOME/bin:$PATH
        export CLASSPATH=$CLASSPATH:$JAVA_HOME/jre/lib/ext:$JAVA_HOME/lib/tools.jar

        # 실행
        source /etc/profile

#

    2. 계정 추가
    
#
    
        # SSH 설치 및 공개 키 설정 
        #   Hadoop클러스터에서 Master와 Slave들 간에 통신은 SSH를 이용함
        #   모든 컴퓨터에는  SSH가 설치되어 있어야 함
        #   Master에서 암호없이 Slave에 접속하기 위해서 공개 키가 필요함

        useradd hadoop
        su - hadoop
        ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
        cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
        chmod 0600 ~/.ssh/authorized_keys
#
    3. 로컬호스트 들어갔다 나오기
#
        ssh localhost
        exit
        (ctrl + d)
#
    4. 하둡다운로드
#
        cd /home
        mkdir hadoop
        cd hadoop
        wget http://apache.tt.co.kr/hadoop/common/hadoop-2.7.1/hadoop-2.7.1.tar.gz
        tar -zxvf hadoop-2.7.1.tar.gz
#
    5. 컨피규어링
#
    
        $vi $HOME/.bashrc

        # 아래 11개 export 만 추가해주면 됨
        export JAVA_HOME=/usr/java/jdk1.8
        export HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar
        export HADOOP_HOME=/home/hadoop/hadoop-2.7.1
        export HADOOP_INSTALL=$HADOOP_HOME
        export HADOOP_MAPRED_HOME=$HADOOP_HOME
        export HADOOP_COMMON_HOME=$HADOOP_HOME
        export HADOOP_HDFS_HOME=$HADOOP_HOME
        export HADOOP_YARN_HOME=$HADOOP_HOME
        export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
        export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
        export JAVA_LIBRARY_PATH=$HADOOP_HOME/lib/native:$JAVA_LIBRARY_PATH

        # 실행
        $source $HOME/.bashrc



# OpenTSDB Install

## centos update
    
        # root 권한으로 필요시 수행
        yum -y update

## JAVA Setting

        [기존 java 삭제하기] 
        # 기존 시간에 설정한 사람은 다시 할 필요 없음
        # yum -y remove "java-*"
#
        1. jdk 다운로드
#
        cd ~/Downloads

        (64비트인 경우)
        wget —no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz

        (32비트인 경우)
        wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u60-b27/jdk-8u60-linux-i586.tar.gz"


        cd ~/Downloads/
        tar –zxvf jdk-8u5-linux-x64.tar.gz
        mkdir /usr/java
        mv jdk1.8.0_05 /usr/java/jdk1.8

        vim /etc/profile

        밑에 export 3줄만 추가

        export JAVA_HOME=/usr/java/jdk1.8
        export PATH=$JAVA_HOME/bin:$PATH
        export CLASSPATH=$CLASSPATH:$JAVA_HOME/jre/lib/ext:$JAVA_HOME/lib/tools.jar

        # 실행
        source /etc/profile
    
#

##hbase Install(버전이 바뀔수도 있음)

        cd /usr/local
        mkdir data
        cd data
        wget http://www.apache.org/dist/hbase/stable/hbase-1.1.2-bin.tar.gz
        tar xvfz hbase-1.1.2-bin.tar.gz
        cd hbase-1.1.2
        hbase_rootdir=${TMPDIR-'/usr/local/data'}/tsdhbase
        iface=lo'uname | sed -n s/Darwin/0/p'

###hbase-site.xml correction

        vim conf/hbase-site.xml

###configuration Add to between the tags

    <configuration>
            <property>
                <name>hbase.rootdir</name>
                <value>file:///DIRECTORY/hbase</value>
            </property>
        <property>
            <name>hbase.zookp.property.eataDir</name>
            <value>/DRECTORY/zookeeper</value>
        </property>
    </configuration>
