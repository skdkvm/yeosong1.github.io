---
published: true
lang: 'ko'
---
# Libft
위키 만들기 전에 풀어가지고... 기록이 없다..

## 주의
* ft_split(“”, ‘a’)
  - ret[0] = NULL;
  - printf("[%s] ", ret[0]) ----> [(null)]
* ft_split(“cde”, ‘a’)
  - printf("[%s] ", ret[0]) ----> [cde]
  - printf("[%s] ", ret[1]) ----> [(null)]
* ft_split에서 2번째 malloc 실패시 앞에 성공했던 malloc들도 free 하기

## Tester
collected in 2020.<br>
- [https://github.com/jtoty/Libftest](https://github.com/jtoty/Libftest)
- [https://github.com/alelievr/libft-unit-test](https://github.com/alelievr/libft-unit-test)
- [https://github.com/ska42/libft-war-machine](https://github.com/alelievr/libft-unit-test)
