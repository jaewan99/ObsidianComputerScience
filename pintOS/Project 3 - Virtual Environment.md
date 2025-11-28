Background
source files

1. The Makefile is updated to turn on the setting -DVM. We provide an enormous amount of template code. Use the template code

우리가 바꿔야할 파일들

1.  vm/vm.c
	1. provide general interface for virtual memory
2. uninit.c
	1. all pages are initially set up as uninitialized pages, then it transforms to anonymous pages or file-backed pages.
3. anom.c
	1. anonymous pages - page not related to the file
4. file.c
	1. file = page related to the file

Memory Terminology

1. pages, virtual page - is a continuous region of virtual memory of size 4096 bytes (the page size) in length. 

choices of implementation
1. pintos includes a bitmap data structure in bitmap.c
2. hash data structure

organization of supplemental page table
1. In terms of segments and in terms of pages.
	1.  a segment here refers to a consecutive group of pages, i.e. memory region containing an executable or a memory-mapped files.

Handling page fault
1. the most important use of the supplemental page table is the page fault handler.

Memory Management
1. Note that, for your understanding, we use the term "page" for virtual page, and the term "frame" for a physical page.