# 서비스와 소켓

- 서비스(service)는 평상시에도 늘 가동하는 서버 프로세스며, 소켓(Socket)은 필요할 때만 작동하는 서버 프로세스다. 서비스와 소켓은(systemd)라는 서비스 매니저 프로그램으로 작동시키거나 관리한다.

> 이전에는 최상의 프로세스인 init 프로세스가 서비스를 직접 관리하는 방식이었으나, 요즘에는 systemd가 서비스 대부분을 관리한다. systemd와 관련된 세부 내용은 https://docs.fedoraproject.org/en-US/quick-docs/understanding-and-administering-systemd/ 주소를 참조하자

## 서비스

서비스의 특징을 살펴보자.

- 시스템과 독자적으로 구동 및 제공되는 프로세스를 말한다. 웹 서버(httpd), DB 서버(mysqld), FTP 서버(vsftpd) 등을 예로 들 수 있다.

- 실행 및 종료는 대개 <b>systemctl start/stop/restart 서비스이름</b> 명령으로 사용된다. 예를 들어 웹 서버는 <b>systemctl start httpd</b> 명령으로 구동한다.

- 서비스의 실행 스크립트 파일은 /usr/lib/systemd/system/ 디렉터리에 '서비스이름.service'라는 이름으로 확인할 수 있다. 예를 들어 Cron 서비스는 crond.service라는 이름의 파일로 존재한다.


* * * 
# 응급 복구

* * * 
## GRUB 부트로더

