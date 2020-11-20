# minishell

[서브젝트 버전: 2020/11/20 다운로드](https://github.com/yeosong1/yeosong1.github.io/files/5571503/en.subject.pdf)


요약 :
이 프로젝트의 목적은 간단한 셸을 만드는 것입니다.  <br>
네, 당신의 자신의 작은 bash 또는 zsh이요.       <br>
프로세스 및 파일 설명자에 대해 많이 배우게 될 것입니다.

# 소개
쉘의 존재는 `IT`의 존재 직결되어 있습니다.  <br>
당시 모든 코더는 *정렬된 1/0 스위치를 사용하여 컴퓨터와 통신하는 것은 진심으로 성가시다는 것* 에 동의했습니다.  <br>
*어떤 식으로든 영어에 가까운 대화형 명령줄을 사용해서 컴퓨터와 소통하겠다* 는 아이디어를 내놓은 것은 정말 논리적이었습니다.  <br>  <br>

Minishell을 통해, 당신은 시간을 거슬러올라가 Windows가 존재하지 않았을 때 사람들이 직면했던 문제를 만나는 여행을 할 수 있습니다.

# Common Instruction

<details>
<summary> <b> 평소랑 같아요(펼쳐보기)</b>  </summary>
<div markdown="1">

- 귀하의 프로젝트는 규범에 따라 작성되어야합니다. 보너스가있는 경우 파일 / 함수, 표준 검사에 포함되며 해당하는 경우 0을 받게됩니다.
내부의 표준 오류입니다.
- 기능이 예기치 않게 종료되지 않아야합니다 (세그먼트 오류, 버스 오류, 이중 free 등) 정의되지 않은 동작을 제외하고. 이런 일이 발생하면 프로젝트는
작동하지 않는 것으로 간주되며 평가 중에 0을 받게됩니다.
- 필요한 경우 모든 힙 할당 메모리 공간을 적절히 해제해야합니다. 누출 없음 용인 될 것입니다.
- 주제가 요구하는 경우, 당신의 컴파일을위한 Makefile을 제출해야합니다. -Wall, -Wextra 및 -Werror 플래그를 사용하여 필요한 출력에 소스 파일을 추가합니다.
Makefile은 다시 연결해서는 안됩니다.
- Makefile에는 최소한 $ (NAME), all, clean, fclean, re.
- 프로젝트에 보너스를 적용하려면 Makefile에 규칙 보너스를 포함해야합니다. 금지 된 모든 다양한 헤더, 라이브러리 또는 기능을 추가합니다. 프로젝트의 주요 부분. 보너스는 다른 파일 _bonus. {c / h}에 있어야합니다.
필수 및 보너스 부품 평가는 별도로 수행됩니다.
- 프로젝트에서 libft를 사용할 수있는 경우 해당 소스와 libft 폴더의 관련 Makefile과 관련 Makefile. 프로젝트 Makefile은 Makefile을 사용하여 라이브러리를 컴파일 한 다음 프로젝트를 컴파일해야합니다.
- 이 작업에도 불구하고 프로젝트에 대한 테스트 프로그램을 만드는 것이 좋습니다. 제출할 필요가 없으며 채점되지 않습니다. 그것은 당신에게 기회를 줄 것입니다
자신의 작업과 동료의 작업을 쉽게 테스트 할 수 있습니다. 특히 그 테스트를 찾을 수 있습니다 수비 중에 유용합니다. 실제로 수비 중에는 테스트를 자유롭게 사용할 수 있습니다.
및 / 또는 평가중인 동료의 테스트.
- 할당 된 git 저장소에 작업을 제출합니다. git 저장소의 작업 만 등급이 지정됩니다. Deepthought가 작업 등급을 지정하면 완료됩니다. 동료 평가 후. 작업 중에 오류가 발생한 경우 Deepthought의 채점, 평가가 중지됩니다.
</div>
</details>
<br>

# 필수 파트

- [x] 프로그램 이름이 minishell 인가?
- [x] Makefile이 있는가?
- [x] Libft 사용 가능합니다.
- [x] 한 마디로: shell을 작성하세요.

| 이름 | 형태 | 사용처 | 예시 | 헤더 |
| --- | --- | ---  | --- | --- |
| malloc  | void * malloc(size_t size);                               | 메모리 할당할 때         || #include <stdlib.h> |
| free    | void free(void *ptr);                                     | 할당한 메모리 해제할 때    || #include <stdlib.h> |
| write   | ssize_t write(int fildes, const void *buf, size_t nbyte); | 콘솔 쓰기              || #include <unistd.h> |
| open    | int open(const char *path, int oflag, ...);               | 시스템콜 파일 오픈       || #include <fcntl.h>  |
| read    | ssize_t read(int fildes, void *buf, size_t nbyte);        | 시스템콜 파일 읽기       || #include <sys/types.h> <sys/uio.h> <unistd.h> |
| close   | int  close(int fildes);                                | 시스템콜 파일 닫기       || #include <unistd.h> |
| fork    | pid_t fork(void);                            | 부모 프로세스와 같은 자식 프로세스를 복제 || #include <unistd.h> |
| wait | pid_t wait(int **별**stat_loc); | 부모가 자식 프로세스를 끝나기 기다리는 함수, 자식 프로세스로부터 signal 받으면 종료되면서, 부모 프로세스에 SIGCHLD 시그널이 보내짐. 자식이 에러면 -1, 정상이면 0 리턴 | #include <sys/wait.h> |
|         |                         | 자식 프로세스 끝난 걸 확인하면 그 뒤에 줄에 있는 부모 프로세스의 남은 코드를 진행한다.
| waitpid | pid_t waitpid(pid_t pid, int *stat_loc, int options); | 프로세스pid가 종료되길 기다리는 함수 | #include <sys/wait.h> |
| wait3   | pid_t wait3(int *statloc, int options, struct rusage *rusage); |자식종료 기다리며, 종료된 프로세스의 상태/자원 사용량을 알려줌|#include <sys/wait.h> |
| wait4   | pid_t wait4(pid_t pid, int *statloc, int options, struct rusage *rusage);|위와 같음?|#include <sys/wait.h> |
| signal  | void (*signal(int sig, void (*func)(int)))(int);  ||#include <signal.h>|
|         | 또는 읽기 쉽게 typedef void (*sig_t) (int); 해서 아래처럼 |||
|         | sig_t   signal(int sig, sig_t func);               |||
| kill    |
| exit    | void exit(int status);
| getcwd  |
| chdir   |
| stat    |
| lstat   |
| fstat   |
| execve  |
| dup     |
| dup2    |
| pipe    |
| opendir |
| readdir |
| closedir |
| strerror |
| errno   |


<details>
<summary> <b> 사용 가능한 함수의 목록 (펼쳐 보기)</b>  </summary>
<div markdown="1">

  - malloc
  - free
  - write
  - open
  - read
  - close
  - fork
  - wait
  - waitpid
  - wait3
  - wait4
  - signal
  - kill
  - exit
  - getcwd
  - chdir
  - stat
  - lstat
  - fstat
  - execve
  - dup
  - dup2
  - pipe
  - opendir
  - readdir
  - closedir
  - strerror
  - errno
</div>
</details>
<br>

당신의 쉘은 반드시:

- [ ] 새 명령을 기다릴 때 프롬프트 표시
- [ ] 올바른 실행(executable) 파일을 검색하고 실행합니다(실행 파일 - PATH 변수 또는 상대 또는 절대 경로를 기반으로) (bash에서와 같이)
- [ ] 내장 기능(빌트인)을 구현해야합니다. (bash에서와 같이)
  - [ ] `echo` ’-n’옵션도
  - [ ] `cd` 상대 또는 절대 경로만
  - [ ] `pwd` 옵션 없이
  - [ ] `export` 옵션 없이
  - [ ] `unset` 옵션 없이
  - [ ] `env` 옵션 및 인수 없이
  - [ ] `exit` 옵션 없이
- [ ] 명령에서의 ;는 명령을 분리해야합니다. (bash에서와 같이)
- [ ] ....는 여러 줄 명령을 제외하고 bash 에서처럼 작동해야합니다. (bash에서와 같이)
- [ ] 리디렉션.....은 파일 설명자 집계를 제외하고 작동해야합니다. (bash에서와 같이)
- [ ] 파이프 &#124; (bash에서와 같이)
- [ ] 환경 변수 ($ 뒤에 문자) (bash에서와 같이)
- [ ] ...(bash에서와 같이)
- [ ] ...는 bash에서와 동일한 결과를 가져야합니다.


# 보너스 파트

- 필수 부분이 완벽하지 않다면 보너스에 대해 생각조차하지 마세요
- 모든 보너스를 할 필요는 없습니다.

- [ ] ... 리디렉션 (bash에서와 같이)
- [ ] Termcaps를 사용한 히스토리 및 줄 편집 (예 : man tgetent)
  - [ ] 커서가 있는 줄을 편집합니다. 특정 위치에서 선을 편집 할 수 있도록 커서를 왼쪽과 오른쪽으로 이동합니다. 분명히 기존 문자 사이에 새 문자를 삽입해야합니다. 고전적인 껍질과 비슷합니다.
  - [ ] 위쪽 및 아래쪽 화살표를 사용하여 명령 내역을 탐색합니다. 그런 다음 원하면 편집 할 수 있습니다 (히스토리 말고 선).
  - [ ] 원하는 키 시퀀스를 사용하여 줄의 전체 또는 일부를 잘라 내고 복사하고 / 또는 붙여 넣습니다.
  - [ ] Ctrl + LEFT를 사용하여 왼쪽 또는 오른쪽으로 단어 단위로 직접 이동하고 Ctrl + 오른쪽.
  - [ ] 홈과 끝을 눌러 줄의 시작 또는 끝으로 바로 이동합니다.
  - [ ] 몇 줄에 걸쳐 명령을 작성하고 편집합니다. 이 경우 우리는 그것을 좋아할 것입니다 ctrl + UP 및 ctrl + DOWN을 사용하면 명령에서 한 줄에서 다른 줄로 이동할 수 있습니다. 동일한 열 또는 그렇지 않으면 가장 적합한 열에 남아 있습니다.
- [ ] &&, &#124;&#124; 우선 순위 괄호 (bash에서와 같이)
- [ ] wilcard * (bash에서와 같이)


------------------------------------

# 일반 파트 작성을 위한 배경 지식 & 구현 과정

##  새 명령을 기다릴 때 프롬프트 표시


## 올바른 실행(executable) 파일을 검색, 실행
실행 파일 - PATH 변수 또는 상대 또는 절대 경로를 기반으로
## 내장 기능(빌트인)
### echo
-n
### cd
상대 또는 절대 경로만
### pwd
옵션 없이
### export
옵션 없이
### unset
옵션 없이
### env
옵션 및 인수 없이
### exit
옵션 없이

## ; 로 명령 분리

## 따옴표...
여러 줄 명령을 제외하고 bash 에서처럼 작동해야합니다.

## 리디렉션 
파일 설명자 집계를 제외하고 작동해야합니다.

## 파이프 

## 환경 변수 ( 뒤에 문자)
