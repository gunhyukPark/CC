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
