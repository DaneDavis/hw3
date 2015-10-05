I have done various debugging techniques on this code
I recieve all this after running a backtrace:

Program received signal SIGSEGV, Segmentation fault.
0x00007ffff7a5ed17 in _IO_vfprintf_internal (
    s=s@entry=0x7fffff7ff430, 
    format=format@entry=0x7ffff7b95830 "%s%s%s:%u: %s%sAssertion `%s' failed.\n%n", ap=ap@entry=0x7fffff7ff558)
    at vfprintf.c:270
270	vfprintf.c: No such file or directory.
(gdb) backtrace
#0  0x00007ffff7a5ed17 in _IO_vfprintf_internal (
    s=s@entry=0x7fffff7ff430, 
    format=format@entry=0x7ffff7b95830 "%s%s%s:%u: %s%sAssertion `%s' failed.\n%n", ap=ap@entry=0x7fffff7ff558)
    at vfprintf.c:270
#1  0x00007ffff7a872a3 in _IO_vasprintf (
    result_ptr=0x7fffff7ff680, 
    format=0x7ffff7b95830 "%s%s%s:%u: %s%sAssertion `%s' failed.\n%n", args=args@entry=0x7fffff7ff558) at vasprintf.c:62
#2  0x00007ffff7a69657 in ___asprintf (
    string_ptr=string_ptr@entry=0x7fffff7ff680, 
    format=format@entry=0x7ffff7b95830 "%s%s%s:%u: %s%sAssertion `%s' failed.\n%n") at asprintf.c:35
#3  0x00007ffff7a44ae2 in __assert_fail_base (
    fmt=0x7ffff7b95830 "%s%s%s:%u: %s%sAssertion `%s' failed.\n%n", 
    assertion=assertion@entry=0x400a02 "(void*)temp == request", file=file@entry=0x4009f8 "mm_test.c", line=line@entry=36, 
    function=function@entry=0x400a57 <__PRETTY_FUNCTION__.3486> "requestSpace") at assert.c:57
#4  0x00007ffff7a44c32 in __GI___assert_fail (
    assertion=0x400a02 "(void*)temp == request", 

I recieve some error regarding print formats and have been unable to solve this..
My code is of a malloc, free and reallocate format but due to this error I recieve a segfault 
