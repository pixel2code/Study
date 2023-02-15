# Indexes

Indexes are a type of a look-up table where the database server can quickly look up rows in the database tables. Imagine a (technical) textbook which has the index at the end. This index contains keywords in that book and it tells you on which pages those keyword appear. It helps to find pages that contains a word `promise` instead of looking for each page one by one. Note that a keyword may appear on more than one pages.

In this case, you will see all pages on which this keyword appears. In a JavaScript book, the word `function` may appear on many pages while the word
`prototype chaining` may appear only once. In the index, you can quickly find on which page these words appear.

A primary key is always an index, but you can add other indexes to the table yourself if you know that you are going to do many queries using that column. This will speed up your querying, but be aware that adding indexes will slow down writing to the table. As every time a change is made it needs to update all of the indexes.

Have a look at the following video on indexes for a rundown of how this works and how you can add/remove indexes to a table:

<a href="https://www.youtube.com/watch?v=kSlS5WvHKd0">
<img src="https://via.placeholder.com/728x90.png?text=Video+Preview+Coming+Soon" alt="" />
</a>

To learn more about this topic, check out the following:

- [Indexes, when to use and when to avoid](https://levelup.gitconnected.com/indexes-when-to-use-and-when-to-avoid-in-sql-445ffae6b4a3)