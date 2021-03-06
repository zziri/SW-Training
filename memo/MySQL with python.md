
## MySQL 설치

https://dev.mysql.com/downloads/windows/installer/

## MySQL로 데이터베이스 만들기

- "MySQL Command Line Client"을 실행합니다
- 설치할 때 세팅했던 비밀번호를 입력합니다
- 현재 사용 가능한 database를 확인합니다
```bash
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sakila             |
| sys                |
| world              |
+--------------------+
6 rows in set (0.01 sec)
```
- db_test 라는 이름의 데이터베이스를 만듭니다
```bash
mysql> create database db_test
Query OK, 1 row affected (0.01 sec)
```
- db_test 데이터베이스로 전환
```bash
mysql> use db_test
Database changed
```

- 테이블 생성
```bash
mysql> CREATE TABLE dept(
    -> dept_no INT(11) unsigned NOT NULL,
    -> dept_name VARCHAR(35) NOT NULL,
    -> PRIMARY KEY (dept_no)
    -> );
Query OK, 0 rows affected, 1 warning (0.09 sec)
```

- insert tuple
```bash
mysql> INSERT INTO dept(dept_no, dept_name) VALUES('1', '개발팀');
Query OK, 1 row affected (0.07 sec)
mysql> INSERT INTO dept(dept_no, dept_name) VALUES('2', '품질팀');
Query OK, 1 row affected (0.07 sec)
```

## python code
- mysql python module 설치
```bash
pip install pymysql
```

- code 작성

db_test.py
```python

import pymysql

db = pymysql.connect(
    host="localhost",
    user='root',
    passwd='$password',
    db='db_test',
    charset='utf8'
)

cursor = db.cursor()
cursor.execute("SELECT * FROM dept;")

rows = cursor.fetchall()
print(rows)

db.commit()
db.close()
```

```bash
$ python db_test.py
((1, '개발팀'), (2, '품질팀'))
```

## 정리

- 데이터베이스를 만듭니다
```bash
mysql> create database $name
mysql> use $name
```

- 테이블을 만듭니다
```bash
mysql> CREATE TABLE dept($parameters);
```

- tuple을 insert합니다

```bash
mysql> INSERT INTO $table_name($parameters) VALUES($parameters);
```

- 데이터들을 가져옵니다

```bash
mysql> select * from dept;
```
