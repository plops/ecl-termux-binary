
```
su
cd /
tar xf /data/data/com.termux/files/home/ecl-16.1.2_termux.tar
export PATH=$PATH:/usr/local/bin
```

Trying to install slime:

```
apt install emacs
git clone https://github.com/slime/slime
cd slime
ecl -load swank-loader
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