#  opmorange
opm for orange 0.7

Usage:
    1 git clone orange项目后，执行命令：
    ```
        cd orange
        opm get zhangbao0325/opmorange
    ```
    2 当前目录下会生成一份lualib文件目录，里面是所有orange 0.7 版本所依赖的lua包
    3 修改conf/nginx.conf文件的lua_package_path如下：
    ```
     #----------------------------Orange configuration-----------------------------
      lua_package_path './lualib/?.lua;./lualib/resty/?.lua;../?.lua;/usr/local/lor/?.lua;;';
    ```
