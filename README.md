Trying to install Quicklisp:
```
cd /data/data/com.termux/files/home
curl -O https://beta.quicklisp.org/quicklisp.lisp
export PATH=$PATH:/usr/local/bin
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