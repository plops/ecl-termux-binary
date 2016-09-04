```
cd ~/ecl
./configure --host=arm-linux-androideabi --with-system-gmp --enable-boehm=included  --with-cxx --with-dffi --disable-soname --prefix=/data/data/com.termux/files/usr/local --with-cross-config=`pwd`/src/util/android.cross_config
```


```
> *features*

(:WALKER :ECL-BYTECMP :LINUX :FORMATTER :ECL-WEAK-HASH :LITTLE-ENDIAN
 :ECL-READ-WRITE-LOCK :LONG-LONG :UINT64-T :UINT32-T :UINT16-T
 :RELATIVE-PACKAGE-NAMES :LONG-FLOAT :UNICODE :DFFI :CLOS-STREAMS :CMU-FORMAT
 :UNIX :ECL-PDE :CLOS :THREADS :BOEHM-GC :ANSI-CL :COMMON-LISP
 :IEEE-FLOATING-POINT :PREFIXED-API :FFI :ARMV7L :COMMON :ECL)

```
```
su
cd /
tar xf /data/data/com.termux/files/home/ecl-16.1.2_termux.tar
export PATH=$PATH:/usr/local/bin
```

Trying to install slime:

```
git clone https://github.com/slime/slime
cd slime
ecl -load swank-loader
(require 'sb-bsd-sockets)
(swank-loader:init)
(swank:create-server :dont-close t)
```

fails with

```
Condition of type: PROTOCOL-NOT-SUPPORTED-ERROR
Socket error in "socket": EPROTONOSUPPORT (Protocol not supported)

Available restarts:

1. (USE-VALUE) Try a port other than 4005
2. (RESTART-TOPLEVEL) Go back to Top-Level REPL.

Broken at SWANK/BACKEND:CREATE-SOCKET. In: #<process TOP-LEVEL>.
 File: #P"/data/data/com.termux/files/home/slime/swank/ecl.lisp" (Position #2099)

```

Trying to install Quicklisp:
```
cd /data/data/com.termux/files/home
curl -O https://beta.quicklisp.org/quicklisp.lisp
ecl -load quicklisp.lisp
(quicklisp-quickstart:install)
```

fails with
```
Condition of type: PROTOCOL-NOT-SUPPORTED-ERROR
Socket error in "socket": EPROTONOSUPPORT (Protocol not supported)

Available restarts:

1. (RESTART-TOPLEVEL) Go back to Top-Level REPL.

Broken at QLQS-NETWORK::%OPEN-CONNECTION. In: #<process TOP-LEVEL>.
 File: #P"/data/data/com.termux/files/home/quicklisp.lisp" (Position #11143)

```