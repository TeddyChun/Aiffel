# Aiffel (대전3기)


apt-get: APT 패키지 관리자를 통해 공인 저장소에서 패키지를 가져다 설치하거나 제거합니다.
$ sudo apt-get update 등록된 공인 저장소에 있는 패키지 목록을 최신 버전으로 가져옵니다.
$ sudo apt-get install htop # CPU 및 메모리 사용량을 시각화하고, 프로세스 별 CPU 사용량을 표시해 주는 프로그램입니다.

삭제는 설치만큼 쉽습니다. apt-get 뒤에 install 대신 remove를 넣어서 프로그램만을 제거하거나, purge를 넣어 해당 프로그램의 설정 파일까지 모두 삭제시킬 수 있습니다. 만약 중간에 확인([Y/n])을 물으면 y를 누르고 엔터를 쳐서 제거를 승인합니다.
$ sudo apt-get remove htop
sudo 명령어: 하나의 메인프레임 컴퓨터에 여러 개의 터미널을 붙여 사용할 수 있게 했던 것처럼, 한 대의 컴퓨터를 여러 사람이 함께 사용하는 것은 운영체제의 초기 역사부터 일반적인 사용법이었습니다. 이 때문에 사용자(user)를 구분하고 권한을 나누는 일이 중요했으며, 그 개념은 한 사람이 한 대의 컴퓨터를 사용하는 개인용 컴퓨터(personal computer, PC) 시대의 운영체제에도 그대로 남았습니다. 
특히 유닉스 계열 운영체제들은 개인용 컴퓨터보다 서버용 또는 기타 산업용으로 쓰이는 경우가 잦기에, 다른 운영체제보다 사용자와 권한의 개념을 훨씬 더 자주 마주치게 됩니다.
유닉스 계열 운영체제에서 모든 권한은 사용자를 기준으로 인증합니다. 운영체제에서 어떤 작업을 실행하기 위해서는 어떤 사용자 이름으로 실행할지 미리 정해져 있어야 한다는 뜻입니다.

ps -ef 명령어를 사용하면 프로세스마다 누구의 권한으로 실행되는지(UID, User ID) 확인할 수 있습니다. 프로세스는 현재 사용자가 가진 범위만큼의 권한을 가집니다. 우리가 위에서 cd /root로 최고 관리자의 디렉토리에 접근하려고 했을 때처럼, 해당 사용자의 권한을 넘어서는 작업을 요청하면 운영체제의 커널이 이를 거부합니다.
보통 우리가 사용하는 사용자 계정은 운영체제를 설치할 때 최초로 생성한 계정입니다. 개인용 컴퓨터에서는 이 사용자가 해당 컴퓨터를 사용할 주된 사람일 것입니다. 하지만 리눅스 기반 운영체제, 윈도우, 맥 OS 모두 공통적으로, 해당 사용자 계정에게 운영체제에 대한 모든 권한이 주어지지는 않습니다. 보안 및 시스템 안정성을 위해 완전한 권한은 운영체제에 기본으로 설정된 최고 관리자(superuser) 계정만이 가지고 있으며, 
윈도우에서는 이 계정을 Administrator이라고 부르고, 유닉스 계열 운영체제에서는 root라는 아이디를 가지고 있습니다.
우리가 직접 생성한 사용자 계정은 일반 사용자 계정입니다. 이 때문에 운영체제 자체에 영향을 주는 일(커널 권한이 필요한 프로그램의 설치나 실행 등)은 최고 관리자 권한을 빌려야 합니다. 윈도우에서 무언가를 설치할 때 가끔 보게 되는 "관리자 권한으로 실행" 경고창이나, 유닉스 계열 운영체제에서 사용하는 sudo(superuser do) 명령어가 바로 이 역할을 하며, 
일반 사용자가 잠시 최고 관리자(또는 다른 사용자) 권한으로 행동할 수 있게 해줍니다. 매번 확인해야 하는 것이 번거로울 수 있지만, 
한 번 더 확인함으로써 실수를 방지할 기회를 준다는 것 외에도 모든 권한이 아닌 일부 권한만 허용할 수 있는 등 다양한 보안상의 이점이 있습니다.
root 계정이 갖고 있는 디렉토리 : /root

사용자 그룹
사용자들이 여러 명 있을 때, 쉽게 묶어서 관리하는 개념이 바로 그룹(group)입니다. 예를 들어 한 사용자가 sudo 명령어를 실행하기 위해서는, 동일한 이름(sudo)라는 이름의 그룹에 속해있어야 합니다.
컴퓨터에 어떤 그룹들이 있고, 해당 그룹마다 어떤 사용자들이 들어있는지 한번 확인해 봅시다. 유닉스 계열 운영체제에서는 설정 파일이나 장치 모두 파일로 접근 가능해야 한다는 철학이 있기 때문에, 
그룹 설정도 텍스트 파일로 저장되어 있습니다.
cat: 하나 이상의 텍스트 파일을 순서대로 출력합니다./`cat` 명령어는 고양이가 아니라 concatenate(이어붙이다)의 약자
$ cat /etc/group
참고: 사용자들의 목록은 /etc/passwd에 기록되어 있는데, 원래 예전에는 해당 파일에서 사용자의 비밀번호까지 기록했기 때문입니다. 
이제 대부분의 리눅스 기반 운영체제에서 비밀번호는 최고 관리자만 접근 가능한 /etc/shadow 파일에 암호화되어 저장됩니다.


접근 권한
그럼 누가 어떤 프로그램을 실행할 수 있는지는 어떻게 구분할까요? 다시 한 번, 프로그램도 파일이기 때문에, 프로그램 실행 권한은 파일 접근 권한과 동일한 방법으로 구분합니다.
프로그램과 디렉토리를 포함한 모든 "파일"에는 소유 사용자와 소유 그룹이 있습니다. 
소유 사용자가 할 수 있는 일, 소유 그룹에 소속된 사용자들이 할 수 있는 일, 그리고 그 밖의 사용자들이 할 수 있는 일을 파일마다 설정할 수 있습니다. 
이 설정값은 ls -lah 명령을 통해서도 확인할 수 있습니다.


root 가 여러번 나오네요 3번 열은 소유 사용자이고, 4번째 열은 소유 그룹입니다. 
위에 두 줄을 보면 현재 디렉토리(/aiffel, 여기서는 .)는 사용자로서 root과 그룹으로서 root이 소유하고 있으며, 그 위의 디렉토리(/, 여기서는 ..)는 사용자와 그룹으로서의 root가 소유하고 있음을 알 수 있습니다. 
한번 이걸 변경해볼까요? 현재 디렉토리의 소유 사용자를 root로, 소유 그룹은 adm으로 변경했다가 복구해 보겠습니다.
chown: 대상 파일의 소유 사용자와 그룹을 변경
$ sudo chown root:adm .
$ ls -lah


tail -n titanic.csv | cut -d -f ||uniq
