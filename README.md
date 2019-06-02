#  opmorange
opm for orange 0.7    

# Usage:
1 git clone orange项目后，执行命令：
```
    cd orange
    opm --install-dir=./ get zhangbao0325/orangelib
```
2 当前目录下会生成一份lualib文件目录，里面是所有orange 0.7 版本所依赖的lua包    
3 修改conf/nginx.conf文件的lua_package_path如下：
```
 #----------------------------Orange configuration-----------------------------
 lua_package_path './lualib/?.lua;./lualib/resty/?.lua;../?.lua;/usr/local/lor/?.lua;;';
```
4 orange还依赖于luafilesystem和luasocket包，推荐用luarocks安装。

# Problem 
opm和luarocks安装过程中可能遇到的报错：      
1 Can't locate Digest/MD5.pm in @INC (@INC contains: /usr/local/lib64/perl5 /usr/local/share/perl5 /usr/lib64/perl5/vendor_perl /usr/share/perl5/vendor_perl /usr/lib64/perl5 /usr/share/perl5 .) at /home/openresty/bin/opm line 16.
  BEGIN failed--compilation aborted at /home/openresty/bin/opm line 16.
解决方法：
```
	yum -y install perl perl-devel
	yum -y install perl-Digest-MD5
```

2 /usr/bin/luarocks install luafilesystem      
Installing https://luarocks.org/luafilesystem-1.7.0-2.src.rock...    
Using https://luarocks.org/luafilesystem-1.7.0-2.src.rock... switching to 'build' mode    
gcc -O2 -fPIC -I/usr/include -c src/lfs.c -o src/lfs.o    
src/lfs.c:66:17: fatal error: lua.h: No such file or directory    
 #include <lua.h>    
                 ^    
compilation terminated.    

Error: Build error: Failed compiling object src/lfs.o    
解决方法：
```
# 删除原有的luarocks工具
# rpm -e luarocks --nodeps

执行find命令找到lua.h的路径：
# find / -name "lua.h"
/home/openresty/luajit/include/luajit-2.1/lua.h

源码安装luarocks
下载luarocks源码包，解压后安装
./configure --prefix=/usr/local/luarocks --with-lua-include=/home/openresty/luajit/include/luajit-2.1
make && make install
再执行luarocks install luafilesystem
```
