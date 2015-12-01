---
layout: post
title: "Sparksql: Adding new columns"
date: 2015-09-07 11:23:18 +0530
comments: true
published: false
categories: data
---

I had to spend quite a bit of last week trying to figure out how to migrate a SparkSQL table completely. Essentially we had to add a bunch of new columns to the existing table which contain a given default, and it ended up being a right pain despite the underlying conceptual simplicity. Basically, we had a few existing external tables with a timestamp partition, and we had to rename a bunch of columns, and add a few new columns. However, the new columns were not backed by the parquet files in HDFS, and so, any select/aggregation sort of query on top of those columns would wind up giving us NULL values. Those are not very useful for the new columns, and particularly bad for the old columns, since the old data is now hidden. For the new columns, we did consider repeatedly using `COALESCE(new_col, default_value)` to throw out a default value, but that was a pain for the analysts using the system.

So, the query flow is that the table metadata is essentially described in two places: one at the bin\_metatable table in the SparkSQL database and the second is at the data files themselves. The bin\_metadata table is an internal table, i.e, it is backed by vanilla sqldb, postgres or some such. The trouble now is that the two schemas should agree if we are to be able to use SQL commands to run spark jobs that can actually handle that data. Now, changing the metadata in SparkSQL is pretty simple, just fire a bunch of `alter table` commands at the interface. However, that will not touch the backing data, and since the schemas now differ, this is not very useful if we want to keep working with the old data. So the cure for that is to manually change the schemas of the underlying parquet data, and thereby getting it to play well with the new SparkSQL schemas.
