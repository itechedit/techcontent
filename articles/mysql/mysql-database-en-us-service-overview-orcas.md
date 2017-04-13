<properties linkid="" urlDisplayName="" pageTitle="Azure Database for MySQL Service Overview – Microsoft Azure Cloud" metaKeywords="Azure Cloud, technical documentation, documents and resources, MySQL, database, beginner’s guide, Azure MySQL, MySQL PaaS, Azure MySQL PaaS, Azure MySQL Service, Azure RDS" description="The Azure Database for MySQL Service Overview lists the features and advantages of using the Azure Database for MySQL cloud database service." metaCanonical="" services="MySQL" documentationCenter="Services" title="" authors="" solutions="" manager="" editor="" />

<tags ms.service="mysql" ms.date="04/06/2017" wacn.date="04/06/2017" wacn.lang="cn" />

> [AZURE.LANGUAGE]
- [Chinese](/documentation/articles/mysql-database-service-overview-orcas/)

# About Azure Database for MySQL

Azure Database for MySQL is the MySQL cloud database service that we launched on the Azure platform. It is a type of relational database service that is fully compatible with MySQL protocols and provides users with a fully managed database service that features stable performance, rapid deployment, high availability, and high security. To cater to different user performance requirements, the Azure Database for MySQL service offers a total of four performance versions in two service tiers (basic and standard); performance improves exponentially in each version.

## What are the advantages of Azure Database for MySQL?
Azure Database for MySQL is a fully managed database platform service. Unlike locally created databases or solutions that are built using virtual machines, you don’t need to worry about infrastructure details, so you can focus better on developing service logic.

## Supports flexible upscaling/downscaling and simplifies the purchase experience

You no longer need to keep recalculating your database server configuration requirements, or worry about how to adjust various aspects of the configuration to achieve better database performance. The Azure Database for MySQL service is available in several versions offering differing performances, so you can choose the version that matches your current performance requirements and then flexibly up-scale or downscale as actual operating conditions change.

## Excellent monitoring experience

Azure Database for MySQL provides more than 20 types of monitoring indicators to help you monitor real-time indicators and historical data for every aspect of database performance. The indicators help you better understand database usage, identify problems, and make adjustments in a timely manner. You can also open and download database logs, which help database administrators to better manage and optimize the database. For specifics, see: Monitor and Manage Azure Database for MySQL.

## Offers high levels of availability and security

Azure Database for MySQL uses a high-availability architecture that guarantees database server availability rates in excess of 99.99% and delivers rapid failover. Azure Database for MySQL provides incremental backup and restore solutions, a firewall function that can whitelist your client-side public IP address (or IP address block), and supports SSL connections for database access. For more detailed information on SSL configuration, see Use SSL to Securely Access Azure Database for MySQL. We provide incremental backup and database restore functions, where the system automatically backs up the incremental changes in the database over the previous 35 days (7 days for the basic version) to facilitate rollback from any point in time. You can then restore the database to any point in time in the last 35 days (7 days for the basic version). (For details about backup and restore methods, see: Backup and Restore Azure Database for MySQL. )

## Rapid deployment with no need for manual infrastructure maintenance

Azure Database for MySQL makes it easy to deploy a high-availability MySQL database server in just one or two minutes. It also provides an automatic software patch function that means you don’t need to perform any infrastructure maintenance on the database service. To find out how to quickly deploy a MySQL database server, refer to the introduction course entitled Create and Use Your First MySQL Cloud Database Server.

## Supports familiar platforms and tools

Azure Database for MySQL is compatible with MySQL protocols and supports MySQL 5.6 and MySQL 5.7. You can perform database development and integration using platforms and technologies that are compatible with MySQL. You can also use familiar management tools such as mysql.exe and Workbench.

## Subsequent steps

### Understanding Service Tiers and Versions

Helps you find out about the different performance versions of Azure Database for MySQL.

### Beginner’s Guide to Azure Database for MySQL

Helps you quickly understand how to use Azure Database for MySQL.

<!---HONumber=AcomDC_0403_2017_MySql-->