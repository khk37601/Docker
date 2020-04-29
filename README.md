# :whale: Docker?

* :pray: 발표 : 2013년 3월 13일( 솔로몬 하익스(Solomon Hykes) ) 

* :paperclip: 저장소 : github.com/docker/docker-ce

*  리눅스 컨테이너(LXC (Linux containers)) 기술을 이용함.
```
운영체제 수준의 가상화 기술로 리눅스 커널을 공유하면서 프로세스를 격리된 환경에서 실행하는 기술.

* 운영체제 수준의 가상화 : 운영체제의 커널이 하나의 사용자 공간 인스턴스가 아닌, 여러 개의 격리된 사용자 공간 인스턴스를 갖출 수 있도록 하는 서버 가상화 방식.  
```
LXC : https://ko.wikipedia.org/wiki/LXC(위키백과)

#### LXC 특징 

##### 1. ```빠른 속도``` : 하나의 프로세스로 관리 하기때문에 속도가 매유 빠름.
##### 2. ```높은 이식성``` : 모든 컨테이너는 독자적인 실행 환경을 가지고 있다.  


#### 등장배경

기존의 가상화 방법은 VMware, VirtualBox를 이용하여 Host OS위에 여러종류의 OS를 가상화 하는 방식이였습니다.
이런 방법은 간단하지만 무겁고, 느리며 환경설정을 그때그때 해줘야 한다는 단점이 존재 합니다.
이러한 단점을 개선하기 위해서 Docker를 이용하여 프로스세스 단위의 가상화가 등장했습니다. 

#### 용어
 
 * Image : 개발 환경을 구축하기위해 필요한 라이브러리 및 패키지르르 모아 하나의 파일로 만들어 놓은 것.

 * Container : Image가 실행돤 상태, 격리돤 프로세스.
 
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
 
 

