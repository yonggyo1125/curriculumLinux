# gitlab 설치하기

- gitlbal ce 공식 설치 스크립트 : https://about.gitlab.com/install/#centos-8?version=ce

## 종속성 설치

```
# dnf install -y curl policycoreutils openssh-server openssh-clients
```

![image1](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/19~20%EC%9D%BC%EC%B0%A8(6h)%20-%20GitLab%20%EC%84%9C%EB%B2%84/images/image1.png)



```
# firewall-cmd --permanent -add-service=http
# firewall-cmd --permanent --add-service=https
# firewall-cmd --reload
```

- http, https 방화벽을 열어줍니다.

![image2](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/19~20%EC%9D%BC%EC%B0%A8(6h)%20-%20GitLab%20%EC%84%9C%EB%B2%84/images/image2.png)

```
# dnf -y install postfix
# systemctl enable postfix
# systemctl start postfix
```

- postfix를 설치하여 이메일 서비스를 사용할 수 있도록 합니다.

## gitlab-ce 패키지 설치

- curl을 이용하여 gitlab을 등록합니다.

```
# curl -sS https://packages.gitlab.gitlbal.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | bash
```

![image3](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/19~20%EC%9D%BC%EC%B0%A8(6h)%20-%20GitLab%20%EC%84%9C%EB%B2%84/images/image3.png)

- 등록이 되었으므로 이제 dnf를 이용해서 설치가 가능합니다.

```
# EXTERNAL_URL="접속할 도메인 혹은 IP" dnf install -y gitlab-ce 
```

- 접속할 도메인을 EXTERNAL_URL 변수에 저장하고 설치를 진행합니다. 도메인이 없다면 IP를 넣어주셔도 됩니다. 

```
# EXTERNAL_URL="10.0.2.100" dnf install -y gitlab-ce
```

![image4](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/19~20%EC%9D%BC%EC%B0%A8(6h)%20-%20GitLab%20%EC%84%9C%EB%B2%84/images/image4.png)

- 설치가 완료되면 첫 화면에서 root 비밀번호를 설정해야 합니다.

```
# gitlab-ctl reconfigure
```

## 비밀번호 설정 및 로그인
- [현재활동] -> [파이어폭스]를 열고 10.0.2.100을 입력합니다.

![image5](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/19~20%EC%9D%BC%EC%B0%A8(6h)%20-%20GitLab%20%EC%84%9C%EB%B2%84/images/image5.png)

- 깃랩 초기 화면 화면에서 root 패스워드를 설정합니다. 8자리 이상에 특수문자를 포함해야 합니다. 설정이 완료되면 root 계정으로 로그인합니다.

![image6](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/19~20%EC%9D%BC%EC%B0%A8(6h)%20-%20GitLab%20%EC%84%9C%EB%B2%84/images/image6.png)

- 로그인을 하게 되면 깃랩의 첫 화면이 나오게 됩니다.

![image7](https://raw.githubusercontent.com/yonggyo1125/curriculumLinux/master/Linux2/19~20%EC%9D%BC%EC%B0%A8(6h)%20-%20GitLab%20%EC%84%9C%EB%B2%84/images/image7.png)
