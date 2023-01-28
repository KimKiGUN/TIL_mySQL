## pandas 라이브러리와 pymysql

#### 1. read_sql()
- sql 연결객체를 활용하여 쿼리 구문으로 반환된 결과를 데이터프레임으로 바로 생성해주는 함수



```python
import pymysql
import pandas as pd
```


```python
host_name = 'localhost'
host_port = 3306
username = 'root'
password = 'password'
database_name = 'student_mgmt'
```


```python
# db  연결
db = pymysql.connect(
    host = host_name,
    port=host_port,
    user=username,
    passwd=password,
    db=database_name,
    charset='utf8'
)
```


```python
sql = 'show tables'
df = pd.read_sql(sql,db)
df
```

    C:\Anaconda3\lib\site-packages\pandas\io\sql.py:762: UserWarning: pandas only support SQLAlchemy connectable(engine/connection) ordatabase string URI or sqlite3 DBAPI2 connectionother DBAPI2 objects are not tested, please consider using SQLAlchemy
      warnings.warn(
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Tables_in_student_mgmt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>students</td>
    </tr>
  </tbody>
</table>
</div>




```python
sql = 'select * from students'
df = pd.read_sql(sql, db)
```

    C:\Anaconda3\lib\site-packages\pandas\io\sql.py:762: UserWarning: pandas only support SQLAlchemy connectable(engine/connection) ordatabase string URI or sqlite3 DBAPI2 connectionother DBAPI2 objects are not tested, please consider using SQLAlchemy
      warnings.warn(
    


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>NAME</th>
      <th>GENDER</th>
      <th>BIRTH</th>
      <th>ENGLISH</th>
      <th>MATH</th>
      <th>KOREAN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>minsun</td>
      <td>WOMAN</td>
      <td>1982-10-16</td>
      <td>30</td>
      <td>88</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>david</td>
      <td>MAN</td>
      <td>1982-12-10</td>
      <td>78</td>
      <td>77</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>david</td>
      <td>MAN</td>
      <td>1982-12-10</td>
      <td>78</td>
      <td>77</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>jade</td>
      <td>MAN</td>
      <td>1979-11-01</td>
      <td>45</td>
      <td>66</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>jane</td>
      <td>MAN</td>
      <td>1990-11-12</td>
      <td>65</td>
      <td>32</td>
      <td>90</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>wage</td>
      <td>WOMAN</td>
      <td>1982-01-13</td>
      <td>76</td>
      <td>30</td>
      <td>80</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>tina</td>
      <td>WOMAN</td>
      <td>1982-12-03</td>
      <td>87</td>
      <td>62</td>
      <td>71</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>dave</td>
      <td>MAN</td>
      <td>1983-07-16</td>
      <td>90</td>
      <td>80</td>
      <td>71</td>
    </tr>
  </tbody>
</table>
</div>




```python
type(df['MATH'][0]) # 테이블의 컬럼 형식을 그대로 유지
```




    numpy.int64




```python
df.to_csv('students.csv', sep = ',', index = False, encoding = 'utf-8')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>NAME</th>
      <th>GENDER</th>
      <th>BIRTH</th>
      <th>ENGLISH</th>
      <th>MATH</th>
      <th>KOREAN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>minsun</td>
      <td>WOMAN</td>
      <td>1982-10-16</td>
      <td>30</td>
      <td>88</td>
      <td>60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>david</td>
      <td>MAN</td>
      <td>1982-12-10</td>
      <td>78</td>
      <td>77</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>david</td>
      <td>MAN</td>
      <td>1982-12-10</td>
      <td>78</td>
      <td>77</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>jade</td>
      <td>MAN</td>
      <td>1979-11-01</td>
      <td>45</td>
      <td>66</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>jane</td>
      <td>MAN</td>
      <td>1990-11-12</td>
      <td>65</td>
      <td>32</td>
      <td>90</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>wage</td>
      <td>WOMAN</td>
      <td>1982-01-13</td>
      <td>76</td>
      <td>30</td>
      <td>80</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>tina</td>
      <td>WOMAN</td>
      <td>1982-12-03</td>
      <td>87</td>
      <td>62</td>
      <td>71</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>dave</td>
      <td>MAN</td>
      <td>1983-07-16</td>
      <td>90</td>
      <td>80</td>
      <td>71</td>
    </tr>
  </tbody>
</table>
</div>




```python
db.close()
```

### 외래키(Foreign Key)를 만드는 이유
- 두 테이블 사이에 관계를 선언해서 데이터의 무결성을 보장한다.


```python
import pymysql
import pandas as pd
```


```python
host_name = 'localhost'
host_port = 3306
username = 'root'
password = 'password'
database_name = 'sqlDB'
```


```python
# db  연결
db = pymysql.connect(
    host = host_name,
    port=host_port,
    user=username,
    passwd=password,
    db=database_name,
    charset='utf8'
)
```


```python
sql = 'select * from userTbl'
df = pd.read_sql(sql,db)
df
```

    C:\Anaconda3\lib\site-packages\pandas\io\sql.py:762: UserWarning: pandas only support SQLAlchemy connectable(engine/connection) ordatabase string URI or sqlite3 DBAPI2 connectionother DBAPI2 objects are not tested, please consider using SQLAlchemy
      warnings.warn(
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>userID</th>
      <th>name</th>
      <th>birthYear</th>
      <th>addr</th>
      <th>mobile1</th>
      <th>mobile2</th>
      <th>height</th>
      <th>mDate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>BBK</td>
      <td>바비킴</td>
      <td>1973</td>
      <td>서울</td>
      <td>010</td>
      <td>0000000</td>
      <td>176</td>
      <td>2013-05-05</td>
    </tr>
    <tr>
      <th>1</th>
      <td>EJW</td>
      <td>은지원</td>
      <td>1972</td>
      <td>경북</td>
      <td>011</td>
      <td>8888888</td>
      <td>174</td>
      <td>2014-03-03</td>
    </tr>
    <tr>
      <th>2</th>
      <td>JKW</td>
      <td>조관우</td>
      <td>1965</td>
      <td>경기</td>
      <td>018</td>
      <td>9999999</td>
      <td>172</td>
      <td>2010-10-10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>JYP</td>
      <td>조용필</td>
      <td>1950</td>
      <td>경기</td>
      <td>011</td>
      <td>4444444</td>
      <td>166</td>
      <td>2009-04-04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>KBS</td>
      <td>김범수</td>
      <td>1979</td>
      <td>경남</td>
      <td>011</td>
      <td>2222222</td>
      <td>173</td>
      <td>2012-04-04</td>
    </tr>
    <tr>
      <th>5</th>
      <td>KKH</td>
      <td>김경호</td>
      <td>1971</td>
      <td>전남</td>
      <td>019</td>
      <td>3333333</td>
      <td>177</td>
      <td>2007-07-07</td>
    </tr>
    <tr>
      <th>6</th>
      <td>LJB</td>
      <td>임재범</td>
      <td>1963</td>
      <td>서울</td>
      <td>016</td>
      <td>6666666</td>
      <td>182</td>
      <td>2009-09-09</td>
    </tr>
    <tr>
      <th>7</th>
      <td>LSG</td>
      <td>이승기</td>
      <td>1987</td>
      <td>서울</td>
      <td>011</td>
      <td>1111111</td>
      <td>182</td>
      <td>2008-08-08</td>
    </tr>
    <tr>
      <th>8</th>
      <td>SSK</td>
      <td>성시경</td>
      <td>1979</td>
      <td>서울</td>
      <td>None</td>
      <td>None</td>
      <td>186</td>
      <td>2013-12-12</td>
    </tr>
    <tr>
      <th>9</th>
      <td>YJS</td>
      <td>윤종신</td>
      <td>1969</td>
      <td>경남</td>
      <td>None</td>
      <td>None</td>
      <td>170</td>
      <td>2005-05-05</td>
    </tr>
  </tbody>
</table>
</div>




```python
sql = 'select * from buyTbl'
df = pd.read_sql(sql,db)
df
```

    C:\Anaconda3\lib\site-packages\pandas\io\sql.py:762: UserWarning: pandas only support SQLAlchemy connectable(engine/connection) ordatabase string URI or sqlite3 DBAPI2 connectionother DBAPI2 objects are not tested, please consider using SQLAlchemy
      warnings.warn(
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>num</th>
      <th>userID</th>
      <th>prodName</th>
      <th>groupName</th>
      <th>price</th>
      <th>amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>KBS</td>
      <td>운동화</td>
      <td>None</td>
      <td>30</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>KBS</td>
      <td>노트북</td>
      <td>전자</td>
      <td>1000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>JYP</td>
      <td>모니터</td>
      <td>전자</td>
      <td>200</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>BBK</td>
      <td>모니터</td>
      <td>전자</td>
      <td>200</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>KBS</td>
      <td>청바지</td>
      <td>의류</td>
      <td>50</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>BBK</td>
      <td>메모리</td>
      <td>전자</td>
      <td>80</td>
      <td>10</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>SSK</td>
      <td>책</td>
      <td>서적</td>
      <td>15</td>
      <td>5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>EJW</td>
      <td>책</td>
      <td>서적</td>
      <td>15</td>
      <td>2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>EJW</td>
      <td>청바지</td>
      <td>의류</td>
      <td>50</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>BBK</td>
      <td>운동화</td>
      <td>None</td>
      <td>30</td>
      <td>2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>EJW</td>
      <td>책</td>
      <td>서적</td>
      <td>15</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>BBK</td>
      <td>운동화</td>
      <td>None</td>
      <td>30</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



buyTbl에 데이터를 추가
- 외래키로 지정되어 있는 userid에 입력되는 새로운 값 STJ가 userTbl에 없는 값이기 때문에 무결성 오류 발생한다.


```python
cursor = db.cursor()
sql_query = "INSERT INTO buyTbl (userID, prodName, groupName, price, amount) VALUES('STJ', '운동화', '의류', 30, 2);"
cursor.execute(sql_query)
db.commit()
```


    ---------------------------------------------------------------------------

    IntegrityError                            Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_11512\1552227676.py in <module>
          1 cursor = db.cursor()
          2 sql_query = "INSERT INTO buyTbl (userID, prodName, groupName, price, amount) VALUES('STJ', '운동화', '의류', 30, 2);"
    ----> 3 cursor.execute(sql_query)
          4 db.commit()
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\cursors.py in execute(self, query, args)
        146         query = self.mogrify(query, args)
        147 
    --> 148         result = self._query(query)
        149         self._executed = query
        150         return result
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\cursors.py in _query(self, q)
        308         self._last_executed = q
        309         self._clear_result()
    --> 310         conn.query(q)
        311         self._do_get_result()
        312         return self.rowcount
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\connections.py in query(self, sql, unbuffered)
        546             sql = sql.encode(self.encoding, "surrogateescape")
        547         self._execute_command(COMMAND.COM_QUERY, sql)
    --> 548         self._affected_rows = self._read_query_result(unbuffered=unbuffered)
        549         return self._affected_rows
        550 
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\connections.py in _read_query_result(self, unbuffered)
        773         else:
        774             result = MySQLResult(self)
    --> 775             result.read()
        776         self._result = result
        777         if result.server_status is not None:
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\connections.py in read(self)
       1154     def read(self):
       1155         try:
    -> 1156             first_packet = self.connection._read_packet()
       1157 
       1158             if first_packet.is_ok_packet():
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\connections.py in _read_packet(self, packet_type)
        723             if self._result is not None and self._result.unbuffered_active is True:
        724                 self._result.unbuffered_active = False
    --> 725             packet.raise_for_error()
        726         return packet
        727 
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\protocol.py in raise_for_error(self)
        219         if DEBUG:
        220             print("errno =", errno)
    --> 221         err.raise_mysql_exception(self._data)
        222 
        223     def dump(self):
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\err.py in raise_mysql_exception(data)
        141     if errorclass is None:
        142         errorclass = InternalError if errno < 1000 else OperationalError
    --> 143     raise errorclass(errno, errval)
    

    IntegrityError: (1452, 'Cannot add or update a child row: a foreign key constraint fails (`sqldb`.`buytbl`, CONSTRAINT `buytbl_ibfk_1` FOREIGN KEY (`userID`) REFERENCES `usertbl` (`userID`))')


- usertbl에 userid가 STJ인 데이터가 없기 때문에 오류가 발생한다.
- buytbl 테이블의 userid 컬럼은 usertbl 테이블의 userid를 참조할 때, usertbl 테이블에 userid가 STJ인 데이터가 없으면 입력이 안 된다.
- 데이터의 무결성 : 두 테이블간 관계에 있어서, 데이터의 정확성을 보장하는 제약 조건을 넣는 것을 말한다.
- 현업에서는 꼭 필요한 경우만 사용하는 경우가 많음(비즈니스 로직이 다양하기 때문에, 제약을 걸어놓을 경우 예외적인 비즈니스 로직 처리가 어렵기 때문이다)


```python
db.close()
```


```python
# db 연결을 활성화 해주는 함수 구현
def conn(d_name):
    import pymysql
    host_name = 'localhost'
    host_port = 3306
    username = 'root'
    password = 'password'
    database_name = d_name
    db = pymysql.connect(
        host=host_name,
        port=host_port,
        user=username,
        passwd=password,
        db=database_name,
        charset='utf8'
    )
    return db
```


```python
db = conn('sqlDB')
```

이번에는 userTbl에 userID가 STJ 인 데이터를 넣어준 후에, 다시 buyTbl userID에 STJ 관련 데이터를 넣어줌


```python
cursor = db.cursor()
sql_query = "INSERT INTO userTbl VALUES('STJ', '서태지', 1975, '경기', '011', '00000000', 171, '2014-4-4');"
cursor.execute(sql_query)
db.commit()
```


```python
sql_query = "INSERT INTO buyTbl (userID, prodName, groupName, price, amount) VALUES('STJ', '운동화', '의류', 30, 2);"
cursor.execute(sql_query)
db.commit()
```

이번에는 userTbl에 userID가 STJ 관련 데이터를 삭제 해보자.

- buyTbl에 해당 userID를 참조하는 데이터가 있기 때문에 오류가 나야 정상이다.


```python
sql_query = "delete from userTbl where userID='STJ'"
cursor.execute(sql_query)
db.commit()
```


    ---------------------------------------------------------------------------

    IntegrityError                            Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_11512\2566689751.py in <module>
          1 sql_query = "delete from userTbl where userID='STJ'"
    ----> 2 cursor.execute(sql_query)
          3 db.commit()
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\cursors.py in execute(self, query, args)
        146         query = self.mogrify(query, args)
        147 
    --> 148         result = self._query(query)
        149         self._executed = query
        150         return result
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\cursors.py in _query(self, q)
        308         self._last_executed = q
        309         self._clear_result()
    --> 310         conn.query(q)
        311         self._do_get_result()
        312         return self.rowcount
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\connections.py in query(self, sql, unbuffered)
        546             sql = sql.encode(self.encoding, "surrogateescape")
        547         self._execute_command(COMMAND.COM_QUERY, sql)
    --> 548         self._affected_rows = self._read_query_result(unbuffered=unbuffered)
        549         return self._affected_rows
        550 
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\connections.py in _read_query_result(self, unbuffered)
        773         else:
        774             result = MySQLResult(self)
    --> 775             result.read()
        776         self._result = result
        777         if result.server_status is not None:
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\connections.py in read(self)
       1154     def read(self):
       1155         try:
    -> 1156             first_packet = self.connection._read_packet()
       1157 
       1158             if first_packet.is_ok_packet():
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\connections.py in _read_packet(self, packet_type)
        723             if self._result is not None and self._result.unbuffered_active is True:
        724                 self._result.unbuffered_active = False
    --> 725             packet.raise_for_error()
        726         return packet
        727 
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\protocol.py in raise_for_error(self)
        219         if DEBUG:
        220             print("errno =", errno)
    --> 221         err.raise_mysql_exception(self._data)
        222 
        223     def dump(self):
    

    ~\AppData\Roaming\Python\Python39\site-packages\pymysql\err.py in raise_mysql_exception(data)
        141     if errorclass is None:
        142         errorclass = InternalError if errno < 1000 else OperationalError
    --> 143     raise errorclass(errno, errval)
    

    IntegrityError: (1451, 'Cannot delete or update a parent row: a foreign key constraint fails (`sqldb`.`buytbl`, CONSTRAINT `buytbl_ibfk_1` FOREIGN KEY (`userID`) REFERENCES `usertbl` (`userID`))')

