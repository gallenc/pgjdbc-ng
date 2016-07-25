# pgjdbc-ng-osgi

Branch pgjdbc-ng-osgi is a fork of the verion 0.6 release with the osgi changes back ported from 0.7 snapshot so that this version loads correctly in karaf

See pgjdbc-ng issue 250 https://github.com/impossibl/pgjdbc-ng/issues/250 

The latest 0.6 release of this driver has OSGi metadata using the very old styleManifest-Version = 1.0 
which doesn not import  javax and org.xml dependencies correctly. The patch for this issue allows
this bundle to install nicely in OSGi containers such as Apache Karaf

The patch for this issue in version 0.7-SNAPSHOT is 
https://github.com/impossibl/pgjdbc-ng/commit/e8e188d98bb1a3cbccfb3d1515b5547f2317c220  committed on Mar 16

When 0.7 is released by the pgjdbc-ng project we will be able to use it directly.

to use this branch build and reference the jar
 <groupId>com.impossibl.pgjdbc-ng</groupId>
 <artifactId>pgjdbc-ng</artifactId>
 <version>0.6.osgi</version>

# pgjdbc-ng

A new JDBC driver for PostgreSQL aimed at supporting the advanced features of JDBC and Postgres

[http://impossibl.github.io/pgjdbc-ng](http://impossibl.github.io/pgjdbc-ng "pgjdbc-ng homepage")

## Connection format

The connection format for the pgjdbc-ng driver is

	jdbc:pgsql://<server>[:<port>]/<database>

An example

	jdbc:pgsql://localhost:5432/test

## Driver

The java.sql.Driver class is

	com.impossibl.postgres.jdbc.PGDriver

The driver will accept configuration parameters in the style of

	jdbc:pgsql://localhost:5432/test?applicationName=MyApp&networkTimeout=10000

## Data sources

The javax.sql.DataSource class is

	com.impossibl.postgres.jdbc.PGDataSource

, the javax.sql.ConnectionPoolDataSource class is

	com.impossibl.postgres.jdbc.PGConnectionPoolDataSource

and the XADataSource class is

	com.impossibl.postgres.jdbc.xa.PGXADataSource

## Configuration

The driver and data sources supports the following configuration
properties (name, type and default value).

	host      (String) localhost

The 'host' parameter specifies the host name of the database server. Data sources only.

	port         (int)     5432

The 'port' parameter specifies the port number of the database server. Data sources only.

	database     (String)

The 'database' parameter specifies the name of the database on the database server. Data sources only.

	user   (String)

The 'user' parameter specifies the user name.

	password     (String)

The 'password' parameter specifies the password.

	housekeeper      (boolean) true

The 'housekeeper' parameter specifies if the JDBC driver should keep track connections, statements and result sets
and automatically close them if they can't no longer be reached.

	parsedSqlCacheSize   (int)   250

The 'parsedSqlCacheSize' parameter specifies how big the cache size for parsed SQL statements should be.

	preparedStatementCacheSize (int)     50

The 'preparedStatementCacheSize' parameter specifies how big the cache size for PreparedStatement instaces should be.

	applicationName          (String)  pgjdbc app

The 'applicationName' parameter specifies the application name associated with the connection on the database server.

	clientEncoding          (String)  UTF8

The 'clientEncoding' parameter specifies the client encoding for the database server.

	networkTimeout         (int)     0

The 'networkTimeout' parameter specifies the default timeout in milliseconds for the connections.
A value of 0 indicates that there isnt a timeout for database operations.

	strictMode          (boolean)  false

The 'strictMode' parameter specifies if the JDBC driver should follow behavior assumed by
certain frameworks, and test suites. See
[http://github.com/impossibl/pgjdbc-ng/wiki/StrictMode](http://github.com/impossibl/pgjdbc-ng/wiki/StrictMode "pgjdbc-ng strictMode")
for additional details.

## License

pgjdbc-ng is released under the 3 clause BSD license.

## Building
The driver is built with maven. Simply build with:

	mvn clean package

This will produce, in the target directory, two JAR files. One with dependencies
packaged inside and another without.

## Testing

The unit tests need a PostgreSQL database to execute against. The tests assume theses defaults:

	SERVER:     localhost
	PORT:       5432
	DATABASE:   test
	USERNAME:   pgjdbc
	PASSWORD:   test

The following system properties are supported in order to customize the setup

	pgjdbc.test.server
	pgjdbc.test.port
	pgjdbc.test.db
	pgjdbc.test.user
	pgjdbc.test.password

If you'd like to build the driver without running the unit tests use the command:

	mvn clean package -DskipTests
