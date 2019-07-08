How to install this in termux:
```
cd ~
wget http://github.com/plops/ecl-termux-binary/blob/master/dot_local.tar.gz?raw=true
tar xaf dot_local.tar.gz
wget http://beta.quicklisp.org/quicklisp.lisp
.local/bin/ecl --load quicklisp.org

(quicklisp-quickstart:install)
(ql:add-to-init-file)
(ql:quickload "quicklisp-slime-helper")
```

Then use an emacs configuration like dot_emacs in this repo



This is how I built the ECL binary on a Xiaomi 4c 2GB:
```
pkg install build-essential texinfo
cd ~
git clone https://gitlab.com/embeddable-common-lisp/ecl.git
# commit 06f0a93421b261aaa0fbfb2c9d077eebfc366280 Fri Jun 21 20:15:31 2019 +0200
cd ecl
/configure --prefix=$HOME/.local --build=aarch64-linux-android --enable-gmp=included
make -j6
make install 
cd ~
tar czf dot_local.tar.gz .local
```

Trying to start a swank server using quicklisp takes forever:

```
(ql:quickload :swank)
# the quickload takes forever :-(
(swank:create-server :dont-close t)

```

Note: The following is not really true anymore. Slime works fast enough. But I keep it because I might want to know how to set up Emacs with Tramp.

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

Configure ~/.ssh/config on laptop
```
Host termux localhost
    IdentityFile ~/.ssh/id_rsa_tree
    User martin
    Port 8022    
```



Open tunnel from laptop to tablet:
```
ssh -R 4005:localhost:4005 -i ~/.ssh/id_rsa_tree -p 8022 localhost
```

Link some files to /bin on tablet so that emacs TRAMP mode can use them
```
mkdir -p /usr/bin
ln -s /data/data/com.termux/files/usr/bin/applets/{ls,chown} /bin
```

On Laptop start emacs and connect to remote swank:
```
emacs
M-x slime-connect 127.0.0.1 4005

```

Configure TRAMP in  ~/.emacs on laptop 
```
(add-to-list 'slime-filename-translations
             (slime-create-filename-translator
	      :machine-instance "localhost" :remote-host "localhost" :username "martin"
	      ))

```

In emacs on laptop use TRAMP to open a remote file
```
C-x C-f /martin@localhost:/data/data/com.termux/files/home/bla.lisp
```
