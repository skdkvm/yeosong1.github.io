# miniRT [시작 예제] 창 띄워보기

* 현재 환경: macOS Mojave 10.14.6


## 강의에 나오는대로 하기: /usr/경로에/넣어서

**0**  minilibx_opengl.tgz와 minilibx_mms_20200219_beta.tgz 다운로드, 압출 풀기<br>
**1**  두 폴더에 들어가서 make 해서 라이브러리 파일을 만든다<br>
**2**  /usr/local/include/에 헤더 복사

~~~
cp minilibx_mms_20200219/*.h /usr/local/include/
cp minilibx_opengl_20191021/*.h /usr/local/include/ 
~~~

**3**  /usr/local/lib/에 라이브러리 파일 복사

~~~
cp minilibx_mms_20200219/libmlx.dylib /usr/local/lib/
cp minilibx_opengl_20191021/libmlx.a /usr/local/lib/ 
~~~

**4**  [mlx 개발자 OL님이 인트라 강의에서 시키는대로](https://elearning.intra.42.fr/notions/minilibx/subnotions/mlx-introduction/videos/introduction-to-minilibx) start.c 작성

~~~
#include "mlx.h"

int	main()
{
	void	*mlx_ptr;
	void	*win_ptr;


	mlx_ptr = mlx_init();
	win_ptr = mlx_new_window(mlx_ptr, 500, 500, "띄울_창_타이틀");
	mlx_loop(mlx_ptr);
}
~~~

**5**

~~~
강의에서 적은대로 쓰면 이렇고
cc -I /usr/local/include/ miniRT/start.c -L /usr/local/lib/ -lmlx -framework OpenGL -framework AppKit

그냥 cc -lmlx start.c 해도 된다..

./a.out
~~~

창이 뜬다.<br>
<img width="612" alt="스크린샷 2020-05-27 오후 8 47 32" src="https://user-images.githubusercontent.com/53321189/83015376-5498f580-a05b-11ea-9cfa-86d9b3c732bb.png">

#### OpenGL?
오픈 그래픽 라이브러리은 1992년 실리콘 그래픽스사에서 만든 2차원 및 3차원 그래픽스 표준 API 규격으로, 프로그래밍 언어 간 플랫폼 간의 교차 응용 프로그래밍을 지원한다.

#### AppKit?
일반적으로 AppKit이라고 하는 Application Kit는 NeXTSTEP의 그래픽 사용자 인터페이스 툴킷 입니다. Foundation 및 Display PostScript 와 함께 OpenStep API 사양의 핵심 부분 중 하나입니다. macOS와 함께 번들로 제공되는 대부분의 응용 프로그램 (예 : Finder , TextEdit , Calendar 및 Preview)은 AppKit을 사용하여 사용자 인터페이스를 제공합니다.



---------------------------------------



## 지금 내 루트 안에서 가져다 쓰기

**0**  minilibx_*.tgz 다운로드, 압축 풀기<br>
**1**  각 폴더 들어가서 make<br>
**2**  [mlx 개발자 OL님이 인트라 강의에서 시키는대로](https://elearning.intra.42.fr/notions/minilibx/subnotions/mlx-introduction/videos/introduction-to-minilibx) start.c 작성

~~~
#include "mlx.h"

int	main()
{
	void	*mlx_ptr;
	void	*win_ptr;


	mlx_ptr = mlx_init();
	win_ptr = mlx_new_window(mlx_ptr, 500, 500, "띄울_창_타이틀");
	mlx_loop(mlx_ptr);
}
~~~

**3**  루트에 각 폴더 속 liblmx.*를 카피<br>

(위에 있는 /usr/경로에 넣는 작업을 안했더니 permission denied 나오면서 execute가 안된다..<br>
mms 또는 opengl 폴더 안에 있는 liblmx.* 파일을 루트로 가져오면 실행이 잘 된다.)

~~~
cp minilibx_mms_20200219/libmlx.dylib .
cp minilibx_opengl_20191021/libmlx.a .

gcc -I minilibx_mms_20200219 libmlx.dylib srcs/start.c
// 지금은 liblmx.a에 있는 함수 쓴 게 없어서 liblmx.a는 안불러와도 된다.

./a.out
~~~

창이 뜬다.<br>
<img width="612" alt="스크린샷 2020-05-27 오후 8 47 32" src="https://user-images.githubusercontent.com/53321189/83015376-5498f580-a05b-11ea-9cfa-86d9b3c732bb.png">

ctrl c 해서 닫기.
