1) 리눅스 명령어 : top, ps, jobs, kill 명령어 조사하기

(1) 개요
프로세스를 관리하기 위해서는 먼저 프로세스가 무엇인지 정확히 이해 해야 한다. 먼저 컴퓨터는 사람에 의해 명령을 받게 되면 내부 장치인 중앙처리장치(CPU)에 의해 작업처리가 진행된다. 그렇다면 현재 사용자가 내린 명령은 CPU가 처리하고 있는 중으로 이 상태를 프로세스라고 한다. 그러므로 프로세스는 사용자가 컴퓨터를 활용하기 위해 몇 가지의 응용프로그램을 사용하든 CPU는 사용자가 내린 각각의 명령을 처리하게 되므로 이때 생성되는 프로세스는 사용자가 내린 각각의 명령으로 응용프로그램의 개수만큼 생성되게 된다. 
이렇듯 사용자라 입력한 명령은 프로세스가 되어 실행되고 관리된다. 프로세스는 현재 실행 중인 프로그램을 의미하는 것으로, 시스템에서는 사용자가 실행한 프로세스 외에도 사용자 관리, 메모리 관리, 네트워크 접속 관리 등 다양한 기능을 수행하는 많은 프로세스가 실행되고 있다. 일상적으로 사용하는 대부분의 명령은 실행 시간이 짧아 실행된 두 바로 종료되기 때문에 짧은 시간 동안만 프로세스 상태를 유지하게 된다.
과제의 주제처럼 ‘리눅스 명령어 top, ps, jobs, kill 명령어의 활용에 관한 조사를 통해 프로세스의 개념, 프로세스 목록 확인, 특정 프로세스의 정보를 검색, 불필요한 프로세스 종료, 프로세스의 상황 파악을 위한 관리 도구, 셀에서 제공하는 포그라운드와 백그라운드를 통한 작업 제어에 대해 알아보겠다.

① top 명령
top 명령은 프로세스 관리 명령 중 하나로 현재 실행 중인 프로세스의 정보를 주기적으로 출력하는데, 프로세스의 자세한 요약 정보를 상단에 출력하고 각 프로세스의 정보를 하단에 출력해 준다. top 명령이 출력하는 프로세스의 세부 정보는 아래의 <표1-1>와 같다. 여기서 프로세스는 현재 시스템에서 실행 중인 프로그램을 뜻하며, 리눅스는 기본적으로 다중 프로세스 시스템이므로 여러 개의 프로세스가 동시에 실행된다. 또한 리눅스의 운영에 필요한 다양한 기능을 수행하는 시스템 프로세스도 있고, 사용자가 실행한 프로그램인 사용자 프로세스도 존재한다.

<표1-1> top 명령에 의한 세부 정보

항목
의미
PID
프로세스 ID
USER
사용자 계정
PR
우선순위
NI
Nice 값
VIRT
프로세스가 사용하는 가상 메모리의 크기
RES
프로세스가 사용하는 메모리의 크기
SHR
프로세스가 사용하는 공유 메모리의 크기
%CPU
퍼센트로 표시한 CPU 사용량
%MEM
퍼센트로 표시한 메모리 사용량 
TIME+
CPU 누적 이용 시간
COMMAND
명령 이름

항목
의미
PID
프로세스 ID
USER
사용자 계정
PR
우선순위
NI
Nice 값
VIRT
프로세스가 사용하는 가상 메모리의 크기
RES
프로세스가 사용하는 메모리의 크기
SHR
프로세스가 사용하는 공유 메모리의 크기
%CPU
퍼센트로 표시한 CPU 사용량
%MEM
퍼센트로 표시한 메모리 사용량 
TIME+
CPU 누적 이용 시간
COMMAND
명령 이름


리눅스에서  top 명령이 실화면을 살펴보면 아래 <그림1-1>과 같다.


<그림1-1> top 명령의 실행 화면

top 명령은 종료하지 않고 실시간으로 프로세스의 상태를 보여주며 내부적으로 사용하는 명령도 있다. top 명령의 내부 명령으로는 아래 <표1-2>와 같다.

<표1-2> top 명령의 내부 명령

내부명령
기능
‘Enter’, ‘Space Bar’
화면을 즉시 다시 출력한다.
h,?
도움말 화면을 출력한다.
k
프로세스를 종료한다. 종료할 프로세스의 PID를 물어본다.
n
출력하는 프로세스의 개수를 바꾼다.
p
CPU 사용량에 따라 정렬하여 출력한다.
q
top 명령을 종료한다.
M
사용하는 메모리의 크기에 따라 정렬하여 출력한다.
u
사용자에 따라 정렬하여 출력한다.


프로세스 관리 명령 중 ps 명령은 현재 프로세스의 목록만을 확인할 수 있지만 top 명령을 사용하면 사용자가 보기 편하게 다양한 기능을 제공할 수 있으며, 프로세스의 자세한 정보를 통해 ‘시스템 감시’를 할 수 있으므로 시스템 관리자의 입자에서 실행 중인 프로세스를 확인할 때 유용하다.

② ps 명령
프로세스 관리와 관련된 명령에는 현재 실행 중인 프로세스의 목록을 알아보는 명령, 특정 프로세스가 실행 중인지 확인하는 명령, 프로세스를 강제로 종료하는 명령 등이 있다. 그 중 ps 명령은 프로세스의 목록을 확인할 수 있도록 해주는 명령이다.
ps 령은 현재 실행 중인 프로세스의 목록을 보는 명이며, ps 명령이 출력하는 PID를 통해 프로세스의 부모-자식 관계도 확인할 수 있다. 
리눅스 계열 중 우분투 리눅스에서의 ps 명령은 <유닉스, BSD, GNU> 세 가지 유형의 옵션을 모두 지원한다.

첫째, 유닉스
     - 유닉스(SVR4) 옵션 : 묶어서 사용할 수 있고 붙임표로 시작한다(예: -ef).
둘째, BSD
     - BSD 옵션 : 묶어서 사요할 수 있고 붙임표로 시작하지 않는다(예: aux).
셋째, GNU
     - GNU 옵션 : 붙임표 두 개로 시작한다(예: --pid).

위의 세 가지 옵션 유형을 모두 섞어서 사용할 수 있으나 충돌이 발생할 수도 있으니 여러 가지의 옵션들을 사용해 보고 필요한 옵션을 선택적으로 사용하는 것이 좋다. 리눅스 및 우분트 리눅스 등 리눅스 계열의 ps 명령의 기능과 세부 명령은 아래의 <표1-3>과 같다.  

<표1-3> ps 명령의 기능 및 세부 명령

ps 명령
기능
현재 실행 중인 프로세스의 정보를 출력한다.
형식
ps [옵션]
옵션
<유닉스 옵션>
-e : 시스템에서 실행 중인 모든 프로세스의 정보를 출력한다-f : 프로세스의 자세한 정보를 출려한다.
-l : -f 옵션 보다 더 자세히 정보를 출력한다.
-u uid : 특정 사용자에 대한 모든 프로세스의 정보를 출력한다. 
-p pid : pid로 지정한 특정 프로세스의 정보를 출력한다.
<BSD 옵션>
a : 터미널에서 실행한 프로세스의 정보를 출력한다. 
u : 프로세스 소유자 이름, CPU 사용량, 메모리 사용량 등 상세 정보를         출력한다.
x : 시스템에서 시랭 중인 모든 프로세스의 정보를 출력한다.
<GNU 옵션>
--pid PID 목록 : 목록으로 지정한 특정 PID의 정보를 출력한다.
사용법
ps        ps –ef          ps aux

ps 명령에 의한 현재 단말기의 프로세스 목록을 옵션 없이 사용하면 현재 셀이나 터미널에서 실행한 프로세스의 정보를 출력한다. 아래 <그림1-2>은 ps명령의 결과를 보여준다.


<그림1-2> ps 명령의 결과

여기서 PID는 프로세스 번호이고, TTY는 현재 터미널 번호,  TIME은 해당 프로세스가 사용한 CPU 시간의 양이며, CMD는 프로세스가 실행 중인 명령이 무엇인지 알려준다. 또한 bash를 터미널 0번에서 실행 중이고 PID가 4249번임을 알 수 있다. PID는 시스템에 따라 다르게 나타난다.

프로세스를 확인할 때 가장 많이 사용하는 ps 명령은‘ps –f’, ‘ps –ef’ 등의 명령이다. 아래 <그림1-3>는 ‘ps –ef’ 명령을 이용하여 프로세스의 상세한 정보를 출력한 것으로, 옵션이 없는 ps 명령에 비해 PPID와 터미널 번호, 시작 시간 등의 정보가 추가로 출력된다.
 
<그림1-3> ‘ps –ef’ 명령의 결과

위의 실행에서는 root 상용자는 —s를 17시 16분에 ?번 터미널에서 실행하고 있으며, 부모 프로세스의 PID(PPID)는 1번이다. ‘ps –ef’, ‘ps –f’ 명령의 상세 정보는 <표1-4>와 같다. 

<표1-4> ps –f 명령의 상세 정보

항목
의미
UID
프로세스를 실행한 사용자 ID
PID
프로세스 번호
PPID
부모 프로세스 번호
C
CPU 사용량(% 값)
STIME
프로세스의 시작 날짜나 시간
TTY
프로세스가 실행된 터미널의 종류와 번호
TIME
프로세스 실행 시간
CMD
실행되고 있는 프로그램 이름(명령)

ps 명령은 프로세스들의 구조를 트리(tree) 형태로 출력할 수도 있다. 프로세스를 트리(tree)구조로 출력하기 위해서는 pstree 명령을 사용해야 한다. 아래 <표1-5>는 pstree 명령의 상세 정보를 나타낸다.

<표1-5> pstree 명령의 상세 정보

옵션
설명
명령 형식
pstree [옵션]
-q
명령어 인수까지 출력
-n
PID 순으로 정렬하여 출력
-p
PID 출력
-u
UID 출력
-V
버전 정보 출력


아래 <그림1-4>에서는 pstree –p 옵션을 통해 pid를 출력한 모습을 나타내고 있다.


<그림1-4> pstree –p 명령의 결과

③ jobs 명령
프로세스 관리 명령 중에는 포그라운드, 백그라운드 프로세스와 작업 제어라는 명령이 존재한다. 여기서 작업 제어는 프로세스(현재 진행 중인 프로그로그램을 의미) 작업 진행 중 작업 전환, 작업 일시 중지, 작업 종료에 대한 제어를 뜻한다. 작업 전환은 포그라운드 작업을 백그라운드 작업으로 전환하거나, 백그라운드 작업을 포그라운드 작업으로 전환하는 것을 말한다. 작업 일시 중지는 작업을 잠시 중단하는 것이고, 작업 종료는 프로세스를 종료하는 것처럼 작업을 종료하는 것이다. 
여기서 포그라운드 작업과 백그라운드 작업에 대해 간략히 설명을 한다면 첫째, 포그라운드 작업은 터미널에서 작업할 때 일반적으로 사용자가 명령을 입력하면 셀이 그 명령을 해석하여 실행하고 결과를 화면에 출력한다. 그러면 사용자는 화면에 출력된 결과를 보고 다시 명령을 입력하는 대화식으로 작업을 수행한다. 이렇게 사용자가 입력한 명령이 실행되어 결과가 출력될 때까지 기다리는 방식으로 처리되는 프로세스를 포그라운드 프로세스하고 하며, 작업 제어에서는 포그라운드 작업이라고 한다. 아래 <그림1-5>는 포그라운드 작업의 예시이다.



<그림1-5> 포그라운드 작업


둘째, 백그라운드 작업은 한 번에 하나씩 실행하는 포그라운드 작업에 비해 작업 제어가 제공하는 백그라운드 기능을 사용하면 포그라운드 프로세스가 실행되는 동안에 뒤에서 다른 프로세스를 실행할 수 있으므로 한 터미널에서 여러 개의 프로세스를 동시에 실행할 수 있다. 즉 백그라운드 방식은 명령의 처리가 끝나는 것과 관계없이 곧바로 프롬프트가 출력되어 사용자가 다른 작업을 계속할 수 있다. 그러므로 여러 작업을 백그라운드로 실행한 후 터미널에서는 포그라운드 작업을 계속 진행할 수 있다. 백그라운드 방식으로 처리되는 프로세스를 백그라운드 프로세스라고 하며, 작업 제어에서는 백그라운드 작업이라 한다. 아래 <그림1-6>는 백그라운드 작업의 예시이다.


<그림1-6> 백그라운드 작업

이렇듯 진행 중인 작업을 제어하기 위해서는 현재 진행 중인 프로세스의 작업 목록의 정보를 확인할 수 있어야 한다. 이러한 프로세스의 작업 목록 보기의 명령이 jobs 명령이다.
jobs 명령은 현재 실행 중인 백그라운드 작업을 보는 명령이다. jobs는 배시(bash) 셀(shell)의 내부 명령이다. 아래 <표1-6>은 jobs 명령의 기능 및 상세 정보이다.

<표1-6> jobs 명령의 기능 및 상세 정보

jobs 명령
기능
백그라운드 작업을 모두 보여준다. 특정 작업 번호를 지정하면 해당 작업의 정보만 보여준다.
형식
jobs [%작업 번호]
%작업 번호
%번호 : 해당 번호의 작업 정보를 출력한다
%+ 또는 %% : 작업 순서가 +인 작업 정보를 출력한다.
%- : 작업 순서가 –인 작업 정보를 출력한다.
사용법
jobs         jobs %1

아래 <그림1-7>은 jobs 명령을 시행한 결과이다. 


<그림1-7> jobs 명령의 실행 결과
또한, jobs 명령에 의한 출력 결과의 의미를 하나씩 나타내면 아래 <표1-7>과 같다.

<표1-7> jobs 명령의 출력 정보

항목
출력 예
의미
작업 번호
[1]
작업 번호로서 백그라운드로 실행할 때마다 순차적으로 증가한다([1],[2],[3],..)
작업 순서
+
작업 순서를 표시한다.
● +: 가장 최근에 접근한 작업
● -: +작업 보다 바로 전에 접근한 작업
● 공백: 그 외의 작업
상태
실행중
작업 상태를 표시한다.
● 실행중: 현재 실행 중이다.
● 완료: 작업이 정상적으로 종료되었다.
● 종료됨: 작이이 비정상적으로 종료되었다.
● 장지됨: 작업이 잠시 중단되었다.
명령
sleep 100&
백그라운드로 실행 중인 명령이다.


▶ 작업 전화하기
작업 전환과 관련된 명령은 아래 <표1-8>과 같다.

<표1-8> 작업 전환명령

명령
기능
Ctrl+z 또는 stop %작업 번호
포그라운드 작업을 중지한다(종료하는 것이 아닌 잠시 중단하는 것이다).
bg %작업 번호
작업 번호가 지시하는 작업을 백그라운드 작업으로 전환한다.
fg %작업 번호
작업 번호가 지시하는 작업을 백그라운드 작업으로 전환한다.


현재 포그라운드로 실행 중인 작업을 백그라운드로 전환하려면 우선 Ctrl+z로 작업을 중지한 후 'bg %작업 번호' 명령으로작업을 백그라운드로 전환한다(bg 명령만 사용하면 작업 순서가 +인 작업에 적용된다).
▶ 작업 종료하기 : ‘Ctrl + c’
포그라운드 작업은 Ctrl+C를 입력하면 대부분 종료된다. Ctrl+c는 인터럽트 시그널을 포그라운드 프로세스에 전달하며,  인터럽트를 받으면 기본적으로 프로세스를 종료하도록 되어 있다.  물론 프로그램에서 Ctrl+c를 무시하도록 설정한 경우에는 종료되지 않는다.  
포그라운드 작업을 종료하는 또 다른 방법은 다른 터미널에서 해당 프로세스의 PID를 찾아 강제로 종료하는 것이다.  

ex) sleep 100  --> 포그라운드로 실행 중        
    ctrl+c   --> 강제 종료함.  
백그라운드 작업은 kill 명령으로 강제 종료해야 한다. kill 명령의 인자로 PID 대니 '% 작업 번호'를 지정해도 된다.  

ex) sleep 100&    --> 백그라운드로 실행 중        
    kill %1    --> 강제 종료 함.       
    [1]+ 종료됨            sleep 100    --> 종료 메시지 출력

▶ 로그아웃 후에도 백그라운드 작업 계속 실행하기 : nohup
백 그라운드 작업을 실행한 터미널이 종료되거나 사용자가 로그아웃하면 실행 중이던 백그라운드 작업도 함께 종료된다. 그런데 로그아웃한 다음에도 작업이 완료될 때까지 백그라운드 작업을 실행해야 할 경우가 있다. 이 때 nohup 명령 사용하며, <표1-9>는 nohup 명령의 상세 정보를 나타낸다.

<표1-9> nohup 명령의 상세 정보

nohup 명령
기능
로그아웃한 후에도 백그라운드 작업을 계속 실행한다.
형식
nohup 명령&


   - nohup 명령을 사용할 때에는 반드시 백그라운드로 실행해야 한다. 별도로 출력 방향 전환을 하지 않으면 명령의 실행 결과와 오류 메시지가 현재 디렉토리에 nohup.out 파일로 자동 저장된다.

④ kill 명령
프로세스 관리 명령 중에는 프로세스를 종료하기 위한 명령도 존재한다. 이러한 명령은 응답이 없는 프로세스나 불필요한 프로세스를 강제로 종료하려면 해당 프로세스의 PId를 알아야 한다. ps –ef나 ps aux 명령으로 프로세스의 정보를 확인하면 PID와 PPID를 알 수 있다. 프로세스를 종료하는 데는 ‘kill’이나 ‘pkill’ 명령을 사용한다. 이 명령들은 프로세스에 시그널을 보내어 프로세스를 종료한다.
시그널(signal)은 프로세스에 무언가 발생했음을 알리는 간단한 메시지이다. 이 메시지는 무엇이 발생했는지를 나타내는 미리 정의된 상수를 사용한다. 시그널은 번호로 구분되며 이름을 갖고 있다. 시그널을 받은 프로세스는 기본적으로 종료된다. 리눅스에서 지원하는 시그널의 목록은 kill –l 명령으로 알 수 있다. 아래 <그림1-8>은 kill –l 명령의 실행에 따른 상세 정보 화면이다.


<그림1-8> kill –l 명령의 상세 정보

<표1-10>은 주로 사용하는 시그널을 나타낸다.

<표1-10> 주로 사용하는 시그널(signal)

시그널
번호
기본 처리
의미
SIGHUP
1
종료
터미널과의 연결이 끊어졌을 때 발생한다.
SIGINT
2
종료
인터럽트로 사용자가 Ctrl+C를 입력하면 발생한다.
SIGQUIT
3
종료, 코어덤프
종료 신호로 사용자가 Ctrl+\을 입력하면 발생한다.
SIGKILL
9
종료
이 시그널을 받은 프로세스는 무시할 수 없으며 강제로 종료된다.
SIGALRM
14
종료
알람에 의해 발생한다.
SIGTERM
15
종료
kill 명령이 보내는 기본 시그널이다.


<그림1-9>는 시그널 핸들러(Handler)에 대해 나타내고 있으며, 각 시그널의 경우를 두어 선택되도록 한다. <표1-11>을 시그널 핸들러에 대한 설명이다.


<그림1-9> Signal Handler

<표1-11> 시그널 핸들러의 설명

● 프로세스가 특정 시그널을 포착했을 때 수행해야 할 별도의 함수(인터럽트 처리 함수)
● 프로그램을 개발할 때 시그널 신호를 받을 경우 특정 동작을 정의하는 함수
● 개발자는 프로그램을 개발할 때 특정 시그널을 수신했을 경우에 실행되기를 바라는 함수 또는 동작(시그널 핸들러)을 정의할 수 있습니다.
● 시그널 핸들러를 특별히 지정하지 않았을 경우 커널에 기본 정의된 액션(TERM, IGN, CORE, STOP, CONT)을 실행합니다.
● 예외적으로, 프로세스는 SIGKILL(9)과 SIGSTOP(19)에 대한 처리를 할 수 없도록 되어있습니다.
● 프로세스를 안전하게 종료하기 위해서는 SIGKILL(9)을 권장하지 않습니다. (해당 프로세스가 시그널 처리 불가능)


▶ kill 명령으로 프로세스 종료하기
kill 명령은 인자로 지정한 프로세스에 시그널을 전달한다. 프로세스는 각 시그널을 받았을 때 어떻게 처리할 것인지 동작이 지정되어 있다. 15번 시그널은 일반적으로 프로세스 종료이지만, 시그널을 무시하거나 다른 동작을 하도록 지정되어 있다면 프로세스가 종료되지 않을 수 있다.
kill 명령에서 시그널을 지정하지 않ㅇㄹ 경울 15번 시그널로 간주된다. 9번 시그널은 강제 종료이므로 무조건 종료되지만 좀비 프로세스의 경우 9번 시그널을 받아도 종료되지 않을 수 있다. 아래 <표1-12>은 kill 명령의 구조이며, <표1-13>는 프로세스 신호의 종류를 나타낸다.

<표1-12>  kill 명령의 구조

kill 명령의 구조
기능
지정한 시그널을 프로세스에 보낸다.
형식
kill [-시그널] PID
시그널
2: 인터럽트 시그널을 보낸다(Ctrl+C).
9: 프로세스를 강제로 종료한다.
15: 프로세스와 관련된 파일을 정리한 후 종료한다. 종료되지 않는 프로세스가 있을 수 있다.
사용법
kill   1001
kill  -9  1001
kill  -15  1001


<표1-13> 프로세스 신호 종류

신호 번호
신호 이름
설명
1
HUP
프로세스 종료 없이 구성파일 리로드
2
INT
키보드 인터럽트
3
QUIT
키보드 종료 및 덤프 생성
9
KILL
즉각적인 강제적 종료
15
TERM
정상적인 종료
18
CONT
중지된 프로세스 다시 시작
19
STOP
프로세스 동작 중지
20
TSTP
프로세스 동작 중지

▶ pkill 명령으로 프로세스 종료하기
kill 명령과 마찬가지로 시그널을 보내지만 PID 가 아니라 프로세스의 명령이름(CMD)으로 프로세스를 찾아 종료한다. kill 명령과 차이점은 해당하는 명령이름으로 여러 개가 검색될 경우 한 번에 모두 종료하지만 자신이 소유한 프로세스만 종료 가능하다.
ex) pkill man

▶ killall 명령으로 프로세스 종료하기
pkill 명령 처럼 프로세스의 명령 이름(CMD)으로 프로세스를 찾아 종료한다. 이 이름으로 실행 중인 모든 프로세스를 한 번에 종료하지만 해당 프로세스를 소유하고 있어야 한다.
































2) vim 에디터에서 매크로 사용 방법에 대하여 조사하기(q,@)

(1) 개요
리눅스에서 파일을 편집할 때는 GUNI에서 기본으로 제공하는 gedit를 사용해도 되지만, 터미널 환경에서 사용할 수 있는 편집기의 사용법도 알아야 한다. 실제로 시스템 관리를 위해 터미널을 많이 사용하는데 그때마다 파일을 열어서 보기 위해 gedit를 띄워야 하므로 불편하다. 이렇듯 리눅스에서 문서를 편집할 때는 문서 편집기를 사용하면 편리하다. 리눅스의 대표적인 문서 편집기는 바로 vim이다.
vim은 유닉스에서 제공한 편집기인 vi를 업그레이드한 것으로 기본적인 사용법은 vi와 같다. 리눅스에서 파일을 편집하려면 vim 사용법을 필수적으로 익혀야 한다.

(2) 문서 편집기의 종류
문서를 편집하는 것은 리눅스 전인 유닉스에서부터 사요했던 행 편집기(라인 편집기)와 화면 편집기가 있다. 행 편집기는 유닉스의 초기 편집기로 한 번에 한 행씩 작성하거나 수정할 수 있는데, GUI에 익숙하다면 이런 편집기를 사용하는 것은 대단히 번거롭고 귀찮기 때문에 유닉스나 리눅스를 사용하지 않을 것이다. 화면 편집기는 윈도의 메모장이나 gedit처럼 호면 단위로 내용을 보고 커서를 이동하면서 작업할 수 있다. 아래 <표2-1>은 리눅스에서 사용 가능한 편집기의 종류이다. 

<표2-1> 리눅스의 편집기 종류

구분
종류
행 단위 편집기
ed, ex, sed
화면 단위 편집기
vi, emacs
GUI 편집기
gedit


▶ 행 단위 편집기
   - ed: 유닉스 초기의 행 편집기로 지금은 거의 사용하지 않는다.
   - ex: 행 편집기이지만 단독으로 사용하기 보다는 vi에 연결하여 vi를 더욱 강력하게 하는 다양           한 기능을 제공한다. 
   - sed: 스크림 편집기로, 일반 편집기와 달리 지시된 명령에 따라 파일의 내용을 일과적으로 바           꾸어 줄력해준다. 셀 스크립트를 작성할 때 파이을 읽어들여 편집하는 기능을 수행하는            데 주로 사용된다.

▶ 화면 단위 편집기
   - vi: 리늑스에서 일반적으로 사용하는 화면 편집기이다. ex 편집기를 바탕으로 만들어졌기 때           문에 ex 편집기의 명령을 그대로 사용할 수 있고, 명령이 매우 단순하여 빠르게 편집할           수 있어서 널리 사용된다. vi는 행 편집기인 ed에 비해 편리하지만 글자를 입력하는 방법           부터 수정하고 삭제하는 방법이 일반적인 GUI 편집기와는 다르기 때문에 방법을 익히기           전까지는 다소 불편할 수 있다. 하지만 vi 사용법을 익히는 것은 리눅스를 제대로 활용하           려면 반드시 거쳐야 하는 과정이다.   - emacs(이맥스): 제공하는 긴으이 매우 다양하지만 사용법이 어렵고 복잡하여 전문적인 애호           가 위주로 사용되고 있는 편집기이다. 화면 단위 emacs 편집기 중에서는  GNU Emacs           가 가장 유명하다. GNU Emacs는 무료로 배포되며, 보통은 설치되어 있지 않으므로 별           도로 설치해야 한다.

(3) 모드형과 비모드형 편집기
또한, 문서 편집기는 모드형과 비모드형이 있다. 모드형은 입력 모드와 명령 모드가 구분되어 있고, 비모드형은 두 모드가 구분되어 있지 않다. 입력 모드는 텍스를 입력할 수 있는 모드이고, 명령 모드는 텍스트를 수정하고, 삭제하고, 복사하고, 붙이기를 하는 등 편집을 하는 모드이다. 우리가 윈도우에서 문서 작성용으로 주로 사용하는 한글과 워드는 비모드형 편집기이다. 
즉 비모드형 편집기에서는 편집 기능을 ‘Ctrl’ 이나 ‘Alt’ 같은 특수 키와 함께 사용한다. 반면에 모드형 편비기의 경우 같은 글자라도 입력 모두에서는 텍스트로 처리되어 입력되고, 명령 모드에서는 텍스트로 입력되는 것이 아니라 편집 명령으로 사용된다. vi가 바로 대표적인 모드형 편집기인데 입력 모드와 명령 모두가 따로 있어 입력 모드에서 j를 누르면 j가 입력되지만 명령 모두에서 j를 누르면 커서가 아래로 이동한다.
아래 <표2-2>르 보면 입력 모드에서느 모드형과 비모드형 모두 입력한 테스트가 그대로 입력됨을 알 수 있다. 그러나 명령 모드에서는 모드형의 경우 그냥 알파벳을 누르면 되고, 비모드형의 경우 ‘Ctrl’ 키와 함께 사용한다. 모드형에서는 모드 전환 키가 필요하며, 비모드형의 경우 입력 모드나 명령 모드의 구분이 없으므로 모드 전환 키가 필요하지 않다.

<표2-2> 모드형과 비모드형 편집기의 비교

구분
모드형(vi)
비모드형(메모장)
입력 모드
텍스트 입력
명령 모드
복사
yy
‘Ctrl + c’
붙이기
p
‘Ctrl + v’
저장
:wq, ZZ
‘Ctrl + s’
모드 전환
I, a, o, ‘Esc’
해당 없음


(4) vim 이란?
vim은 vi 호환 텍스트 편집기이다. 대부분 mac os나 리눅스에 기본적으로 깔려있어서 터미널에서 사용이 가능합니다.  현재 visual studio, vscode, atom, android studio 등과 같이 많은 에디터들이 존재하는데도 굳이 vim 에디터는 왜 필요할까요? vim 에디터는 다른 에디터들과 다르게 터미널에서 직접 파일 생성, 수정이 가능합니다. aws에서 내프로젝트 를 배포하고, env 파일이나 다른 등등.. 파일들을 생성 수정할 일들이 있는데 터미널에서 작업할 수 있는 장점이 있습니다.

(5) vim 사용법
vim 에디터는 어떻게 사용해야 하는지 알아보자.

▶ 실행하기
터미널에서 vim 명령어로 실행할 수 있다. vim 명령어의 구조는 ‘$ vim [파일명]’으로 되어 있으며, ‘$ vim index.js’ 식으로 명령을 내릴 수 있다. 이때 현재 경로에 index.js 파일이 없다면 생성되고, 있다면 index.js 파일에 저장되어 있는 정보가 터미널에 나타난다. 아래 <그림2-1>은 터미널에 표시된 vim 명령이다.


<그림2-1> vim 명령 실행

아래 <표2-3>은 vim의 실행 명령 중 편집 모드를 나타내며, 편집을 시작하려면 <표2-3>과 같은 명령어를 입력해야 한다. 

<표2-3> 편집 모드

항목
설명
i
현재 위치에서 —insert—mode가 시작된다.
o
들여 쓰기 된 상태로 insert mode가 시작된다.
a
다음 문자열에서 insert mode가 시작된다.
I
커서가 위치한 행의 첫 컬럼으로 이동하여 입력한다.
A
커서가 위치한 행의 마지막 칼럼으로 이동하여 입력한다.
O
커서가 위치한 행의 이전 행에 입력한다.


아래 <그림2-2>는 리눅스에서 실행된 편집 모드 이다.


<그림2-2> 편집 모드 실행

▶ 저장 & 종료
코드를 다 작성했다면 이제 저장하거나 종료를 해야 한다. 저장 및 종료 역시 아래 <표2-4>에 표시된 명령어들을 이용하여 진행하여야 한다.

<표2-4> 자장과 종료 명령

항목
설명
:q
코드 수정 없이 종료할 때 사용한다.
:q!
강제로 에디터를 종료한다.
:w
변경사항들을 저장한다.
:wq
변경사항들을 저장해주고 에디터를 종료한다.
:e[파일명]
[파일명]으로 이동합니다.

아래 <그림2-3>은 파일을 수정하고 저장하고 종료하는 모습이다.


<그림2-3> 파일 수정, 저장, 종료

▶ 창 분할
창 분할도 아래 <표2-5>의 명령을 이용하여 내려야 하며, <그림2-4>는 창 분할 명령 실행을 보여준다.

<표2-5> 창 분할의 세부 명령

항목
설명
:vs[파일명]
세로로 창을 분할 한다.
:sp[파일명]
가로로 창을 분할 한다.



<그림2-4> 창 분할 명령 실행

(6) vim 매크로(macro)
Macro는 Vim 명령어'들'을 기록하고, 이를 반복할 수 있는 기능이다. 이전에 Vim Micro Macro(dot command)를 활용해서 이전 명령을 바로 반복할 수 있었다. 그러나, 이는 이전 명령을 반복할 뿐, '이동 후 명령'과 같은 작업에 대해서는 그 반복이 불가능하다.
그렇다면 ‘매크로’는 어느 순간에 필요한 것인가? 가령 다음 스크린샷의 좌측과 같은 코드가 있다고 가정해보자. 이를 오른쪽 코드와 같이 바꾸고자 한다. javascript 에서 key 를 그대로 value 에 넣은 뒤 이를 대문자로 바꾸려고 한다. 아래 <그림2-5>는 vim 매크로 기능을 활용<좌측 코드를 우측 코드와 바꾸기>를 나타낸다. 


<그림2-5> vim 매크 활용(1)

일단, jazz가 포함된 라인(2번줄)에서 vim을 활용하여 이 과정을 진행한다면 아래 <그림2-6>과 같이 기존 코드를 변경한다.


<그림2-6> 기존 코드 변경

이 작업을 수행하기 위한 시퀀스를 다음 순서를 따르며, key에 해당하는 문자열을 value string에 그대로 넣은 뒤 대문자로 변경하는 과정은 <그림2-7>과 같다.
	1. jazz의 j로 커서를 이동한다.(^)
	2. 단어를 복사한다.(yiw)
	3. 첫 번째 따옴표로 이동한다.(f“)
	4. 복사한 단어를 붙여넣는다.(p)
	5. 분여넣어진 단어를 대문자로 변경한다.(gUaw)
		-참고: ‘gU{모션}’은 모션은 범위를 대문자로 변경한다.  gu는 소문자로 변경한다.
	6. 아래 주로 이동한다.(j)

 
<그림2-7> key에 해당하는 문자열을 value string에 넣은 뒤 대문자로 변경하는 과정
위에서 설명한 1-6까지의 과정이 똑같이 반복된다면 opera가 포함된 라인에도 동일한 동작이 수행되게 할 수 있으므로 굳이 매크로르 쓰지 않아도 적절히 몇 번 반복하면 끝난다고 생각할 수 있지만 동일한 작업의 라인이 수십줄이 넘어간다고 상상해보자. 매크로를 활용하지 못한다면 각 라인마다 각각 12회의 키를 입력해야 한다. 매크로의 기능이 절실할 것이다.
이러한 관점에서 일련의 동작들을 기록하고 재사용할 수 있도록 하는 기능이 바로 ‘vim macro’ 이다. <표2-6>은 vim macro의 세부 명령을 나타낸다. 

<표2-6> vim macro 세부 명령

항목
설명
‘q{레지스터}’
매크로 기록 시작
‘q’
매크로 기록 중지
‘@{레지스터}’
저장된 매크로 실행
‘@@’
직전에 실행한 매크로 실행
‘{반복회수}@{레지스터}’
또는
‘{반복횟수}@@’
저장된 매크로를 ‘반복횟주’만큼 재실행


▶ q – vim macro 기록하기 & 기록 종료하기
Normal Mode에서 q를 입력하면, 하단 상태표시줄에 q가 표시된다. 이는 앞으로 기록할 레지스터를 지정해주기를 대기하고 있는 상태이다. 레지스터(a-z, 0-9 중 하나)를 정하여 입력하면 상태표시줄에 'Recording @a'(레지스터로 'a'를 입력했다고 가정)와 같이 실제 명령어를 대기하고 있는 상태가 된다. 일련의 동작들을 입력한 뒤 다시 q를 입력하면 매크로 기록이 종료된다.

아래 <그림2-8>은 위의 1~6 과정에서 입력한 과정들을 매크로로 기록하는 과정을 나타내며, 매크로 기록할 레지스터로 a를 사용했다.


<그림2-8> 매크로 기록 과정

▶ @ - vim macro 실행하기
`@{레지스터}`로 특정 레지스터에 저장된 매크로를 실행시킬 수도 있고, `@@`로 직전에 실행한 매크로를 재실행할 수도 있다. "opera"라인(3번줄)은 `@a`로 재실행하면 아래 <그림2-9>와 같으며, <그림2-8>에서 이어진다.


<그림2-9> @{매크로가 저장된 레지스터}를 통해 저장된 매크로를 실행시키는 단계

rock라인은(4번줄)은 `@@` 로 직전에 실행한 매크로를 반복하면 아래 <그림2-10>과 같으며, <그림2-9>에서 이어진다.


<그림2-10> @@ 명령으로 직전에 실행된 매크로를 재실행하는 단계

지금까지 매크로의 사용법을 알아보았으며, 매크로를 활용하는 것은 이것이 전부라 해도 과언이 아니다. 아래에서 매크로와 관련하여 몇 가지 사항을 더 알아보도록 하겠다.

▶ 레지스터에 저장된 매크로 확인해보기
vim에서는 레지스터에 저장된 내용을 확인하기 위한 command mode 명령어를 제공한다. `:register`가 그것이다. 단순히 이 명령어를 입력하면 모든 레지스터의 저장된 값들을 리스팅해준다. ':register'명령어는 인자를 받기도 하는데, `:register a`와 같이 명령어의 인자로 레지스터명을 전달하면 해당 레지스터에 저장된 값을 표현해준다(오리지널 vim 에서도 UI만 다를 뿐 VSCode Vim과 동일하게 동작한다.). 아래 <그림2-11>은 VSCode Vim 에서 `:register` 커맨드 모드 명령어로 레지스터의 내용을 확인하는 모습, a 레지스터에 우리가 저장한 동작이 보인다.



<그림2-11> VSCode Vim에서의 레지스터 동작 특성



<그림2-12> 레지스터를 지정하여("a) 붙여넣기(p)를 수행한 모습

레지스터에 저장된 내용이기 때문에, 당연하게도 `"ap` 명령어로 a 레지스터의 내용을 붙여넣을 수 있다. 위의 <그림2-12>는 레지스터를 지정하여("a) 붙여넣기(p)를 수행한 모습이다. 우리가 매크로로 기록했던 내용이 붙여넣어졌다. 매크로는 레지스터에 저장된다는 점을 활용하여 복잡한 매크로의 경우 .vimrc 등의 파일에 등록하여 관리하기도 한다.
매크로는 하나의 명령이기 때문에 매크로를 실행하기 전에 반복횟수를 지정할 수 있다. 반복횟수의 지정은 단어와 단어로 구조화되어 있으며 tap 문자로 구분되어 있다. 아래 <표2-7>은 매크로에서 반복횟수를 지정하는 tap 문자를 나타낸다.

<표2-7> 매크로 반복횟수 지정 tap 문자

매크로 반복횟수 지정 tap 문자








위의 반복횟수 지정 데이터를 가공하여 각 라인을 아래 <그림2-13>처럼 처리할 수 있다.


<그림2-13> 반복횟수 지정

이 과정을 매크로의 기능을 활용하여 반복하려면 매크로를 기록하고 모든 라인에 적용하면 된다. 아래 <그림2-14>는 작업 과정을 매크로로 기록하는 단계를 나타낸다.


<그림2-14> 첫번째 줄을 요구사항대로 가공하는 동작을 매크로에 기록하는 장면
<그림2-14>에서 매크로로 기록한 작업을 순서에 따른 기능을 전체 라인에 적용하면 사용자가 힘들이 각 라인별로 작성하지 않아도 매크로에 의해 자동을 적용된다. 아래 <그림2-15>는 매크로에 의해 전체 라인이 적용되는 단계를 보여준다.


<그림2-15> 100@@ 로 나머지 라인들에 대해 매크로를 일괄적으로 적용하는 모습

이와 같이 '충분한' 숫자를 반복횟수로 지정하여 남아있는 처리 대상에 대해 매크로가 적용되게 할 수 있다. 매크로는 더 이상 진행될 수 없으면 그 동작을 멈추므로 실제로는 37 라인밖에 되지 않지만, `100@@`와 같이 '충분한' 반복횟수를 지정하는 것으로 편리하게 '나머지 대상 전부'를 지정할 수 있다.
위의 <그림2-15>의 경우처럼 100의 경우 그 처리가 제대로 되지 않은 것을 확인할 수 있는데(one hundred만 이름 사이에 공백이 들어가 있음), 매크로를 기록할 때 이러한 다양한 상황까지 고려하여 작성해주어야 할 필요가 있을 수 있다.
매크로는 동일한 이름을 공유하는 마이크로 매크로(dot command)보다는 그 활용도가 낮다고 할 수 있다. 매크로는 위에서 본 것과 같이 '복잡한 시퀀스'를 '여러번 수행'하여야 할 때 그 진가를 발휘한다. 그러므로 반복되는 작업은 매크로를 활용하여 편리하게 작업하자.
