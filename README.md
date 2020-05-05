# :whale: Docker?


<img src="https://github.com/khk37601/Docker/blob/master/docker_image/docker_logo.PNG" height="100">

* :pray: 발표 : 2013년 3월 13일( 솔로몬 하익스(Solomon Hykes) ) 
    
    - [The future of Linux Containers](https://www.youtube.com/watch?v=wW9CAH9nSLs) 
* :paperclip: 저장소 : github.com/docker/docker-ce

* GO언어로 구성 

* Linux Base (오직 리눅에서만 구동)

*  리눅스 컨테이너(LXC (Linux containers)) 기술을 이용함.
```
운영체제 수준의 가상화 기술로 리눅스 커널을 공유하면서 프로세스를 격리된 환경에서 실행하는 기술.

* 운영체제 수준의 가상화 : 운영체제의 커널이 하나의 사용자 공간 인스턴스가 아닌, 여러 개의 격리된 사용자 공간 인스턴스를 갖출 수 있도록 하는 서버 가상화 방식.  
```
[LXC](https://ko.wikipedia.org/wiki/LXC(위키백과)) 
 
 ```namespace```기능을 이용하여 각 컨테이너릐 독립적인 공간을 제공 합니다.
 
 * PID namespace :  프로세스에 할당된 고유한 ID를 통해 프로세스를 격리할 수 있습니다.
 
 * Network namespace : ip주소, port번호 등 namespace마다 프로세스를 격리할 수 있습니다.
 
 리눅스 namespace기능 : https://galid1.tistory.com/442

 ```cgroups(Control groups)```프로세스들이 사용할 수 있는 컴퓨팅 자원들을 제한하고 격리시킬 수 있는 기능.
   
   * 메모리, CPU, 네트워크 ..등 그룹단위로 제어 가능


##### docker는 두개의 기술을 기반으로 container에 자원할당과 독립적인 프로세스 공간을 제공 해줍니다.



#### LXC 특징 

##### 1. ```빠른 속도``` : 하나의 프로세스로 관리 하기때문에 속도가 매유 빠름.
##### 2. ```높은 이식성``` : 모든 컨테이너는 독자적인 실행 환경을 가지고 있다.  



#### 용어
 
 * Image : 개발 환경을 구축하기위해 필요한 라이브러리 및 패키지를 모아 하나의 파일로 만들어 놓은 것.
 (실행파일)

 * Container : Image가 실행돤 상태, 격리돤 프로세스.
(프로세스)

#### 등장배경

기존의 가상화 방법은 VMware, VirtualBox를 이용하여 Host OS위에 여러종류의 OS를 가상화 하는 방식이였습니다.
이런 방법은 간단하지만 무겁고, 느리며 환경설정을 그때그때 해줘야 한다는 단점이 존재 합니다.
이러한 단점을 개선하기 위해서 Docker를 이용하여 프로스세스 단위의 가상화가 등장했습니다. 

![대체텍스트](https://github.com/khk37601/docker/blob/master/docker_image/docker_%EA%B8%B0%EC%A1%B4%EB%B0%A9%EB%B2%95.PNG) 
```
 Hypervisor위에 새로운 os를 설치하는 방법이라서 많은 오버헤드가 발생 하게 됩니다.
 (os, 커널을 통째로 가상화)
 새로운 os를 설치 할때마 설정을 처음부터 해야 한다는 단점이 존재합니다.
```
![대체텍스트](https://github.com/khk37601/docker/blob/master/docker_image/docker_%EC%83%88%EB%A1%9C%EC%9A%B4%20%EB%B0%A9%EB%B2%95.PNG) 
```
docker는 컨테이너 환경에서 실행됨, 하나의 컨테이너는 독립된 프로세스라고 생각하면 됩니다.(filesystem만 가상화 PC의 커널을 공유)
컨테이너의 설정은 Image라는 것으로 저장이 가능 하며, Image를 이용하여 동일한 환경의 컨테이너 구동이 가능해 집니다.
```

#### :arrow_down: 설치
 
*  윈도우(Win10) 
 ```
 $ https://docs.docker.com/docker-for-windows/install/#download-docker-for-windows
 $ Download from Docker Hub > Get Docker click
 $ cmd > docker version 
 ```
 
 * centos6 (참조 : https://jang8584.tistory.com/262)
 ```
 $ yum -y update
 $ curl -O -sSL https://get.docker.com/rpm/1.7.1/centos-6/RPMS/x86_64/docker-engine-1.7.1-1.el6.x86_64.rpm
 $ rpm -Uvh docker-engine-1.7.1-1.el6.x86_64.rpm --nodeps
 $ yum -y install libcgroup
 $ docker -v
 ```
 
 * centos7 
 ```
 $ yum -y update
 $ yum -y install docker docker-registry
 ```
 
 #### 명령어
 진행한 환경은 Window10입니다.
 
 * 이미지목록 확인 
 ```
  $ docker images 
 ```
 ![](https://github.com/khk37601/Docker/blob/master/docker_image/docker_images.PNG)
  각 이지미에는 고유한 ID가 부여됩니다.
 
 
 * 이미지 찾기 
 ```
 $ docker search <name> 
 ex) docker search mysql or centos or nginx ...
 
 ```
 ![](https://github.com/khk37601/Docker/blob/master/docker_image/docker_search.PNG)
 DockerHub: https://hub.docker.com/ 에서도 image를 찾아서 다운받을 수 있습니다.
 
 * 이미지 다운로드
 ```
 $ docker pull nginx
 ```
 ![](https://github.com/khk37601/Docker/blob/master/docker_image/docker_nginx_pull.PNG)
 
 * nginx 실행
 
 ```
 # 현재 실행 중인 프로세스 목록
 $ docker ps
 # 백그라운드에서 ngnix 실행
 $ docker run -d  -p 8383:81 nginx
 ```
 ![](https://github.com/khk37601/Docker/blob/master/docker_image/docker_imges_run.PNG)
 image를 실행한 상태인 컨테이너 입니다. 현재상태와 포트번호 등 정보를 살펴 볼 수 있습니다.
 
 ![](https://github.com/khk37601/Docker/blob/master/docker_image/nginx_%EC%8B%A4%ED%96%89.PNG)
 

 
 * nginx 여러개의 컨테이너
 
 ![](https://github.com/khk37601/Docker/blob/master/docker_image/docker_%EC%97%AC%EB%9F%AC_%EC%BB%A8%EB%8D%B0%EC%9D%B4%EB%84%88.PNG)
 각의 nginx는 프로세스로 독립된 공간에서 실행중입니다.
 
 * 실행중인 컨테이너 접근
 ```
 $ docker attach <container-name>quirky_napier
 ```
 
 
