
# Common Table Expressions Lab

Common table expressions provide a temporary result set that can be used in a query.  They are useful for operating on table data then querying from that resulting information.  CTEs also can simplify the readability of complex SQL queries.  In this lab we will write several CTEs to calculate a dataset's average, then select the inputs that are above that average.  We will also use CTEs to delete duplicate rows from our table.

## Objectives

1.  Become comfortable writing common table expressions with the `WITH [CTE_name] AS ()` clause
2.  Write a CTE to calculate the average of a dataset and return the table inputs that are above that average
3.  Use a CTE to delete duplicate inputs from the table

## Record Store Sales Reprise

We will work from the same set of Records-R-Sweet store sales data from the Window Functions lab.  Recall that Records-R-Sweet had a store in five places: Manhattan, Brooklyn, Washington, Houston, and London.  What if Records-R-Sweet wishes to open a second store in London?  We cannot refer to London twice in our `sales` table, so we have replaced the "location" column with a "location_id" that refers to a separate `locations` table.  Each location now has a unique identifier, its id, and an address.  The two tables are featured below:

`locations`:

|city      |address         |
|----------|----------------|
|Manhattan |350 5th Avenue  |
|Brooklyn  |1904 Surf Avenue|
|Washington|2 15th St NW    |
|Houston   |3 NRG Pkwy      |
|London    |Fulham Rd SW6   |


`sales`:

|sale_id|date_of_sale|location_id|amount|
|-------|------------|-----------|------|
|1      |'2018-04-21'|1          |50    |
|2      |'2018-04-21'|1          |40    |
|3      |'2018-04-22'|1          |60    |
|4      |'2018-04-22'|1          |30    |
|5      |'2018-04-22'|1          |30    |
|6      |'2018-04-23'|1          |30    |
|7      |'2018-04-23'|1          |80    |
|8      |'2018-04-21'|2          |90    |
|9      |'2018-04-22'|2          |80    |
|10     |'2018-04-22'|2          |80    |
|11     |'2018-04-22'|2          |70    |
|12     |'2018-04-23'|2          |90    |
|13     |'2018-04-23'|2          |80    |
|14     |'2018-04-21'|3          |20    |
|15     |'2018-04-21'|3          |30    |
|16     |'2018-04-21'|3          |20    |
|17     |'2018-04-22'|3          |30    |
|18     |'2018-04-22'|3          |40    |
|19     |'2018-04-23'|3          |20    |
|20     |'2018-04-21'|4          |25    |
|21     |'2018-04-22'|4          |30    |
|22     |'2018-04-23'|4          |35    |
|23     |'2018-04-23'|4          |25    |
|24     |'2018-04-21'|5          |100   |
|25     |'2018-04-22'|5          |50    |
|26     |'2018-04-22'|5          |75    |
|27     |'2018-04-23'|5          |45    |
|8      |'2018-04-21'|2          |90    |
|8      |'2018-04-21'|2          |90    |
|8      |'2018-04-21'|2          |90    |
|16     |'2018-04-21'|3          |20    |
|24     |'2018-04-21'|5          |100   |
|24     |'2018-04-21'|5          |100   |
|24     |'2018-04-21'|5          |100   |


### Part 1 - Calculate the average

In the first part of the lab, write your queries inside the `part_1_ctes.py` file.  Your queries should be wrapped inside triple quotes so they can take up multiple lines.

* `use_cte_to_determine_average_sale`

First, write a CTE called `average_sales` that calculates the average sales amount across all locations and dates.  Select all columns (`*`) from the CTE.  This query returns the mean value.

* `select_all_above_average_sales`

Write the same CTE to calculate the `average_sales` number, but this time select only those rows that have an `amount` greater than this average value.

### Part 2 - Delete duplicates

Records-R-Sweet discovered a bug in its data entry program!  Several rows have been entered into the table multiple times by accident, so the queries from Part 1 might be calculating an incorrect average sale value.  In the `part_2_ctes.py` file, write a query that will delete these duplicate rows.

* `cte_deletes_duplicates`

Write a CTE that determines the MIN(id), aliased as `minimum_id`, for each `sale_id` from the table.  Then use the `DELETE FROM` clause to remove the rows with id values that are not found in the CTE.

* `correct_above_avg_sales`

Much like `select_all_above_average_sales` from Part 1, write a query that returns the above average sales.  However, it is difficult to remember which `location_id` matches with which city.  Add a join statement so that the query returns the city's name, the date of the sale, and the sales amount for only those above average sales.
