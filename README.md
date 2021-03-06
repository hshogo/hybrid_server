#Hybrid Server
##How to install ex. Linux

- First, you should access "http://libevent.org/" and download source file(ex. libevent-2.0.22-stable.tar.gz) and you should execute following two commands.

```
./configure --prefix=/usr --disable-static && make
make install
```

- Second, you should execute "mkdir key" and execute following three commands in "key" direcotry, and then you could generate a key and self-signed cerificate.

```
openssl genrsa -out pkey 2048
openssl req -new -key pkey -out cert.req
openssl x509 -req -days 365 -in cert.req -signkey pkey -out cert
```

If you execute "make" and get error,"error: openssl/ssl.h: No such file or directory", you should execute following command

```
sudo apt-get install libssl-dev
```

- Third, you should execute "make"


##How to execute
You should execute ```./hybrid_server```

If you execute this and you get "bind() failed.(98) select() failed.",
you should execute following command.

```
ps aux | grep server
```

And you can see a list of "USER PID CPU MEM SIZE RSS TTY STAT TIME COMMAND".
You should check PID in a row of which COMMAND is "server"
and kill that PID, for example "kill 5032"


##Behavior
You access "https://127.0.0.1:5000" from address bar of your standard browser and browser displays index.html in the same directory server functions.

Also, you access "https://127.0.0.1:5000/sample/test.html" from address bar of your standard browser and browser displays test.html in sample directory under the same directory server functions.

If you access "http://127.0.0.1:5001/sample" from address bar of your standard browser and you redirect to "https://127.0.0.1:5000/sample"

(Caution : You should use different port or different host name between plain text URI and TLS URI)
