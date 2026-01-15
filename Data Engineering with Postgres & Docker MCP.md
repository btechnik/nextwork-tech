<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Data Engineering with Postgres & Docker MCP

**Project Link:** [View Project](http://learn.nextwork.org/projects/mcp-data-engineer1)

**Author:** Nikhil Bhan  
**Email:** nikhilbhan@gmail.com

---

![Image](http://learn.nextwork.org/appreciative_maroon_jolly_saffron/uploads/mcp-data-engineer1_er-diagram-screenshot)

---

## Introducing Today's Project!

In this project, I'm going to use Cursor and MCPs to create and optimize a PostgreSQL database that will be stored within a Docker container.  Docker is a platform that allows users to create containers and package applications in them as well as their dependencies (e.g. tools, code, settings and libraries).  PostgreSQL is an open-source relational database engine that stores data in tables and uses SQL.  I'll use it in my project to develop an e-commerce system.

### Key tools and concepts

The key tools I used include UV (Python package manager), Cursor, MCPs, Docker and PostgreSQL.  Key concepts I learnt include database schemas, database optimization, Docker containers and interacting with Docker and PostgreSQL by using the MCPs in my Cursor environment.

### Challenges and wins

This project took me approximately 1 hour and 30 minutes to complete.  I used another 30 minutes to write my documentation.  The most challenging part was starting Docker Desktop and I resolved it by enabling the WSL service.  It was most rewarding to use natural prompts in Cursor to learn about my data in the database and view the output (e.g. "What products are ordered most frequently?".  With the skills I learnt, I want to develop complex databases with other types of tools.

### Why I did this project

I did this project today to learn how to use MCPs to interact with a PostgreSQL database on a Docker container and how to optimize queries.  Another database skill I want to learn is data warehousing.

---

## Setting Up Docker and UV

In this step, I'm setting up my development environment by installing uv, which is used for managing Python packages.  I'll also install Docker Desktop because it will help me run containers.

![Image](http://learn.nextwork.org/appreciative_maroon_jolly_saffron/uploads/mcp-data-engineer1_8h9i0j1k)

### What's Docker and why containers?

I'm using a Docker container to eliminate the issue where applications have problems running in different operating systems.  This is important because there will be multiple environments where the system configurations will be different from one another.  By using a Docker container I'll be able to have my application run regardless of where it's deployed.

### Verifying installations

I installed the uv tool because it's a Python package manager and it's faster than other tools like pip since it runs a compiled language called Rust.  I confirmed that uv was installed correctly by running the 'uv --version' command in the terminal application.  I'll use uv to install the PostgreSQL and Docker MCP servers.

---

## Connecting MCP Servers

In this step, I'm going to install MCP servers which are programs that connect and interact with tools that are external to my project codebase in Cursor.  Without MCPs, Cursor would be restricted to its own environment and it would only be able to interact with the codebase.  With MCPs, Cursor would be able to take my prompts (MCP tool calls) and it would interact with the external tools such as Docker and PostgreSQL.

### Python project setup

The 'uv init' command set up a Python project because I'll need a Python environment to run the MCP servers.  The files created include pyproject.toml, .gitignore, README.md and main.py.  The 'pyproject.toml' file tracks the project's dependencies.  The 'gitignore' file hides specific files from Git for security.  The 'README.md' file is where the project documentation is stored.  The last file 'main.py' contains an example of a Python program that can be modified for developing the project.

### Installing Docker MCP

![Image](http://learn.nextwork.org/appreciative_maroon_jolly_saffron/uploads/mcp-data-engineer1_mcp-config-screenshot)

---

## Building My Database

In this step, I'm going to use the Docker MCP to create a PostgreSQL container that will store a database schema.  I'll use the PostgreSQL MCP to configure database users so users can perform queries on the database.  Next I'll load demo data in the database and then visualize how the database looks.

![Image](http://learn.nextwork.org/appreciative_maroon_jolly_saffron/uploads/mcp-data-engineer1_postgres-container-screenshot)

### Database security

Every PostgreSQL database comes with a default superuser that's used only for administrative and maintenance tasks.  I created an application user so that my app can connect to the database, but with limited permissions.  This is security best practice because if my application user is compromised, then the attacker is limited to the permissions of that user.


### Loading demo data

I loaded demo data by downloading an SQL file and then running the 'Get-Content' command in the Cursor terminal.  In this command I specified parameters such as the container name (pg-local), the application user (app) and the database to load the data into (demo).  The data contains 4 tables, 2000 customers, 1000 products, 10000 orders and at least 30000 order items.

### Verifying and visualizing the database

I verified my database by prompting Cursor to use the PostgreSQL MCP to read the database schema, a sample of 3 rows from each table and then create a Mermaid ER diagram from the given information.  The Mermaid ER diagram shows the tables as boxes, the columns within each table, and the relationships as lines which shows how tables are related (e.g. customers can make one or more orders to show a 1 to Many relationship).  The diagram also contains sample data so I can see the values from the database.

![Image](http://learn.nextwork.org/appreciative_maroon_jolly_saffron/uploads/mcp-data-engineer1_er-diagram-screenshot)

---

## Performance Audit

I'm going to perform a database performance audit, which analyzes how efficiently my database can process queries.  Database administrators perform these audits to identify slow queries in production because they can take too much time, resources and charges if the database is hosted in a cloud environment.  Optimization is important because it helps identify slow queries that need to be optimized, finds missing indexes that can slow down searches, performs health checks to look for issues in the database and looks for bottlenecks, high costs and inefficiencies.

### Audit findings

Cursor's audit analyzed the database health, planning time, scan types and execution time by running 'Explain Analyze'.  Explain Analyze is a PostgreSQL command that shows what happens behind the scenes when a query is executed in the database.  It found an issue where the foreign key (FN) indexes were missing, which meant the database was currently using sequential scans to search for data and it resulted in slow queries.  The optimized recommendations included adding indexes for the 'orders.customer_id', 'order_items.order_id' and the 'order_items.product_id'.  These indexes would improve the execution time for queries and table join performance.

![Image](http://learn.nextwork.org/appreciative_maroon_jolly_saffron/uploads/mcp-data-engineer1_performance-screenshot)

### Performance gains

I prompted Cursor to use the PostgreSQL MCP to implement the foreign keys in the database.  After creating the indexes the execution time, planning time and cost metrics significantly improved.  Before the indexes were implemented, these metric values were 0.463 ms, 0.079 ms and 0.00 - 205.00 respectively.  After the indexes were implemented, the metric values were 0.028 ms, 0.105 ms and 4.32 - 20.64.  The execution plan changed from a Sequential Scan to a Bitmap Index and Heap Scan, which is useful when you need optimal data retrieval, when there's multiple conditions in queries and there's massive amounts of data.

---

---
