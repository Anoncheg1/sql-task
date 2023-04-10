
# Table of Contents

1.  [definition](#org3411953)
2.  [Solution 1 "CASE WHEN"](#org602a83a)
3.  [Solution 2 "CTE and subquery"](#org6c07e44)
4.  [Solution 3 Python](#org8b3be34)


<a id="org3411953"></a>

# definition

MySQL

tables:

1.  clients\_table
    -   client\_id
    -   gender
2.  loans\_table (docs)
    -   loan\_id
    -   client\_id
    -   loan\_date

Task to select count of first, second, thirst counts of loans in october of 2022

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">&#xa0;</th>
<th scope="col" class="org-left">count of first docs</th>
<th scope="col" class="org-left">count of second docs</th>
</tr>


<tr>
<th scope="col" class="org-left">&#xa0;</th>
<th scope="col" class="org-left">in october of 2022</th>
<th scope="col" class="org-left">in october of 2022</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">male</td>
<td class="org-left">?</td>
<td class="org-left">&#xa0;</td>
</tr>


<tr>
<td class="org-left">female</td>
<td class="org-left">?</td>
<td class="org-left">&#xa0;</td>
</tr>
</tbody>
</table>

    -- DROP TABLE clients_table;

    CREATE TABLE clients_table (
    client_id INTEGER PRIMARY KEY,
    gender VARCHAR(10)
    );

    INSERT INTO clients_table VALUES(NULL, 'male');
    INSERT INTO clients_table VALUES(NULL, 'male');
    INSERT INTO clients_table VALUES(NULL, 'female');
    INSERT INTO clients_table VALUES(NULL, 'male');
    INSERT INTO clients_table VALUES(NULL, 'female');

    SELECT * FROM clients_table;

*results*: create client\_table

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">client_id</th>
<th scope="col" class="org-left">gender</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">1</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">2</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">3</td>
<td class="org-left">female</td>
</tr>


<tr>
<td class="org-right">4</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">5</td>
<td class="org-left">female</td>
</tr>
</tbody>
</table>

    -- DROP TABLE loans_table;

    CREATE TABLE loans_table (
    loan_id INTEGER PRIMARY KEY,
    client_id INTEGER,
    loan_date DATE
    );

    INSERT INTO loans_table VALUES(NULL, 1, '2022-10-01');
    INSERT INTO loans_table VALUES(NULL, 2, '2022-10-02');
    INSERT INTO loans_table VALUES(NULL, 2, '2022-10-09');
    INSERT INTO loans_table VALUES(NULL, 2, '2022-10-11');
    INSERT INTO loans_table VALUES(NULL, 2, '2022-10-12');
    INSERT INTO loans_table VALUES(NULL, 2, '2022-10-13');
    INSERT INTO loans_table VALUES(NULL, 3, '2022-10-02');
    INSERT INTO loans_table VALUES(NULL, 3, '2022-10-03');
    INSERT INTO loans_table VALUES(NULL, 3, '2022-10-04');
    INSERT INTO loans_table VALUES(NULL, 4, '2022-10-04');
    INSERT INTO loans_table VALUES(NULL, 4, '2022-10-08');
    INSERT INTO loans_table VALUES(NULL, 5, '2023-10-08');

    SELECT * FROM loans_table;

*results*: create loans\_table

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-right" />

<col  class="org-right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">loan_id</th>
<th scope="col" class="org-right">client_id</th>
<th scope="col" class="org-right">loan_date</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">1</td>
<td class="org-right">1</td>
<td class="org-right">2022-10-01</td>
</tr>


<tr>
<td class="org-right">2</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-02</td>
</tr>


<tr>
<td class="org-right">3</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-09</td>
</tr>


<tr>
<td class="org-right">4</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-11</td>
</tr>


<tr>
<td class="org-right">5</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-12</td>
</tr>


<tr>
<td class="org-right">6</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-13</td>
</tr>


<tr>
<td class="org-right">7</td>
<td class="org-right">3</td>
<td class="org-right">2022-10-02</td>
</tr>


<tr>
<td class="org-right">8</td>
<td class="org-right">3</td>
<td class="org-right">2022-10-03</td>
</tr>


<tr>
<td class="org-right">9</td>
<td class="org-right">3</td>
<td class="org-right">2022-10-04</td>
</tr>


<tr>
<td class="org-right">10</td>
<td class="org-right">4</td>
<td class="org-right">2022-10-04</td>
</tr>


<tr>
<td class="org-right">11</td>
<td class="org-right">4</td>
<td class="org-right">2022-10-08</td>
</tr>


<tr>
<td class="org-right">12</td>
<td class="org-right">5</td>
<td class="org-right">2023-10-08</td>
</tr>
</tbody>
</table>

    SELECT * from loans_table as l
    LEFT JOIN clients_table as c ON l.client_id = c.client_id
    WHERE l.loan_date BETWEEN '2022-10-01' AND '2022-11-01'
    ;
    -- select NULL;

*results*: step 1: select subspace

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-right" />

<col  class="org-right" />

<col  class="org-right" />

<col  class="org-right" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-right">loan_id</th>
<th scope="col" class="org-right">client_id</th>
<th scope="col" class="org-right">loan_date</th>
<th scope="col" class="org-right">client_id</th>
<th scope="col" class="org-left">gender</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-right">1</td>
<td class="org-right">1</td>
<td class="org-right">2022-10-01</td>
<td class="org-right">1</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">2</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-02</td>
<td class="org-right">2</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">3</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-09</td>
<td class="org-right">2</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">4</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-11</td>
<td class="org-right">2</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">5</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-12</td>
<td class="org-right">2</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">6</td>
<td class="org-right">2</td>
<td class="org-right">2022-10-13</td>
<td class="org-right">2</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">7</td>
<td class="org-right">3</td>
<td class="org-right">2022-10-02</td>
<td class="org-right">3</td>
<td class="org-left">female</td>
</tr>


<tr>
<td class="org-right">8</td>
<td class="org-right">3</td>
<td class="org-right">2022-10-03</td>
<td class="org-right">3</td>
<td class="org-left">female</td>
</tr>


<tr>
<td class="org-right">9</td>
<td class="org-right">3</td>
<td class="org-right">2022-10-04</td>
<td class="org-right">3</td>
<td class="org-left">female</td>
</tr>


<tr>
<td class="org-right">10</td>
<td class="org-right">4</td>
<td class="org-right">2022-10-04</td>
<td class="org-right">4</td>
<td class="org-left">male</td>
</tr>


<tr>
<td class="org-right">11</td>
<td class="org-right">4</td>
<td class="org-right">2022-10-08</td>
<td class="org-right">4</td>
<td class="org-left">male</td>
</tr>
</tbody>
</table>


<a id="org602a83a"></a>

# Solution 1 "CASE WHEN"

    SELECT c.gender, COUNT(l.client_id) lc, l.client_id from loans_table as l
    LEFT JOIN clients_table as c ON l.client_id = c.client_id
    WHERE l.loan_date BETWEEN '2022-10-01' AND '2022-11-01'
    GROUP BY gender, l.client_id;
    select NULL;

*results*: preparation

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-right" />

<col  class="org-right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">gender</th>
<th scope="col" class="org-right">lc</th>
<th scope="col" class="org-right">client_id</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">female</td>
<td class="org-right">3</td>
<td class="org-right">3</td>
</tr>


<tr>
<td class="org-left">male</td>
<td class="org-right">1</td>
<td class="org-right">1</td>
</tr>


<tr>
<td class="org-left">male</td>
<td class="org-right">5</td>
<td class="org-right">2</td>
</tr>


<tr>
<td class="org-left">male</td>
<td class="org-right">2</td>
<td class="org-right">4</td>
</tr>


<tr>
<td class="org-left">NULL</td>
<td class="org-right">&#xa0;</td>
<td class="org-right">&#xa0;</td>
</tr>
</tbody>
</table>

    select fff.gender,
    SUM(case when lc > 0 then 1 else 0 end) c_first_202210,
    SUM(case when lc > 1 then 1 else 0 end) c_second_202210,
    SUM(case when lc > 2 then 1 else 0 end) c_third_202210,
    SUM(case when lc > 3 then 1 else 0 end) c_forth_202210
    from
    ( SELECT c.gender, COUNT(l.client_id) lc, l.client_id from loans_table as l
    LEFT JOIN clients_table as c ON l.client_id = c.client_id
    WHERE l.loan_date BETWEEN '2022-10-01' AND '2022-11-01'
    GROUP BY gender, l.client_id) as fff
    group by gender;

*results*: select count of first, second, thirst counts of loans in october of 2022 -  SQL 'case when' solution

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-right" />

<col  class="org-right" />

<col  class="org-right" />

<col  class="org-right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">gender</th>
<th scope="col" class="org-right">c_first_202210</th>
<th scope="col" class="org-right">c_second_202210</th>
<th scope="col" class="org-right">c_third_202210</th>
<th scope="col" class="org-right">c_forth_202210</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">female</td>
<td class="org-right">1</td>
<td class="org-right">1</td>
<td class="org-right">1</td>
<td class="org-right">0</td>
</tr>


<tr>
<td class="org-left">male</td>
<td class="org-right">3</td>
<td class="org-right">2</td>
<td class="org-right">1</td>
<td class="org-right">1</td>
</tr>
</tbody>
</table>


<a id="org6c07e44"></a>

# Solution 2 "CTE and subquery"

    WITH RECURSIVE  cte_pre AS (
    SELECT * from loans_table as l
    LEFT JOIN clients_table as c ON l.client_id = c.client_id
    WHERE l.loan_date BETWEEN '2022-10-01' AND '2022-11-01'
    ), cte_first AS (
      SELECT gender, COUNT(*) cc FROM (
        SELECT COUNT(*) fc, gender from cte_pre
        GROUP BY client_id
      --HAVING fc >=1
      )
      GROUP BY gender

    ), cte_second AS (
      SELECT gender, COUNT(*) cc FROM (
        SELECT COUNT(*) fc, gender from cte_pre
        GROUP BY client_id
        HAVING fc >=2
      )
      GROUP BY gender

    ), cte_third AS (
      SELECT gender, COUNT(*) cc FROM (
        SELECT COUNT(*) fc, gender from cte_pre
        GROUP BY client_id
        HAVING fc >=3
      )
      GROUP BY gender

    )
    select cf1.gender, cf1.cc c_first_202210, cf2.cc c_second_202210, cf3.cc c_third_202210 from cte_first cf1
    JOIN cte_second cf2 ON cf1.gender = cf2.gender
    JOIN cte_third cf3 ON cf1.gender = cf3.gender

    ;

*results*: select count of first, second, thirst counts of loans in october of 2022 -  SQL 'CTE' solution

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-right" />

<col  class="org-right" />

<col  class="org-right" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">gender</th>
<th scope="col" class="org-right">c_first_202210</th>
<th scope="col" class="org-right">c_second_202210</th>
<th scope="col" class="org-right">c_third_202210</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">female</td>
<td class="org-right">1</td>
<td class="org-right">1</td>
<td class="org-right">1</td>
</tr>


<tr>
<td class="org-left">male</td>
<td class="org-right">3</td>
<td class="org-right">2</td>
<td class="org-right">1</td>
</tr>
</tbody>
</table>


<a id="org8b3be34"></a>

# Solution 3 Python

    import pandas as pd
    import sqlite3
    con = sqlite3.connect("/tmp/test-sqlite.db")
    cur = con.cursor()
    res = cur.execute("""SELECT * from loans_table as l
    LEFT JOIN clients_table as c ON l.client_id = c.client_id
    WHERE l.loan_date BETWEEN '2022-10-01' AND '2022-11-01'
    ;""")
    # print(cur.description())
    # print(len(cur))
    a = res.fetchall()
    field_names = [x[0] for x in cur.description]
    # print(field_names)

    df = pd.DataFrame(a, columns = ['loan_id', 'client_id1', 'loan_date', 'client_id2', 'gender'])
    # print(df)
    # print()
    # for x in df:
    #     first = 0
    v = df.groupby(['gender', 'client_id1'],as_index=False).count()
    # v.groupby('gender').
    male = v[v['gender'] == 'male']
    female = v[v['gender'] == 'female']

    res_male = []
    res_female = []
    for i, c in enumerate(['first', 'second', 'third']):
        rm = (v[v['gender'] == 'male']['loan_id'] >= i).sum()
        rf = (v[v['gender'] == 'female']['loan_id'] >= i).sum()
        res_male.append(rm)
        res_female.append(rf)


    print('female', res_female)
    print('male', res_male)

*results*:

    female [1, 1, 1]
    male [3, 3, 2]
