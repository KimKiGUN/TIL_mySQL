>> ## 1. pymysql 모듈 이해 및 실습
***

>> ### 1.1 pymysql 라이브러리 소개 및 설치

- mysql을 python에서 사용할 수 있는 라이브러리
- 이 중에서 설치가 가장 쉬운 라이브러리
- pip install pymysql



### 일반적인 mysql 핸들링 코드 작성 순서

1. pymysql 모듈 import
2. pymysq.connect()메소드를 사용하여 MySQL에 연결
   - 호스트명, 포트, 로그인, 암호, 접속 DB 파라미터 지정
3. MYSQL 접속이 성공하면, Connection 객체로부터 cursor() 메서드를 호출하여 Cursor 객체를 가져온다.
4. Cursor 객체의 execute()메서드를 사용하여 SQL 문장을 DB 서버에 전송
5. SQL 쿼리의 경우 Cursor 객체의 fetchall(), fetchone(), fetchmany()등의 메서드를 사용하여 서버로부터 가져온 데이터를 코드에서 활용
6. 삽입, 갱신, 삭제 등의 DML 문장을 실행하는 경우, INSERT, UPDATE, DELETE 후 Connection 객체의 commit()메서드를 사용하여 데이터를 확정
7. Connection 객체의 close() 메서드를 사용하여 DB연결을 닫음


```python
! pip install pymysql
```

    Defaulting to user installation because normal site-packages is not writeable
    Requirement already satisfied: pymysql in c:\users\pc\appdata\roaming\python\python39\site-packages (1.0.2)
    


```python
import pymysql
```

pymysql.connect() 메소드를 사용하여 MySQL에 연결
- 호스트명, 포트, 로그인, 암호, 접속할 DB 등을 파라미터로 지정
- 주요 파라미터
    - host : 접속할 mysql server 주소
    - post : 접속할 mysql server의 포트 번호
    - user : mysql ID
    - passwd : mysql ID의 암호
    - db : 접속할 데이터베이스
    - charset = 'utf8' : mysql에서 select 하여 데이터를 가져올 때 한글이 깨질 수 있으므로 연결 설정에 넣어줌


```python
# dbms 연결코드 (connect)
db = pymysql.connect(host='localhost', port = 3306, user='root', password='password', charset = 'utf8')
```


```python
db
```




    <pymysql.connections.Connection at 0x163f35f7490>



- MySQl 접속이 성공하면, Connection 객체로부터 cursor() 메서드를 호출하여 Cursor 객체를 가져옴
- Cursor 객체의 execute() 메서드를 사용하여 SQL 문장을 DB 서버에 전송


- DB 생성

    1) cursor object 가져오기 : cursor = db.cursor()
    
    2) SQL 실행하기 : cursor.execute(SQL)
    
    3) 실행 mysql 서버에 확정 반영하기 : db.commit()


```python
cursor = db.cursor()
```


```python
sql = 'CREATE DATABASE IF NOT EXISTS ECOMMERCE'
cursor.execute(sql)
```




    1




```python
sql = 'show databases'
cursor.execute(sql)
result = cursor.fetchall()
result
```




    (('ecommerce',),
     ('exam',),
     ('information_schema',),
     ('my_emp',),
     ('my_emp02',),
     ('mysql',),
     ('performance_schema',),
     ('sakila',),
     ('students',),
     ('sys',),
     ('tabledb',),
     ('world',))




```python
# db 변경
sql = 'use ecommerce'
cursor.execute(sql)
```




    0




```python
# 현재 db 확인
sql = 'select database()'
cursor.execute(sql)
result = cursor.fetchone()
result
```




    ('ecommerce',)




```python
sql = """
      create table product
      (product_code varchar(20) not null,
       title varchar(200) not null,
       ori_price int,
       discount_price int,
       discount_percent int,
       delivery varchar(2),
       primary key(product_code)
       );
"""
```

SQL 실행 (cursor 객체의 execute() 메서드를 사용하여 INSERT, UPDATE 혹은 DELETE 문장을 DB 서버에 보냄) 


```python
cursor.execute(sql)
```




    0




```python
sql = 'show tables'
cursor.execute(sql)
result = cursor.fetchall()
result
```




    (('product',),)



- 삽입, 갱신, 삭제 등이 모두 끝났으면 connection 객체의 commit() 메서드를 사용하여 데이터를 commit


```python
db.close()
```
***


>> ### 1.2 패턴으로 익히는 pymysql



```python
# 1. 라이브러리 가져오기
import pymysql

# 2. 접속하기
db = pymysql.connect(host='localhost', port = 3306, user = 'root', passwd = 'password', db = 'ecommerce', charset = 'utf8')
```


```python
# 3. 커서 가져오기
cursor = db.cursor()
```


```python
# 4. sql 구문 만들기 (CRUD SQL 구문 등)
sql = """
    create table product2(
    product_code varchar(20) not null,
    title varchar(200) not null,
    ori_price int,
    discount_price int,
    discount_percent int,
    delivery varchar(2),
    primary key(product_code)
    );
"""
```


```python
# 5. sql 구문 실행하기

cursor.execute(sql)
```




    0




```python
# 6. DB에 Complete 하기
db.commit()
```


```python
# 7. DB 연결 닫기
db.close()
```

데이터 삽입(INSERT)
- CURSOR OBJECT 가져오기 : cursor = db.cursor()
- SQL 실행하기 : cursor.execute(SQL)
- 실행 mysql 서버에 확정 반영하기 : db.commit()


```python
# 1. 라이브러리 가져오기
import pymysql

# 2. 접속하기
db = pymysql.connect(host='localhost', port = 3306, user='root', passwd='password',db = 'ecommerce', charset='utf8')

```


```python
# 3. 커서 가져오기
cursor = db.cursor()
```


```python
for index in range(10):
    product_code = 216573140+index+1
    # print(product_code)
    sql = """INSERT INTO PRODUCT2 VALUES(
    '""" + str(product_code) + """', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');"""
    print(sql)
    cursor.execute(sql)
```

    INSERT INTO PRODUCT2 VALUES(
        '216573141', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    INSERT INTO PRODUCT2 VALUES(
        '216573142', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    INSERT INTO PRODUCT2 VALUES(
        '216573143', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    INSERT INTO PRODUCT2 VALUES(
        '216573144', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    INSERT INTO PRODUCT2 VALUES(
        '216573145', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    INSERT INTO PRODUCT2 VALUES(
        '216573146', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    INSERT INTO PRODUCT2 VALUES(
        '216573147', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    INSERT INTO PRODUCT2 VALUES(
        '216573148', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    INSERT INTO PRODUCT2 VALUES(
        '216573149', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    INSERT INTO PRODUCT2 VALUES(
        '216573150', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F');
    


```python
db.commit() # 입력된 데이터를 db 서버에 확정 시키기
```


```python
db.close()
```

데이터 조회(SELECT)
- cursor object 가져오기 : cursor = db.cursor()
- SQL 실행하기 : cursor.execute(SQL)
- mysql 서버로부터 데이터 가져오기 : fetch 메서드 사용
  - fetchall(): Fetch all the rows
  - fetchmany(size = None) : Fetch several rows
  - fetchone() : Fetch the next row


```python
import pymysql
```


```python
db = pymysql.connect(host='localhost', port = 3306, user='root', passwd='password',db = 'ecommerce', charset='utf8')
cursor = db.cursor()
```


```python
sql = 'select * from product2'
cursor.execute(sql)
```




    10




```python
result = cursor.fetchone() # 현재 커서를 다음 레코드로 이동시키고 해당 레코드를 반환
result
```




    ('216573141', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F')




```python
result = cursor.fetchall()
result
```




    (('216573142', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F'),
     ('216573143', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F'),
     ('216573144', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F'),
     ('216573145', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F'),
     ('216573146', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F'),
     ('216573147', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F'),
     ('216573148', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F'),
     ('216573149', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F'),
     ('216573150', '스위트바니 여름신상5900원~롱원피스티셔츠/긴팔/반팔', 23000, 6900, 70, 'F'))




```python
db.close()
```

데이터 수정(UPDATE)
- cursor object 가져오기 : cursor = db.cursor()
- SQL 실행하기 : cursor.execute(SQL)
- mysql 서버에 확정 반영하기 : db.commit()


```python
# 1. 라이브러리 가져오기
import pymysql

# 2. 접속하기
db = pymysql.connect(host='localhost', port = 3306, user='root', passwd='password',db = 'ecommerce', charset='utf8')

# 3. 커서 가져오기
cursor = db.cursor()
```


```python
# 4. SQL 구문 만들기
sql = """
update product2 set
title = '하늘하늘 원피스 썸머 스페셜 가디건',
ori_price = 33000,
discount_price = 9900,
discount_percent=70
where product_code = '216573141'
"""

# 5. sql 구문 실행하기
cursor.execute(sql)

# 6. commit 하기
db.commit()
```


```python
# 7. update 확인
sql = 'select * from product2 where product_code = 216573141'
cursor.execute(sql)
result = cursor.fetchone()
result
```




    ('216573141', '하늘하늘 원피스 썸머 스페셜 가디건', 33000, 9900, 70, 'F')




```python
db.close()
```

데이터 삭제(DELETE)
- cursor object 가져오기 : cursor = db.cursor()
- SQL 실행하기 : cursor.execute(SQL)
- mysql 서버에 확정 반영하기 : db.commit()


```python
import pymysql
db = pymysql.connect(host='localhost', port = 3306, user='root', passwd='password',db = 'ecommerce', charset='utf8')
cursor = db.cursor()
```


```python
sql = "delete from product where product_code ='216573141'"
cursor.execute(sql)
db.commit()
db.close()
```


```python
db = pymysql.connect(host='localhost', port = 3306, user='root', passwd='password',db = 'ecommerce', charset='utf8')

cursor = db.cursor()

sql = """select * from product where product_code = '216573141'"""

cursor.execute(sql)

result = cursor.fetchone()
print(result)
db.commit()
db.close()
```