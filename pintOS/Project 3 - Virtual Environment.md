Background
source files

1. The Makefile is updated to turn on the setting -DVM. We provide an enormous amount of template code. Use the template code
	1. Makefile에서 -DVM설정을 on 했습니다. 추가적으로 template code을 많이 제공합니다. 이를 꼭 이용하세요

우리가 바꿔야할 파일들
1.  vm/vm.c
	1. provide general interface for virtual memory
		1. 가상메모리 용 기본적인 인터페이스를 제공합니다 
2. uninit.c
	1. all pages are initially set up as uninitialized pages, then it transforms to anonymous pages or file-backed pages.
		1. 모든 페이지 처음에는 모드 uninit이다
3. anom.c
	1. anonymous pages - page not related to the file
4. file.c
	1. file = page related to the file

Memory Terminology

1. pages, virtual page - is a continuous region of virtual memory of size 4096 bytes (the page size) in length. 