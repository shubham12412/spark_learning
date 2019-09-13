https://learning.oreilly.com/library/view/spark-the-definitive/9781491912201/ch05.html

Definitionally, a DataFrame consists of a series of records (like rows in a table), that are of type Row, and a number of columns (like columns in a spreadsheet) that represent a computation expression that can be performed on each individual record in the Dataset. Schemas define the name as well as the type of data in each column.

Partitioning of the DataFrame defines the layout of the DataFrame or Dataset’s physical distribution across the cluster. The partitioning scheme defines how that is allocated. You can set this to be based on values in a certain column or nondeterministically.


### Schemas
A schema defines the column names and types of a DataFrame. We can either let a data source define the schema (called schema-on-read) or we can define it explicitly ourselves.

If the types in the data (at runtime) do not match the schema, Spark will throw an error. 

### Columns and Expressions

To Spark, columns are logical constructions that simply represent a value computed on a per-record basis by means of an expression. This means that to have a real value for a column, we need to have a row; and to have a row, we need to have a DataFrame. You cannot manipulate an individual column outside the context of a DataFrame; you must use Spark transformations within a DataFrame to modify the contents of a column.


### Columns
There are a lot of different ways to construct and refer to columns but the two simplest ways are by using the col or column functions. To use either of these functions, you pass in a column name:

// in Scala
import org.apache.spark.sql.functions.{col, column}
col("someColumnName")
column("someColumnName")

As mentioned, this column might or might not exist in our DataFrames. Columns are not resolved until we compare the column names with those we are maintaining in the catalog. Column and table resolution happens in the analyzer phase

#### NOTE
We just mentioned two different ways of referring to columns. Scala has some unique language features that allow for more shorthand ways of referring to columns. The following bits of syntactic sugar perform the exact same thing, namely creating a column, but provide no performance improvement:

// in Scala
$"myColumn"
'myColumn

The $ allows us to designate a string as a special string that should refer to an expression. The tick mark (') is a special thing called a symbol; this is a Scala-specific construct of referring to some identifier. They both perform the same thing and are shorthand ways of referring to columns by name. You’ll likely see all of the aforementioned references when you read different people’s Spark code



### EXPLICIT COLUMN REFERENCES
If you need to refer to a specific DataFrame’s column, you can use the col method on the specific DataFrame. This can be useful when you are performing a join and need to refer to a specific column in one DataFrame that might share a name with another column in the joined DataFrame.

As an added benefit, Spark does not need to resolve this column itself (during the analyzer phase) because we did that for Spark

df.col("count")


### Expressions
We mentioned earlier that columns are expressions, but what is an expression? An expression is a set of transformations on one or more values in a record in a DataFrame. Think of it like a function that takes as input one or more column names, resolves them, and then potentially applies more expressions to create a single value for each record in the dataset. Importantly, this “single value” can actually be a complex type like a Map or Array.

In the simplest case, an expression, created via the expr function, is just a DataFrame column reference. In the simplest case, expr("someCol") is equivalent to col("someCol").

### COLUMNS AS EXPRESSIONS
Columns provide a subset of expression functionality. If you use col() and want to perform transformations on that column, you must perform those on that column reference. When using an expression, the expr function can actually parse transformations and column references from a string and can subsequently be passed into further transformations. Let’s look at some examples.

expr("someCol - 5") is the same transformation as performing col("someCol") - 5, or even expr("someCol") - 5. That’s because Spark compiles these to a logical tree specifying the order of operations. This might be a bit confusing at first, but remember a couple of key points:

Columns are just expressions.

Columns and transformations of those columns compile to the same logical plan as parsed expressions.

((col("someCol") + 5) * 200) - 6) < col("otherCol")


--------------------------------------------------------------------------------------------------------------

### Records and Rows
In Spark, each row in a DataFrame is a single record. Spark represents this record as an object of type Row. Spark manipulates Row objects using column expressions in order to produce usable values. Row objects internally represent arrays of bytes. The byte array interface is never shown to users because we only use column expressions to manipulate them.

### DataFrame Transformations



