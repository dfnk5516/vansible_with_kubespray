# Vansible with Kubespray

## How to Use

```sh
$ vagrant plugin install vagrant-env vagrant-vbguest
$ vagrant up
$ vagrant ssh $(vagrant status | tail -5 | sed -n '1p' | awk '{ print $1}')
$ ansible all -m ping -k
SSH password: vagrant
```

## vagrant

박스 관련 명령어

```sh
// 조회
$ vagrant box list

// 추가
$ vagrant box add bento/ubuntu-18.04

// 이름 지정 추가
$ vagrant box add centos_private  https://github.com/tommy-muehle/puppet-vagrant-boxes/releases/download/1.0.0/centos-6.6-x86_64.box

// 삭제
$ vagrant box remove [name]
```

가상머신 관련 명령어

```sh
// 조회
$ vagrant status [name|id]
$ vagrant global-status

// 실행 (실행 시 박스가 없으면 자동으로 다운로드 받는다)
$ vagrant up

// 접속
$ vagrant ssh [name|id] [--extra_ssh_args]

// 종료
$ vagrant halt [name|id]
$ vagrant halting [name|id]

// 세팅 적용 (ex: 네트워크 설정)
$ vagrant reload [name|id]

// 프로비저닝 적용
$ vagrant provision [vm-name]

// 삭제
$ vagrant destroy
$ vagrant destory --force
$ vagrant destory --parallel

// 현재 실행 상태 저장,종료(디스크와 램을 사용하고 있는 상태로 종료)
$ vagrant suspend [name|id]

// suspend 해제 (vagrant up 역시 가능)
$ vagrant resume [name|id]

// ssh-config 조회(network forwarded port 설정되있어야함)
$ vagrant ssh-config

// 스냅샷 조회
$ vagrant snapshot list

// 스냅샷 저장
$ vagrant snapshot save [vm-name] [name]

// 스냅샷 복원
$ vagrant snapshot restore [vm-name] [name]

// 스냅샷 삭제
$ vagrant snapshot delete [vm-name] [name]
```

Share

```sh
// Vagrantfile 공유
$ vagrant login vagrant share
```

Providers

```sh
// default provider 변경
$ vagrant up –provider=vmware_fusion vagrant up –provider=aws
```

Networking

```Vagrantfile
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise32"
  config.vm.provision :shell, path: "bootstrap.sh"
  # 호스트의 4567 를 게스트 80으로 연결
  # 브라우져에서 127.0.0.1:4567 연결하면
  # 호스트의 apache 80번 포트로 연결된다.
  config.vm.network :forwarded_port, host: 4567, guest: 80
end
```

Etc

```sh
// 최신 업데이트 된 박스들 조회
$ vagrant box outdated

// 박스 삭제(address)
$ vagrant remove <address>

// 현재 실행중인 virtualbox 를 재사용 가능한 box로 만든다
$ vagrant package

$ vagrant update
$ vagrant repackage

// vagrant plugin
$ vagrant plugin install
$ vagrant plugin license
$ vagrant plugin list
$ vagrant plugin uninstall
$ vagrant plugin update
```

### 참고한 곳

[노력 이기는 재능 없고 노력 외면하는 결과도 없다, asdf](https://m.blog.naver.com/PostView.nhn?blogId=sory1008&logNo=220759961657&proxyReferer=https:%2F%2Fwww.google.com%2F)  
[YOUNG.K](https://rangken.github.io/blog/2015/vagrant-1/)  
[다양한 환경을 앤서블(Ansible)로 관리하기 with 베이그런트(Vagrant)](https://www.inflearn.com/course/ansible-%EC%9D%91%EC%9A%A9/dashboard)  
[kairen/kubeadm-ansible](https://github.com/kairen/kubeadm-ansible)  
[Ruby 처음 배우기:데이터타입](https://smartbase.tistory.com/47)  
[Joinc](https://www.joinc.co.kr/w/Site/Ruby/File)  
[Python2.net](https://www.python2.net/questions-962144.htm)
