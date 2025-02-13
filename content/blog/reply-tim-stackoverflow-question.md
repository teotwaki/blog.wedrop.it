+++
title = "A reply for Tim's StackOverflow question"
date = "2015-08-25"
description = """An old Maemo friend reached out on Twitter and asked for help regarding some
issue he was running into using mysqli and PHP. Below is my response that I didn't have time to
post before the question was locked."""

[taxonomies]
tags = ["tech", "sql"]
+++

An old Maemo friend [reached out on Twitter][twitter] and asked for help regarding some issue he was
running into using mysqli and PHP. Below is my response that I didn't have time to post before [the
question][stackoverflow] was locked.

Hi Tim,

Looks like you've had a few issues here :). As a general rule, I like to go back to pure-MySQL, and
remove as much application logic as possible. In this case, as you've already discovered, it's
possible to do it all in MySQL.

But first, let's do part of what you forgot to do (and which is probably why you got downvoted a
bit): let's create a test MySQL table so we can run some queries on it:

```mysql
mysql> create table uploads (
    ->   af_uid int unsigned,
    ->   af_fid int unsigned,
    ->   af_dfilename varchar(100),
    ->   af_upload_date datetime
    -> );

mysql> insert into uploads values
    -> (101, 10, 'cat.jpg', '2015-08-16 14:42:46'),
    -> (101, 10, 'dog.jpg', '2015-08-16 14:43:01'),
    -> (101, 11, 'doc.pdf', '2015-08-16 14:44:23'),
    -> (101, 10, 'foo.jpg', '2015-08-16 14:45:00'),
    -> (101, 10, 'bar.jpg', '2015-08-16 14:45:36'),
    -> (101, 10, 'php.jpg', '2015-08-16 14:46:10'),
    -> (101, 10, 'mysql.jpg', '2015-08-16 14:46:52'),
    -> (102, 10, 'fubar.jpg', '2015-08-16 14:51:03');
```

From your question, there's 4 parts to the query you're trying to write:

- you only want `uid = 101`;
- you only want `fid = 10`;
- you want the 5 last items uploaded;
- you only want the 5 first results.

```mysql
mysql> select *
    -> from uploads
    -> where af_uid = 101
    -> and af_fid = 10
    -> order by af_upload_date desc
    -> limit 5;
+--------+--------+--------------+---------------------+
| af_uid | af_fid | af_dfilename | af_upload_date      |
+--------+--------+--------------+---------------------+
|    101 |     10 | mysql.jpg    | 2015-08-16 14:46:52 |
|    101 |     10 | php.jpg      | 2015-08-16 14:46:10 |
|    101 |     10 | bar.jpg      | 2015-08-16 14:45:36 |
|    101 |     10 | foo.jpg      | 2015-08-16 14:45:00 |
|    101 |     10 | dog.jpg      | 2015-08-16 14:43:01 |
+--------+--------+--------------+---------------------+
5 rows in set (0.01 sec)
```

I'm not seeing `limit` misbehaving here, as long as the rest of the query does what it's supposed to
do. A couple notes to keep in mind for the future, though:

Please don't put integer values in quotes. In SQL (and most other languages), there's no reason to
do so. You're just asking the system to do more casting and whatnot. Secondly, try to do most work
in MySQL, especially when it comes to filtering. Always try to reduce your dataset as much as
possible in the first step. There are certain situations where it can be useful to do some filtering
on the client side, but those are micro-optimisations that really only come in very later.

Anyway, now, let's dig in to the rest of your question and more specifically, let's try to figure
out what was going wrong. If we run your original query directly in MySQL, we'll notice that we get
interesting results:

```mysql
mysql> select *
    -> from uploads
    -> where af_uid = 101
    -> order by af_upload_date desc
    -> limit 5;
+--------+--------+--------------+---------------------+
| af_uid | af_fid | af_dfilename | af_upload_date      |
+--------+--------+--------------+---------------------+
|    101 |     10 | mysql.jpg    | 2015-08-16 14:46:52 |
|    101 |     10 | php.jpg      | 2015-08-16 14:46:10 |
|    101 |     10 | bar.jpg      | 2015-08-16 14:45:36 |
|    101 |     10 | foo.jpg      | 2015-08-16 14:45:00 |
|    101 |     11 | doc.pdf      | 2015-08-16 14:44:23 |
+--------+--------+--------------+---------------------+
5 rows in set (0.00 sec)
```

Notice that because of the order in which things appear in the table (due to the `order by` clause),
the last item actually has `af_fid = 11`.

Now, if on the client side, we apply extra filtering as you're doing with `if ($row['af_fid']) ==
10)`, it would only make sense that we end up with only 4 results.

I'm not sure why you saw 3 results, but I'm going to warrant a guess and say that it was due to some
differences in the code or data, compared to what you posted on SO. Conclusion: if you'd done all
your filtering in SQL from the get go, you most probably would've never hit this roadblock to start
with.

Feel free to ping me if you have other questions.

[twitter]: https://twitter.com/timsamoff/status/635230118160429056
[stackoverflow]: http://stackoverflow.com/questions/32161519/mysqli-limit-won-t-work-for-me
