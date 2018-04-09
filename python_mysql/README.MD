
# 镜像封装了mysql 和python


```
mysql_init.sh echo "mysql init ok"
mysqld &
mysqladmin --silent --wait=30 ping || exit 1 

pytest
```