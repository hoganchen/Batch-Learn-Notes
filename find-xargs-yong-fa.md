Find xargs用法
```
由下结果可以看出，xargs是对find的每一条结果执行xargs后的命令，而不加xargs，则是对find的结果整体执行命令

$ grep python `find ./ -name *.bat` | wc -l
119
$ find ./ -name *.bat | xargs grep python | wc -l
119
$ find ./ -name *.bat | grep python | wc -l
0

```
