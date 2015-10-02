#### Cent OS 설치

su

yum install git

#### git 사용법

mkdir ~/workspace

cd ~/workspace

git status

git init

git status

git config --global user.name [유저이름]

git config --global user.email [이메일주소]

git remote add origin https://github.com/kowonsik/raspberry.git

git pull -u origin master     # 파일 다운로드

git add [생성한파일]

git status

git commit -m "메세지"

git status

git push -u origin master     # 파일 업데이트
