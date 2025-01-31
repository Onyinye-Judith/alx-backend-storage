MySQL Performance: How To Leverage MySQL Database Indexing
Justin Palmer
Tutorials
A Mysql Indexing Logo
Throughout this tutorial, we will cover some of the fundamentals of indexing. As part of the MySQL series, we will introduce capabilities of MySQL indexing and the role it plays in optimizing database performance. Liquid Web recommends consulting with a DBA before making any changes to your production level application.



What is Indexing?
Indexing is a powerful structure in MySQL which can be leveraged to get the fastest response times from common queries. MySQL queries achieve efficiency by generating a smaller table, called an index, from a specified column or set of columns. These columns, called a key, can be used to enforce uniqueness. Below is a simple visualization of an example index using two columns as a key.

+------+----------+----------+
| ROW | COLUMN_1 | COLUMN_2 |
+------+----------+----------+
| 1 | data1 | data2 |
+------+----------+----------+
| 2 | data1 | data1 |
+------+----------+----------+
| 3 | data1 | data1 |
+------+----------+----------+
| 4 | data1 | data1 |
+------+----------+----------+
| 5 | data1 | data1 |
+------+----------+----------+

This analogy compares MySQL indexing to indexing in the back of a book.
Queries utilize indexes to identify and retrieve the targeted data, even if they are a combination of keys. Without an index, running that same query results in an inspection of every row for the needed data. Indexing produces a shortcut, with much faster query times on expansive tables. A textbooks analogy may provide another common way to visualize how indexes function.

When to Enable Indexing?
Indexing is only advantageous for huge tables with regularly accessed information. For instance, to continue with our textbook analogy, it makes little sense to index a children’s storybook with only a dozen pages. It’s more efficient to simply read the book to find each occurrence of the word “turtle” than it would be to set up and maintain indexes, query for those indexes, and then review each page provided. In the computing world, those extra tasks surrounding indexing represent wasted resources which would be better purposed by not indexing.

Without indexes, when tables grow to enormous proportions, response times suffer from queries targeting those obtuse tables. Inefficient queries manifest into latency within application or website performance. We commonly identify this latency by using the MySQL slow query log feature. You can find more details about using the slow query log feature in the first article in this series: MySQL Performance: Identifying Long Queries.
Once a colossal table hits its tipping point, it reaches the potential for downtime for applications and websites. Conducting routine evaluations for growing database establishes optimal database performance and sidesteps long queries’ inherent interruptions.

MySQL Indexing Pros vs. Cons
There are benefits and downsides to using MySQL indexing, and we’ll discuss the significant pros and cons for your consideration. These aspects will guide you to decide whether indexing is an appropriate choice for your situation.

quick data transmissions and ideal for OLAP.
What Information Does One Index?
Selecting what to index is probably the most challenging part to indexing your databases. Determining what is important enough to index and what is benign enough to not index. Generally speaking, indexing works best on those columns that are the subject of the WHERE clauses in your commonly executed queries. Consider the following simplified table:

ID, TITLE, LAST_NAME, FIRST_NAME, MAIDEN_NAME, DOB, GENDER, AGE, DESCRIPTION, HISTORY, ETC...

If your queries rely on testing the WHERE clause using LAST_NAME and FIRST_NAME then indexing by these two columns would significantly increase query response times. Alternately, if your queries rely on a simple ID lookup, indexing by ID would be the better choice.

These examples are merely a rudimentary example, and there are several types of indexing structures built-in to MySQL. The following MySQL page discusses these types of indexes in greater detail, and a recommended read for anyone considering indexing: How MySQL Uses Indexes

What is a Unique Index?

Another point for consideration when evaluating which columns to serve as the key in your index is whether to use the UNIQUE constraint. Setting the UNIQUE constraint will enforce uniqueness based on the configured indexing key. As with any key, this can be a single column or a concatenation of multiple columns. The function of this constraint ensures that there are no duplicate entries in the table based on the configured key.

UNIQUE constraints increase write speeds, a taxation of implementation.
What is a Primary Key Index?

As commonly invoked as the UNIQUE constraint the PRIMARY KEY is used to optimize indexes. This constraint ensures that the designated PRIMARY KEY cannot be of a null value. As a result, a performance boost occurs when running on an InnoDB storage engine for the table in question. This boost is due to how InnoDB physically stores data, placing null valued rows in the key out of contiguous sequence with rows that have values. Enabling this constraint ensures the rows of the table are kept in contiguous order for quicker responses.

Primary Key Index is absolutely necessary for large tables.
