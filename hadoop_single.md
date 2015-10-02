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
