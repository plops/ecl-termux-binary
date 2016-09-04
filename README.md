This is how I built the ECL binary:
```
cd ~/ecl
./configure --host=arm-linux-androideabi --with-system-gmp --enable-boehm=included  --with-cxx --with-dffi --enable-shared=no --disable-soname --prefix=/data/data/com.termux/files/usr/local --with-cross-config=`pwd`/src/util/android.cross_config
make -j4
make install
tar cf ~/ecl-16.1.2_termux.tar /data/data/com.termux/files/usr/local/
export PATH=$PATH:/data/data/com.termux/files/usr/local/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/data/data/com.termux/files/usr/local/lib

```

This is how you can install it in termux (assuming the tar file is in the termux home directory):

```
cd /data/com.termux/files/
tar xf /data/data/com.termux/files/home/ecl-16.1.2_termux.tar
export PATH=$PATH:/usr/local/bin
```

Install Quicklisp:
```
cd /data/data/com.termux/files/home
curl -O https://beta.quicklisp.org/quicklisp.lisp
ecl -load quicklisp.lisp
(quicklisp-quickstart:install)
(ql:add-to-init-file)
```
This adds some code in
/data/data/com.termux/files/home/.eclrc

Trying to start a swank server using quicklisp takes forever:

```
(ql:quickload :swank)
# the quickload takes forever :-(
(swank:create-server :dont-close t)

```


Instead I download slime and load it directly:

```
 cd slime/
-bash-4.3# ecl -load swank-loader.lisp 
;;; Loading "/data/data/com.termux/files/home/quicklisp/setup.lisp"
;;; Loading #P"/data/data/com.termux/files/usr/local/lib/ecl-16.1.2/asdf.fasc"
;;; Loading "/data/data/com.termux/files/home/slime/swank-loader.lisp"
ECL (Embeddable Common-Lisp) 16.1.2 (git:326829fd58b733f6f42e81f2e53a7b8c5860c7c5)
Copyright (C) 1984 Taiichi Yuasa and Masami Hagiya
Copyright (C) 1993 Giuseppe Attardi
Copyright (C) 2000 Juan J. Garcia-Ripoll
Copyright (C) 2015 Daniel Kochmanski
ECL is free software, and you are welcome to redistribute it
under certain conditions; see file 'Copyright' for details.
Type :h for Help.  
Top level in: #<process TOP-LEVEL>.
>  (swank-loader:init)
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-util.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-util.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-repl.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-repl.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-c-p-c.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-c-p-c.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-arglists.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-arglists.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-fuzzy.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-fuzzy.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-fancy-inspector.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-fancy-inspector.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-presentations.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-presentations.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-presentation-streams.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-presentation-streams.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-asdf.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-asdf.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-package-fu.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-package-fu.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-hyperdoc.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-hyperdoc.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-mrepl.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-mrepl.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-trace-dialog.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-trace-dialog.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-macrostep.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-macrostep.lisp>
;;; Compiling /data/data/com.termux/files/home/slime/contrib/swank-quicklisp.lisp
;;; Compiling #<input stream /data/data/com.termux/files/home/slime/contrib/swank-quicklisp.lisp>
NIL
> (swank:create-server :dont-close t)
;; Swank started at port: 4005.
```
