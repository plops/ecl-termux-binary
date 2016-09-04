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

Now start a swank server:

```
(ql:quickload :swank)
(swank:create-server :dont-close t)

```
