---
layout: post
title: Relational Database Design and Implementation
---

MKN2 Task 1: Relational Database Design and Implementation Submission 2


MKN2 Task 1: Relational Database Design and Implementation
Part 1: Design Document
A. Scenario: EcoMart Online Marketplace (D597 Scenario 2)
Company Overview
Modern organizations rely on accurate, well-structured data to make informed decisions, streamline operations, and support long-term growth. This paper outlines the design and implementation of a scalable database solution that addresses EcoMart’s business needs. It covers identifying the core business problem, developing a logical data model, creating a clean, optimized schema, and applying performance and integrity enhancements. Together, these components demonstrate how a well-designed database can support operational efficiency and data-driven decision-making within a growing e-commerce environment.

EcoMart is an emerging online marketplace specializing in sustainable and eco-friendly consumer goods. The platform connects environmentally conscious shoppers with ethically sourced products across categories such as groceries, apparel, home goods, and personal care. As the company grows, EcoMart aims to expand its catalog and further strengthen its role as a trusted destination for products aligned with sustainable values. 
How EcoMart’s Data is Managed Today
EcoMart currently manages its operational data using a single flat CSV file derived from the original Excel dataset. While this file provides a snapshot of historical sales activity, it lacks the structure and depth required to support the operational needs of a growing e commerce marketplace. The dataset includes basic transactional attributes—such as region, country, item type, sales channel, order priority, dates, and pricing—but it does not contain the broader set of entities needed to run EcoMart’s business model. 
Malik, Goldwasser, and Johnston explain that although spreadsheets (the original form of EcoMart’s dataset was given in an Excel .xlsx file and converted for SQL functions) can organize data in tables, they lack essential database capabilities. Spreadsheets do not provide built in metadata, enforce data types or valid value ranges, define relationships between tables, or apply constraints that maintain consistency across related data. They also note that most users are not trained to recognize these limitations, which makes spreadsheets unsuitable for tasks that require reliable data management. (Malik, Goldwasser, and Johnston, 2019).
Flat File Before Snapshot:
Region	Country	Item Type	Sales Channel	Order Priority	Order Date
Middle East and North Africa	Azerbaijan	Snacks	Online	C	10/8/14
Central America and the Caribbean	Panama	Cosmetics	Offline	L	2/22/15
Sub-Saharan Africa	Sao Tome and Principe	Fruits	Offline	M	12/9/15
Figure 1.

Why EcoMart’s Design Fails
Because the file is flat and denormalized, descriptive values are repeated in every row, creating redundancy and the risk of inconsistency. The dataset contains no primary keys, foreign keys, or constraints, making it impossible to enforce data validation or maintain referential integrity. Derived values such as total revenue and total profit are stored directly in the file, violating normalization principles and introducing the risk of data mismatches if the underlying values change.
More importantly, the dataset represents only past orders. It does not include essential operational information such as inventory levels, sustainability certifications, customer accounts, supplier relationships, fulfillment workflows, or security controls. As EcoMart expands its product catalog and sustainability initiatives, these limitations become increasingly restrictive. The flat file approach cannot scale to support additional products, vendors, certifications, or concurrent access, nor can it answer key business questions about product performance, profitability, or shipping efficiency.
1. EcoMart’s Core Business Problems
Problem 1: EcoMart cannot manage diverse, rapidly growing product data in its current structure. EcoMart sells eco-friendly products across groceries, apparel, home goods, personal care, and more. Each product has different attributes—pricing, availability, sustainability certifications, descriptions, and user reviews.
Business problem: Their existing data setup cannot scale or adapt to this level of complexity, leading to inconsistencies, duplication, and difficulty adding new product types.
Problem 2: EcoMart needs a scalable, high-performance system to support increasing traffic and data volume. As the marketplace grows, more customers, more products, and more transactions strain the system.
Business problem: Without a well-designed relational model and performance optimization, the platform risks slow queries, poor user experience, and inability to scale.
Problem 3: EcoMart must protect sensitive customer and business data. They handle customer information, order data, and sustainability certifications.
Business problem: Their current system lacks strong security controls—encryption, access management, and audit logging—putting them at risk of data breaches and non-compliance with privacy regulations.
Problem 4: EcoMart lacks monitoring and maintenance processes to ensure long-term stability. As the platform grows, performance bottlenecks, data inconsistencies, and security vulnerabilities become more likely.
Business problem: Without proactive monitoring, the system could degrade over time, leading to downtime, corrupted data, or security incidents.
EcoMart’s business problems center on managing complex product data, scaling their platform for growth, securing sensitive information, and implementing monitoring processes to maintain long-term performance and reliability.
a. Database Structure:
To address these challenges, EcoMart requires a structured, scalable data foundation. The proposed data structure for EcoMart is a normalized relational OLTP (Entity Relationship Model). A relational star schema uses fact and dimension tables, with primary and foreign keys, to establish relationships (Smallcombe, 2023). The database will be normalized to 3rd Normal Form (3NF). 

EcoMart’s transactional workload has real-time operational data, high-frequency transactions, and focuses on data consistency and data integrity, necessitating an online transaction processing (OLTP) database system (WGU, 3.1.3).  Transactional databases support Ecomart’s needs for transactions to be atomic, consistent, isolated, and durable (ACID) to ensure data validity even in the face of failures (Microsoft, 2025). The conceptual model behind the relational schema is the Entity-Relationship model, which is based on entities, attributes, and relationships (Coronel & Morris, 2023).

EcoMart’s relational data structure will be implemented via PostgreSQL 16.2 on the local host (port 5432), which will ensure data integrity and efficient retrieval, and define how the system will be implemented (WGU, 4.1.1). PostgreSQL is ideal for handling EcoMart’s business problem and data structure as it excels in environments where scalability and reliability are critical (geeksforgeeks.org, 2025, Sep 27).

Identify Entities
Entity 	Purpose
regions	Represents high_level geographic areas used to group countries for reporting and analysis
countries	Defines specific nations within each region and links orders to their geographic origin
categories	Groups products into logical categories for organizationa and analysis
products	Stores individual product types referenced in orders and links them to their category.
sales_channels	Identifies whether an order was placed online or offline, supporting channel_based reporting. 
order_priorities	Captures the urgency level of each order (e.g. H, M, L, C) for fulfillment and performance analysis.
orders	Serves as the central fact table containing transactional sales data linked to all dimension tables. 
Figure 2. 
b. How the Proposed Database Design Solves EcoMart’s Business Problems
EcoMart’s original dataset was a flat CSV containing only historical sales transactions. It lacked structure, integrity, security, and the ability to scale with the needs of a real marketplace. The proposed relational database design directly addresses these issues by transforming the flat file into a normalized, interconnected schema that supports both operational workflows and analytical reporting.
The proposed relational database design solves EcoMart’s business problems by replacing the flat, denormalized CSV with a fully normalized schema that enforces data integrity, eliminates redundancy, and supports scalable growth. By separating the regions, countries, categories, products, sales channels, and order priorities into dimension tables, and the orders table into a fact table with multiple foreign keys to the dimensions, the design removes transitive dependencies and ensures consistent, validated data. Foreign key constraints and cascade rules maintain referential integrity, while removing derived values prevents inconsistencies. The structure supports operational needs such as product management, inventory tracking, and secure access control, which the original dataset could not provide. Overall, the database delivers the flexibility, reliability, and performance required for EcoMart to operate and scale sustainably as an online marketplace.

The purpose of this PostgreSQL database is to establish a reliable, normalized foundation for EcoMart’s core operational data. The current design focuses on the elements available in the initial dataset -- regions, countries, categories, products, sales channels, order priorities, and orders -- providing a structured transactional backbone for storing and managing sales information. This first phase ensures data integrity, reduces redundancy, and creates a consistent framework for querying and reporting.

At the same time, the database is intentionally designed with EcoMart’s long-term goals in mind. As the platform evolves, EcoMart will require additional capabilities such as inventory tracking, sustainability certifications, customer accounts, and user reviews. Although these attributes were not present in the original dataset, the schema is structured to accommodate them in future phases without requiring major redesign. This approach allows EcoMart to begin with a solid operational foundation while maintaining flexibility for future expansion.

B. Logical Data Model 
The logical data model transforms EcoMart’s conceptual requirements into a structured relational star schema. Using a relational (OLTP) schema, the design ensures data consistency and eliminates redundancy through normalization (3NF), having no repeating groups and no partial or transitive dependencies (Aly, n.d.). Redundancy is reduced, specifically by isolating category and certification details into separate dimensional tables. An OLTP database is designed to support a company’s day-to-day operations, a necessity for EcoMart. (Coronel & Morris, 2023). 

1. Business Data Usage Within the Database Solution

The business data in EcoMart’s PostgreSQL database supports the core transactional and analytical needs of the marketplace. Each table captures a specific business dimension, and together they form a normalized structure that ensures accuracy, consistency, and scalability as EcoMart grows.
The dimension tables: regions, countries, categories, products, sales channels, and order priorities store descriptive business information that rarely changes. These tables provide controlled vocabularies for geographic areas, product groupings, and operational attributes. By separating this information into dedicated entities, the database eliminates redundancy and centralizes updates to business definitions.
The orders table serves as the central fact table, storing the transactional data that reflects EcoMart’s day-to-day operations. Each order links to the appropriate dimension values via foreign keys, allowing the business to analyze sales by region, product category, channel, or priority, as shown in the ERD below. Storing atomic values such as units sold, unit price, and unit cost enables accurate calculations of revenue and profit without relying on inconsistent derived fields.
This structure allows EcoMart to run reliable queries for reporting, performance analysis, and operational decision-making. It supports questions such as which regions generate the most revenue, which product categories perform best, how sales differ between online and offline channels, and how order priority affects fulfillment timelines.
EcoMart Entity Relationship Diagram (ERD)
 
Figure 3. Each table contains only attributes that depend on the primary key, reflecting a fully 3NF design.
(ERD generated using PgAdmin4 8.2 inside the WGU virtual lab)

2. Database Objects, Storage, and File Attributes 
The tables below expand on the ERD above by listing constraints, nullability, and cascade rules in addition to the table/column names, data types, and key types. 
regions (dimension table)
Attribute 	 Data Type 	 Constraints 	Nullability 	 Cascade Rule
region_id	 SERIAL 	 Primary Key 	 	 
region_name	VARCHAR(100)	 UNIQUE	 NOT NULL 	 

countries (dimension table)
Attribute 	 Data Type 	 Constraints 	Nullability 	 Cascade Rule
country_id	 SERIAL 	 Primary Key 	 	 
country_name	VARCHAR(100)	 UNIQUE	 NOT NULL 	 
region_id	INTEGER	 Foreign key -> referencing regions(region_id)	 NOT NULL 	 ON UPDATE CASCADE, ON DELETE CASCADE

categories (dimension table)
Attribute 	 Data Type 	 Constraints 	Nullability 	 Cascade Rule
category_id 	 SERIAL 	 Primary Key 	 NOT NULL 	 
category_name 	VARCHAR(100) 	 UNIQUE	 NOT NULL 	

products (dimension table)
Attribute 	 Data Type 	 Constraints 	Nullability 	 Cascade Rule
product_id 	 SERIAL 	Primary Key 	 	
category_id 	 INTEGER 	Foreign Key → categories(category_id) 	 NOT NULL 	 ON UPDATE CASCADE, ON DELETE RESTRICT
product_name 	 VARCHAR(100) 	UNIQUE	 NOT NULL 	 

sales_channels (dimension table) 
Attribute 	 Data Type 	 Constraints 	Nullability 	 Cascade Rule
sales_channel_id	 SERIAL 	 Primary Key 	 	
sales_channel_name	VARCHAR(100)	 UNIQUE	 NOT NULL 	 

orders_priorities (dimension table)
Attribute 	 Data Type 	 Constraints 	Nullability 	 Cascade Rule
order_priority_id	 SERIAL 	 Primary Key 	 NOT NULL 	 
order_priority_name	VARCHAR(100) 	 UNIQUE	 NOT NULL 	 

orders (facts table)
Attribute 	 Data Type 	 Constraints 	Nullability 	 Cascade Rule
order_id 	BIGSERIAL	 Primary Key 	 	
order_date	DATE	 	 NOT NULL 	
ship_date	DATE		NOT NULL	
country_id	INTEGER	Foreign key	NOT NULL	ON UPDATE CASCADE 
ON DELETE RESTRICT
sales_channel_id	INTEGER	Foreign key	NOT NULL	ON UPDATE CASCADE 
ON DELETE RESTRICT
order_priority_id	INTEGER	Foreign key	NOT NULL	ON UPDATE CASCADE 
ON DELETE RESTRICT
product_id	INTEGER	Foreign key	NOT NULL	ON UPDATE CASCADE 
ON DELETE RESTRICT
units_sold	INTEGER	CHECK(units_sold>=0)	NOT NULL	
unit_price	NUMERIC(12,2)	CHECK(unit_price >=0)	NOT NULL	
unit_cost	NUMERIC(12,2)	CHECK(unit_cost>=0)	NOT NULL	
Figure 4.

Database Objects: Tables are listed above, with primary keys (PK) and foreign keys (FK) and referenced tables listed alongside each table. These are also labeled in the ERD above. 
Views. A view is a virtual table created from a SELECT statement that queries base tables. It is convenient and prevents stakeholders from having to retype the same query. By creating the view ‘revenue_by_item_type’, EcoMart’s database will provide a reusable, simplified interface for analysts and applications (Colonel & Morris, 2023). The views make an impact by providing consistent, easy access to a frequently used metric without requiring a query rewrite.
Index. An index in a database is similar to an index in a book; instead of going through all available records, it allows queries to use quick index references, saving substantial execution time. The file attributes discussed further in the implementation section of this paper include indexed columns: idx_orders_country_id, idx_orders_product_id, and idx_orders_order_date. 

File Attributes Identification: In this database design, the attributes from EcoMart are categorized by their roles within the relational OLTP schema. 

Keys: The primary and foreign keys in the ERD above define the schema's structure and relationships. For example, the ‘orders’ table links to countries, ‘products’, sales channels, and order priorities. The countries table links back to regions, and the products table links to `categories This confirms that my design follows a classic star schema pattern, with orders as the central fact table and the other tables serving as dimensions.

Relationships. The relationships in the schema are enforced through foreign keys. For example, orders.country_id links each order to a single country, and countries.region_id links each country to a single region, forming a one‑to‑many relationship from regions to countries and from countries to orders.

Relationship	Cardinality	Explanation	
Regions -> countries
Countries -> regions	1:N
1:1	One region contains many products; 
a product has one country.
Countries -> orders
Orders -> countries	1:N
1:1	One country can appear in many orders; 
one order references one country
Categories -> products
Products -> categories	1:N
1:1	One category can have many products; 
one product belongs to one category
Products -> orders
Orders -> products	1:N
1:1	One product can appear in many orders;
One order references one product
Sales_channels -> orders
Orders -> sales_channels	1:N
1:1	One sales channel can be used in many orders;
One order uses one sales channel
Order_priorities -> orders
Orders -> order_priorities	1:N
1:1	One priority level can apply to many orders;
One order has one priority level
Figure 5. 
Constraints: NOT NULL is a column-level constraint that prevents NULL values by requiring a value for that field whenever a row is inserted or updated.
This constraint is set on key columns (e.g., order_date, units_sold, unit_price, unit_cost). UNIQUE constraints ensure that no two rows have the same name. For example, I placed one on region_name and country_name, to ensure each country_id and region_id matches only one name. This keeps the dimension table clean and ensures consistent joins between orders and countries.
Other Constraints. Although cascade rules are not file attributes themselves, they are documented in the Keys and Constraints subsection because they define the referential behavior of foreign key relationships within the schema. Most of the foreign keys use ON UPDATE CASCADE, which means that if a primary key changes in a parent table, the update automatically cascades to the child rows. They also use ON DELETE RESTRICT, which prevents deleting a parent row when dependent child rows exist. This protects the integrity of the fact table and prevents orphaned records.
Storage: In this logical model, storage refers to the relational tables and supporting database objects that hold and organize business data. Each table includes file attributes such as column names, data types, constraints, and keys that determine how data is stored and validated. 
Indexes provide additional storage structures that optimize query performance, and views offer virtual representations of combined data without physically storing it. These objects collectively define how the database stores, retrieves, and manages EcoMart’s operational data.

Normalization: Normalization directly shapes the database's storage objects, tables, keys, constraints, and indexes. By decomposing the CSV into dimension tables—regions, countries, categories, products, sales channels, and order priorities—the design removes repeated descriptive values and enforces consistency across the system. Each entity is stored once, referenced by a surrogate key (order_id), and protected by constraints. This eliminates redundancy, inconsistency risk, and update anomalies inherent to flat files.
Third Normal Form (3NF): EcoMarts schema satisfies 3NF; all transitive dependencies are eliminated by splitting descriptive attributes into dimension tables.
	Every table has a primary key:
•	country_id
•	region_id
•	sales_channel_id
•	order_priority_id
•	category_id
•	product_id
•	order_id 

	There are no transitive dependencies
•	Regions are separated from countries
•	Categories are separated from products
•	Sales channels and priorities are separated into lookup tables
•	Orders reference only surrogate keys
•	Derived metrics are not stored

	No derived values stored
•	Calculated values in the total_revenues, total_cost, and total_profit are intentionally excluded in the orders facts table. 
o	These are derived from units_sold * unit_price; units_sold * unit_cost.

C. Addressing System Scalability, Growth Projections, and Demand Requirements
The schema is optimized for performance and scalability. Indexes on primary and foreign keys, normalized tables, and a star schema-aligned structure allow EcoMart to handle increasing volumes of:
•	products
•	vendors
•	customers
•	transactions

The design supports fast analytical queries and efficient operational workloads, solving the scalability limitations of the CSV
The current database design represents the first phase of EcoMart’s data infrastructure: a normalized transactional foundation built from the attributes available in the original dataset. While this structure supports core order processing and provides a reliable backbone for reporting, EcoMart’s long-term business model anticipates additional capabilities that extend beyond the scope of the initial CSV. As the platform evolves, the database is intentionally positioned to incorporate new entities and relationships without requiring structural redesign.
Although the initial dataset includes only historical sales transactions, the schema is intentionally designed to accommodate future business needs. As EcoMart expands, additional tables—such as inventory, sustainability certifications, suppliers, users, and reviews—can be integrated without restructuring the existing design. This ensures that the database not only supports current operations but also provides a scalable foundation for future marketplace functionality.
Several enhancements are planned for future phases as EcoMart expands its marketplace features and begins collecting richer operational data, including: 
	Inventory and Availability: EcoMart will need to track stock levels, restock dates, and product availability to support real-time purchasing and fulfillment. An inventory table can be added to the existing schema without modification to the current tables.

	Sustainability Certifications: Because EcoMart emphasizes eco-friendly and ethically sourced products, future iterations of the database will include a sustainability_certifications table and a bridge table (`productcertifications) to support many-to-many relationships between products and certifications such as Fair Trade, USDA Organic, or Carbon Neutral.
	Customer Accounts and Reviews: To support user engagement and product feedback, the schema will expand to include users and user_reviews. These additions will enable ratings, comments, and personalized experiences while maintaining the integrity of the existing product and order structure.

	Supplier and Vendor Management: As EcoMart grows its catalog, supplier information will become essential for managing sourcing, pricing, and fulfillment. Future tables can be added to represent vendors, supply relationships, and procurement workflows.

	Operational and Fulfillment Data: The current dataset contains only historical sales transactions. Future phases will incorporate operational data, including warehouse locations, fulfillment statuses, and shipping performance metrics, to support end-to-end marketplace operations.
Because the current design is fully normalized and uses surrogate keys, it can be extended to these additional domains without restructuring the existing tables. Each new feature can be added as a new dimension or relationship, preserving the integrity and performance of the transactional core. This phased approach allows EcoMart to begin with a clean, reliable foundation while maintaining flexibility for future growth. (Geeksforgeeks.org, 2025, Jul 23)
D. Database Privacy and Security Measures
The database protects data through layered technical and administrative controls built directly into the design:
•	Role-based access control (RBAC): Users are assigned roles that limit what tables and operations they can access, ensuring the principle of least privilege.
•	Foreign key constraints and cascades: These enforce data integrity, preventing unauthorized or accidental changes from breaking relationships.
•	Input validation via constraints: CHECK constraints, NOT NULL rules, and data types prevent invalid or malicious data from being stored.
•	Encryption (at rest and in transit): Data is protected on disk and during transmission to prevent interception or unauthorized reading.
•	Audit logging and monitoring: The system records access and changes to detect suspicious activity and support compliance.
•	Secure deletion and retention policies: Cascading rules and controlled deletes ensure data is removed safely and consistently.
•	Network and authentication controls: Strong passwords, MFA, and restricted network access prevent unauthorized connections.
(Malik, Goldwasser, and Johnston, 2019)
	In the EcoMart database, security and privacy are supported at both the system level and within the table structure. 

	Strong authentication practices, such as enforcing complex passwords and MFA, control who can access sensitive tables, such as orders, which contain transactional and financial data. 

	Role-based permissions ensure that only authorized users can modify dimension tables such as products, countries, or regions, preventing unauthorized changes to the reference data on which the fact table depends. 

	Within the schema, integrity constraints provide an additional layer of protection: foreign keys between orders and dimensions like ‘sales_channels’, ‘order_priorities’, and `products’ prevent tampering or accidental deletion of linked records, while CHECK rules on fields such as ‘units_sold’, ‘unit_price’, and ‘unit_cost’ block invalid or malicious values from being inserted. (Malik, 2019).

EcoMart CHECK Constraints:

    "orders_unit_cost_check" CHECK (unit_cost >= 0::numeric)
		1. `unit_cost >= 0` --Prevents negative unit costs.
		A product cannot cost a negative amount to produce.
	  "orders_unit_price_check" CHECK (unit_price >= 0::numeric)
		2. `unit_price >= 0` --Prevents negative selling prices.
		EcoMart cannot sell an item for a negative price.
    "orders_units_sold_check" CHECK (units_sold >= 0)
		3. `units_sold >= 0` --Prevents negative quantities.
EcoMart cannot sell  5 units of something.
These CHECK constraints enforce business rule validation at the database level. They prevent invalid or impossible values from ever being inserted into the orders table.
	Encryption protects sensitive order-level information during storage and transmission, and regular backups ensure the availability of critical tables. Together, these measures safeguard the confidentiality of order data, preserve the integrity of dimension relationships, and maintain the overall availability of the EcoMart database. (Geeksforgeeks.org, 2025, Oct 28). 








Part 2: PostgreSQL Implementation

Create the Database 
 Figure 6.

Purpose: Create a database called “D597 Task 1” in PostgreSQL’s default public schema. This is the default workspace provided by PostgreSQL, and it is fully appropriate for this assessment because all tables, keys, indexes, and views remain organized and accessible within a single, consistent namespace.
Staging Table Creation (raw_eco)
 
Figure 7.

Purpose: to provide a temporary holding area that mirrors the flat file structure, allowing the CSV data to be loaded as is before being cleaned and normalized into the final schema.




Normalized Temporary WorkingTable Creation (ecomart)
 Figure 8. Create a Temporary Table for CSV Import (target columns to bypass cleaning headers in CSV file)

Purpose: To create a temporary table for intermediate transformations and cleaned versions. The staging and temporary working table are dropped after the dimension, and fact tables are created and populated. 
















CSV Import into Temporary Table, Data Transformation and Load into Cleaned Table
 
Figure 9.

Purpose:  To extract the CSV data, stage it in a temporary table, apply normalization and data cleaning, and insert the refined dataset into ecomart

Create and Populate Normalized Tables from Staging

Create and Populate Regions Dimension Table
 
Figure 10.


Create and Populate Countries Dimension Table  
Figure 11.

Create and Populate Sales Channels Dimension Table
 
Figure 12.

Create and Populate Order Priorities Dimension Table 
Figure 13.

Create and Populate Categories Dimension Table 
Figure 14.


Create and Populate Products Dimension Table 
Figure 15.

Purpose: Dimension tables hold the descriptive details that give meaning to the facts, enabling filtering, grouping, and reporting. They contain stable, low volatility attributes that define the “who, what, where, and when” of each fact table record.







Facts Table: Create and Populate Orders Facts Table Figure 16.
Purpose: A fact table stores the measurable business events of the system—such as quantities, prices, costs, and dates—and links them to the surrounding dimension tables through foreign keys. Its purpose is to capture the numeric facts at the lowest level of detail so they can be aggregated, analyzed, and reported across any combination of dimensions.
Drop Tables Figure 17.
Purpose: Now that the facts and dimension tables have been created the staging and temporary working tables can be dropped.  
Query 1 — Revenue by Item (specifically total revenue of item_type ‘Snacks’in 2016) 
The following query demonstrates how the database can be used to retrieve specific business insights, such as total revenue for a particular product within a defined time period. Although this example focuses on Snacks in 2016, the same structure can be applied broadly to analyze any product or timeframe:
 Figure 18. This query shows that historically, household items have generated the most revenue at 27.7 billion, with office supplies running a close second at 27.5 billion  
Query 1 WHERE Clause Figure 19. Business problem addressed: Limited ability to analyze product performance
Query 1 Analysis. This query calculates total revenue for each product type by multiplying units sold by unit price. It identifies which product categories generate the most revenue, helping EcoMart understand demand patterns and prioritize high-performing product lines. The WHERE clause narrows the general revenue by item-type to check for the amount of revenue snacks drew in for the year 2016. 
.













Query 2 – Overall Profit by Region (North America) 
This query retrieves total profit aggregated by region, allowing EcoMart to identify which geographic markets generate the highest profitability. It supports strategic decisions related to regional investment, marketing allocation, and supply chain prioritization. This query provides a global view of total profit by region, which helps EcoMart identify its strongest and weakest geographic markets.
 Figure 20.
Query 2 WHERE Clause Figure 21. Business problem addressed: No visibility into regional profitability or financial risk.
Query 2 Analysis: This query applies the WHERE clause to North America to demonstrate how the database can answer more targeted business questions. Although this example focuses on one region, the structure can be reused for any region or timeframe as needed. 
Query 3 -- Shipping Performance by Region (in 2016)

The third query retrieves the average number of days between order and shipment for each region. It provides a broad view of EcoMart’s shipping performance and helps identify regions where fulfillment processes may be slower or more efficient.

 
Figure 22.



















Query 3 WHERE Clause
 Figure 23. Business problem addressed: No ability to monitor fulfillment performance or identify bottlenecks.	
Query 3 Analysis. This applies the same logic to a WHERE clause applied to a specific timeframe—orders placed in 2016—to demonstrate how the database can support more targeted operational analysis. Although this example focuses on a single year, the structure can be reused for any date range.
The three SQL queries—total profit by item type, overall profit by region, and average shipping performance by region—directly support EcoMart’s need for improved monitoring and operational visibility (Problem 4). These queries provide insight into product profitability, regional performance, and fulfillment efficiency, enabling EcoMart to detect anomalies, identify bottlenecks, and maintain long‑term system stability. Although each query focuses on a different aspect of operations, together they demonstrate how the relational database supports proactive monitoring across the organization.






4. Optimization Techniques
Index List Figure 24.
Optimization Techniques Analysis. The optimization techniques applied to the queries demonstrate how indexing and query planning improve performance in EcoMart’s relational database. By comparing EXPLAIN ANALYZE results before and after creating indexes, each optimization shows how PostgreSQL shifts from slower sequential scans to more efficient index based lookups, reducing execution time and improving scalability as data volume grows.
Query 1 Optimization

Before Index
 
Figure 25.

Before Optimization: PostgreSQL had to scan the entire orders table because it had no efficient way to locate rows for the selected product. Even though the query filtered by product name and date, the database was forced to perform a full table scan and then apply the filters afterward, which meant processing a large number of unnecessary rows. This also required a more expensive hash join between orders and products, adding additional overhead. As a result, the query took longer to run because PostgreSQL was doing far more work than needed to return a small, targeted subset of data.
Create Index and After Optimization  Figure 26. Impact: More efficient product-level revenue analysis, enabling EcoMart to identify high-performing product categories as the catalog grows.
After Optimization: Creating an index on orders_product_id completely changed PostgreSQL’s execution strategy. Instead of scanning the entire table, the database was able to use the new index to jump directly to the relevant product rows. This allowed PostgreSQL to perform a Bitmap Index Scan followed by a Bitmap Heap Scan—both far more efficient than a full table scan—and to reduce the amount of data it needed to process before applying the date filter. The join method also shifted to a nested loop, which is faster when working with a small, filtered dataset. As a result, the query now runs much more efficiently because PostgreSQL retrieves only the necessary rows rather than scanning the entire table.














Create Non-Materialized View Figure 27. Impact: Consistent, easy access to a frequently used metric without rewriting the query.
VIEW Analysis:. After removing the WHERE clause, a non-materialized view (revenue_by_item_type) provides a reusable, simplified interface for analysts and applications (Malik, Goldwasser & Johnston, 2019).










Query 2 Optimization
Before Index Figure 28.
Before Optimization: PostgreSQL had to work much harder to return the total profit for North America because no indexes existed on the join columns. Without an index on `orders.countryid or `countriesregion_id, the database was forced to perform a full scan of the orders table and then join every matching row to `countriesand regions before applying the region filter. This meant PostgreSQL processed far more data than necessary and relied on a more expensive hash join to combine the tables. As a result, the query took longer to execute because the database had no efficient way to locate only the rows belonging to North America.









After Index and Optimization Figure 29.
After Optimization: After creating indexes on orders.country_id and countries.region_id, PostgreSQL was able to change its execution strategy entirely. Instead of scanning the entire orders table, the database used the new indexes to quickly locate only the rows associated with countries in North America. This allowed PostgreSQL to avoid unnecessary work, reduce the amount of data processed during the join, and switch to a more efficient join method. With fewer rows to examine and a direct access path to the relevant data, the query executed much faster and required significantly less effort from the database engine.











Query 3 Optimization
Before Index 
 
Figure 30.

Before Optimization: PostgreSQL had to scan the entire orders table to evaluate the date-range filter because there was no index existed on order_date. Even though the query only needed rows from 2016, the database had to read all rows and then discard those outside the date range. Additionally, without an index on ‘orders.country_id’, PostgreSQL had to perform a more expensive join between ‘orders’ and ‘countries’ before grouping by region. This resulted in unnecessary work, more data being processed, and slower overall execution because the database lacked an efficient way to locate only the rows relevant to the selected year and region.




After Index and Optimization Figure 31. Impact: Faster insight into fulfillment performance, helping EcoMart identify regions with slower shipping and potential operational bottlenecks.
After Optimization: Creating indexes on ‘orders.order_date’ and ‘orders.country_id’ significantly streamlined the query. The index on order_date allowed the database to quickly isolate only the rows from 2016, reducing the workload before the join even began. The index on country_id provided a direct access path for matching orders to their corresponding countries, making the join more efficient and reducing the amount of data PostgreSQL needed to process. With these indexes in place, the database could retrieve only the necessary rows and perform the join and aggregation much faster, resulting in a more efficient execution plan and noticeable performance improvements.
Overall Optimization Benefits to EcoMart
 Across all three queries, performance improved because PostgreSQL was given indexes that allowed it to avoid full-table scans and retrieve only the rows needed for each analysis. By indexing key columns used in joins and filters—such as product_id, country_id, and order_date—the database could jump directly to relevant records rather than scanning entire tables. This reduced the amount of data processed during joins, enabled more efficient access paths like bitmap scans and nested loops, and minimized unnecessary work before grouping or aggregating results. Overall, the optimizations enabled PostgreSQL to execute each query more efficiently by narrowing the search space early and streamlining join and filtering operations.


Database Validation
Validating a database demonstrates that the schema is correctly designed, that the data loads properly, that the relationships function as intended, that the queries return accurate results, and that the constraints reliably enforce data integrity.
 Figure 32.
This query checks the integrity of the foreign key relationships in the orders table by identifying any rows that fail to match a corresponding record in the countries, regions, or products tables. By using LEFT JOIN and counting the number of NULL values, the query reveals whether any orders reference has missing or invalid country IDs, region IDs, or product IDs. This helps confirm that the database is properly linked and that no orphaned or inconsistent records exist across these core tables.

























Confirm PK’s, FK’s, UNIQUE constraints, CHECK constraints
  Figure 33.



Validate Referential Integrity (FK check)  Figure 34.
This query validates referential integrity by joining the orders fact table to each of its related dimension tables and checking for any missing matches. If a foreign key fails to join—resulting in a NULL value—the query flags it as a violation, and if no rows are returned, it confirms that all foreign key relationships in the EcoMart schema are consistent and fully enforced.
Conclusion

The EcoMart database project delivers a complete, normalized, and secure data solution that directly addresses the business problems identified in the scenario. By first identifying three core business challenges, the design process focused on building a structure capable of supporting accurate reporting, eliminating redundancy, and improving decision-making. A fully normalized ERD with six entities and clearly defined relationships was developed, supported by a staging table for safely importing and transforming the flat CSV data. The resulting normalized tables reduce duplication and ensure consistent, high-quality data across the system. 
To solve real manufacturing and operational problems, three targeted business queries were written to analyze sales performance, profitability, and regional trends. Indexes were added to improve query performance and support efficient analytical workloads. Validation steps—including row counts, constraint testing, and multi-table join verification—confirmed that the database behaves as intended and maintains strong referential integrity. Together, these design choices create a robust, secure, and scalable database environment that provides EcoMart with meaningful, actionable insights to support better business decisions.







References

Coronel, C., & Morris, S.. (2023). Database Systems: Design, Implementation, and Management, 1(4th ed.). Cengage Learning, Inc. 

Geeksforgeeks.org. (2025, October 28). Database Security. https://www.geeksforgeeks.org/dbms/database-security/ 

Geeksforgeeks.org. (2025, July 23). How to Design a Relational Database for E-Commerce Website. https://www.geeksforgeeks.org/dbms/how-to-design-a-relational-database-for-e-commerce-website/

Geeksforgeeks.org. (2025, September 27). PostgreSQL Turorial. https://www.geeksforgeeks.org/postgresql/postgresql-turorial/

LinkedIn. (n.d.). How Can You Establish Relationships Between Tables in a Relational Database. https://www.linkedin.com/advice/3/how-can-you-establish-relationships-between-tables-vazgf

Malik, U., Goldwasser, M., & Johnston, B. (2019). SQL for data analytics: Perform fast and efficient data analysis with the power of SQL. Packt Publishing. EBSCOhost eBook Collection.

Microsoft. (last updated 10/2/2025). Online Transaction Processing (OLTP). https://learn.microsoft.com/en-us/azure/architecture/data-guide/relational-data/online-transaction-processing

Rutledge, R. (accessed January 24, 2026). Constructing a Logical Data Model: Tables, Records, and Fields [Class Module, Lesson 4.1.1]. School of Technology, Western Governors University.

Rutledge, R. (accessed January 24, 2026). Data Availability: Data Type Repositories [Class Module, Lesson 3.1.3]. School of Technology, Western Governors University. 

Smallcombe, Mark. (2023, September 4). Star Schema vs Snowflake Schema: 10 Key Differences. https://www.integrate.io/blog/snowflake-schemas-vs-star-schemas-what-are-they-and-how-are-they-different/

Western Governors University. (downloaded January 24, 2026). D597 Case Study 1: Manufacturing–Production Quality Control System [PDF]. WGU Course Resources.

Western Governors University. (downloaded January 24, 2026). Steps to Approach Database Normalization. [Class handout]. School of Technology. Western Governors University. 


[github](https://github.com/MeredithClikkie/D597Task1S1S2.git)
