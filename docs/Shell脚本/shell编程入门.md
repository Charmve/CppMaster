# Shell 编程入门

- 菜鸟教程- https://www.runoob.com/linux/linux-shell.html
- Google Shell 风格指南 https://zh-google-styleguide.readthedocs.io/en/latest/google-shell-styleguide/contents/

案例：

```bash
[root@localhost ~]#name=dangxu       //定义一般变量  
[root@localhost ~]# echo ${name}  
dangxu  
[root@localhost ~]# cat test.sh      //验证脚本，实例化标题中的./*.sh  
#!/bin/sh  
echo ${name}  
[root@localhost ~]# ls -l test.sh    //验证脚本可执行  
-rwxr-xr-x 1 root root 23 Feb  6 11:09 test.sh  
[root@localhost ~]# ./test.sh        //以下三个命令证明了结论一  
  
[root@localhost ~]# sh ./test.sh  
  
[root@localhost ~]# bash ./test.sh  
  
[root@localhost ~]# . ./test.sh     //以下两个命令证明了结论二  
dangxu  
[root@localhost ~]# source ./test.sh  
dangxu  
[root@localhost ~]#  
```

总结：

1. shell 脚本各种执行方式（source ./*.sh, . ./*.sh, ./*.sh）的区别
  <table>
   <tbody>
     <tr>
      <td>
      </td>
       <td>
         ```./*.sh```
        <br>``sh ./*.sh``
        <br>``bash ./*.sh``
      </td>
      <td>
        ``source ./*.sh``
        <br>``. ./*.sh``
      </td>
     </tr>
     <tr>
      <td>
        是否需要执行权限
      </td>
      <td>
         只有`./*.sh`需要权限
      </td>
      <td>
        否
      </td>
    </tr>
    <tr>
      <td>
        是否创建子shell
      </td>
      <td>
         是，变量<b>不与</b>父shell环境交互
      </td>
      <td>
        否, 变量与父shell环境交互
      </td>
    </tr>
   </tbody>  
  </table>

2. 脚本的第一行固定为#!/bin/bash，表示用/bin/bash执行这个脚本
3. 脚本用chmod +x获得可执行权限后，可以用./脚本名.sh的方式执行

```bash
$ chmod +x test.sh
```


<br>

## 大纲

- Shell 变量
- Shell 传递参数
- Shell 数组
- Shell 运算符
- Shell echo命令
- Shell printf命令
- Shell test 命令
- Shell 流程控制
- Shell 函数
- Shell 输入/输出重定向
- Shell 文件包含
