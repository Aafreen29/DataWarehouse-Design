# DataWarehouse-Design
It creates a schema design for the data warehouse that integrates the data sources, identify summarizability problems in the design, and populate data warehouse tables from sample rows in the data sources. 

<p>Mini case study contains two data sources with sample data along with a statement of business needs. Using the data sources and business needs, you will specify a dimensional model with dimensions, measures, and grain, create a schema design for the data warehouse that integrates the data sources, identify summarizability problems in the design, and populate data warehouse tables from sample rows in the data sources.</p>

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
