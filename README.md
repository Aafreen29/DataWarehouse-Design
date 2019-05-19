# DataWarehouse-Design
It creates a schema design for the data warehouse that integrates the data sources, identify summarizability problems in the design, and populate data warehouse tables from sample rows in the data sources. 

<p>Mini case study contains two data sources with sample data along with a statement of business needs. Using the data sources and business needs, we will specify a dimensional model with dimensions, measures, and grain, create a schema design for the data warehouse that integrates the data sources, identify summarizability problems in the design, and populate data warehouse tables from sample rows in the data sources.</p>

<p><h4>First of all lets start with basics of Data Warehousing:</h4></p>

<h3>What is a Data Warehouse?</h3>
<p>A data warehouse is a relational database that is designed for query and analysis rather than for transaction processing. It usually contains historical data derived from transaction data, but it can include data from other sources. It separates analysis workload from transaction workload and enables an organization to consolidate data from several sources.<p>

<p>In addition to a relational database, a data warehouse environment includes an extraction, transportation, transformation, and loading (ETL) solution, an online analytical processing (OLAP) engine, client analysis tools, and other applications that manage the process of gathering data and delivering it to business users.</p>

<div>
  <img src= "https://imgur.com/cxrJ3LH.png", width="500px">
</div>

<h3>Difference between OLTP and OLAP systems</h3>
<p><b>OLTP (Online Transaction Processing):</b> It is used for handling transactions (SELECT,INSERT,UPDATE,DELETE). The primary objective is data processing and not data analysis. The main emphasis for OLTP systems is put on very fast query processing, maintaining data integrity in multi-access environments and an effectiveness measured by number of transactions per second. In OLTP database there is detailed and current data, and schema used to store transactional databases is the entity model (usually 3NF). <b>Databases</b> are modeled on the concept of <b>OLTP</b> </p>
<p><b>OLAP (Online Analytical Processing):</b> The primary objective is data retrieving and data analysis. It is basically an online database query answering system. In OLAP database there is aggregated, historical data, stored in multi-dimensional schemas (usually star schema). Sometime query need to access large amount of data in Management records. <b>Data Warehouse</b> is modeled n the concept of <b>OLAP</b></p>
<p>The following are some examples of differences between <b>data warehouse</b> and <b>OLTP systems</b></p>
<p>1> <b>Workload</b>:<br>
Data warehouses are designed to accommodate ad hoc queries. You might not know the workload of your data warehouse in advance, so a data warehouse should be optimized to perform well for a wide variety of possible query operations.<br>
OLTP systems support only predefined operations. Your applications might be specifically tuned or designed to support only these operations.<br>
  2><b>Data modifications</b>:<br>
A data warehouse is updated on a regular basis by the ETL process (run nightly or weekly) using bulk data modification techniques. The end users of a data warehouse do not directly update the data warehouse.<br>
In OLTP systems, end users routinely issue individual data modification statements to the database. The OLTP database is always up to date, and reflects the current state of each business transaction.<br>

3><b>Schema design</b>:<br>
Data warehouses often use denormalized or partially denormalized schemas (such as a star schema) to optimize query performance.<br>
OLTP systems often use fully normalized schemas to optimize update/insert/delete performance, and to guarantee data consistency.<br>

4><b>Typical operations</b>:<br>
A typical data warehouse query scans thousands or millions of rows. For example, "Find the total sales for all customers last month."<br>
A typical OLTP operation accesses only a handful of records. For example, "Retrieve the current order for this customer."<br>

5><b>Historical data</b>:<br>
Data warehouses usually store many months or years of data. This is to support historical analysis.<br>
OLTP systems usually store data from only a few weeks or months. The OLTP system stores only historical data as needed to successfully meet the requirements of the current transaction.</p>

<h3>OLAP Cube:</h3>
<div>
<img src= "https://imgur.com/YSJOnLA.png">
</div>
<p>At the core of the OLAP, concept is an <b>OLAP Cube</b>. <b>The OLAP cube is a data structure optimized for very quick data analysis.</b>
<br>
The OLAP Cube consists of numeric facts called measures which are categorized by dimensions. OLAP Cube is also called the <b>hypercube</b>.
<br>
Usually, data operations and analysis are performed using the simple spreadsheet, where data values are arranged in row and column format. This is ideal for two-dimensional data. However, OLAP contains <b>multidimensional data</b>, with data usually obtained from a different and unrelated source. Using a spreadsheet is not an optimal option. The cube can store and analyze multidimensional data in a logical and orderly manner. </p>

<h4>How does it work?</h4>
<p>A Data warehouse would extract information from multiple data sources and formats like text files, excel sheet, multimedia files, etc. </p>
<p>The extracted data is cleaned and transformed. Data is loaded into an OLAP server (or OLAP cube) where information is pre-calculated in advance for further analysis. </p>

<h3>Basic analytical operations of OLAP</h3>
<p>Four types of analytical operations in OLAP are:<br>
1>Roll-up <br>
2>Drill-down <br>
3>Slice and dice <br>
4>Pivot (rotate)</p>

<h4>Roll-up:</h4>
<p>Roll-up is also known as "consolidation" or "aggregation." The Roll-up operation can be performed in 2 ways:

1> Reducing dimensions <br>
2> Climbing up concept hierarchy. Concept hierarchy is a system of grouping things based on their order or level.

Consider the following diagram:</p>
<div>
  <img src="https://imgur.com/x8UhTD6.png", width= "400px">
</div>

<p> -In this example, cities New jersey and Lost Angles and rolled up into country USA. <br>
    -The sales figure of New Jersey and Los Angeles are 440 and 1560 respectively. They become 2000 after roll-up. <br>
    -In this aggregation process, data is location hierarchy moves up from city to the country.<br>
    -In the roll-up process at least one or more dimensions need to be removed. In this example, Quater dimension is removed. </p>
    
<h4>Drill-down</h4>
<p> In drill-down data is fragmented into smaller parts. It is the opposite of the rollup process. It can be done via

1> Moving down the concept hierarchy <br>
2> Increasing a dimension

Consider the following diagram:</p>
<div>
  <img src="https://imgur.com/75ntxb1.png", width= "500px">
</div>

<p> -Quater Q1 is drilled down to months January, February, and March. Corresponding sales are also registers.
    -In this example, dimension months are added. </p>

<h4>Slice</h4>
<p>Here, one dimension is selected, and a new sub-cube is created.<br>

Following diagram explain how slice operation performed: </p>
<div>
  <img src="https://imgur.com/BVzAuNU.png", width= "400px">
</div>

<p> -Dimension Time is Sliced with Q1 as the filter.
    -A new cube is created altogether. </p>
    
<h4>Dice</h4>
<p>This operation is similar to a slice. The difference in dice is you select 2 or more dimensions that result in the creation of a sub-cube. <br>
Consider the following diagram:
</p>
<div>
  <img src="https://imgur.com/UhoQ48n.png", width="400px">
  <div>

<h4>Pivot</h4>
<p>In Pivot, you rotate the data axes to provide a substitute presentation of data.<br>

In the following example, the pivot is based on item types. </p>

<div>
  <img src="https://imgur.com/jOyjIFu.png", width= "400px">
</div>

<h4>Dimensions</h4>
<p>The tables that describes the dimensions involved are called <b>Dimension tables</b><br>
Dividing a Data Warehouse project into dimensions provides structured information for analysis and reporting<br>
End users fire queries on these dimension tables which contain descriptive information</p>
<div>
  <img src="https://imgur.com/H4YwcfF.png">
</div>

<h4>Facts and Measures</h4>
<p>A <b>fact</b> is a measure that can be summed, averaged or manipulated<br>
A Fact table contain 2 kinds of data- a <b>dimension key</b> and a <b>measure</b><br>
Every dimension table is linked to a Fact table.</p>
<div>
<img src= "https://imgur.com/8kg3VTf.png">
</div>

<h4>Schemas</h4>
<p>A schema gives the logical description of the entire database<br>
It gives details about the constraints placed on the tables, key values present and how the key values are linked between the different tables<br>
  A <b>database</b> uses relational model, while a <b>datawarehouse</b> uses <b>Star</b>, <b>Snowflake</b>,and <b>Constellation</b> schema.</p>
