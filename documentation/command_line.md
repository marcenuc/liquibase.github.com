---
layout: default
title: Command line
---

# Liquibase Command Line #

Liquibase can be run from the command line by running
**liquibase \[options\] \[command\] \[command parameters\]** (optionally, replace the liquibase command with java -jar &lt;path-to-liquibase-jar&gt;). The command line migrator works well when you want to do migrations on demand, but don't have Ant or Maven available such as on servers. The command line migrator also gives you more control over the process than the ["servlet listener"](servlet_listener.html), [Ant](ant/index.html), or [Maven](maven/index.html) do, allowing you to run maintenance commands like outputting SQL and listing/releasing database changelog locks.

Any values found after the command on the command line invocation will be considered a command parameter. The command line processor will validate whether the command line parameters are allowed for the current command. If the current command does not allow command line parameters or the parameter appears to be an incorrect format, then an error message of 'unexpected command parmeter' will be logged and the execution will terminate.

The command line migrator also allows you to

* [perform rollback operations and generate rollback scripts](rollback.html)
* [generate "diff"s](diff.html)
* [generate creation scripts from existing databases](generating_changelogs.html)
* [generate database change documentation](dbdoc.html)

If you run the command line migrator without any arguments, you will get a help message listing these available parameters:


## Database Update Commands ##

<table>
<tr><td>update</td><td>Updates database to current version</td></tr>
<tr><td>updateCount &lt;value&gt;</td><td>Applies the next &lt;value&gt; change sets  </td></tr>
<tr><td>updateSQL</td><td>Writes SQL to update database to current version to STDOUT</td></tr>
<tr><td>updateCountSQL &lt;value&gt;</td><td>Writes SQL to apply the next &lt;value&gt; change sets to STDOUT  </td></tr>
</table>




## Database Rollback Commands ##

<table>
<tr><td>rollback &lt;tag&gt;</td><td>Rolls back the database to the state it was in when the tag was applied  </td></tr>
<tr><td>rollbackToDate &lt;date/time&gt;</td><td>Rolls back the database to the state it was in at the given date/time  </td></tr>
<tr><td>rollbackCount &lt;value&gt;</td><td>Rolls back the last &lt;value&gt; change sets  </td></tr>
<tr><td>rollbackSQL &lt;tag&gt;</td><td>Writes SQL to roll back the database to the state it was in when the tag was applied to STDOUT  </td></tr>
<tr><td>rollbackToDateSQL &lt;date/time&gt;</td><td>Writes SQL to roll back the database to the state it was in at the given date/time version to STDOUT  </td></tr>
<tr><td>rollbackCountSQL &lt;value&gt;</td><td>Writes SQL to roll back the last &lt;value&gt; change sets to STDOUT  </td></tr>
<tr><td>futureRollbackSQL</td><td>Writes SQL to roll back the database to the current state after the changes in the changeslog have been applied</td></tr>
<tr><td>updateTestingRollback</td><td>Updates the database, then rolls back changes before updating again </td></tr>
<tr><td>generateChangeLog</td><td>generateChangeLog of the database to standard out. v1.8 requires the dataDir parameter currently.</td></tr>
</table>

## Diff Commands ##

<table>
<tr><td>diff \[diff parameters\]</td><td>Writes description of differences to standard out  </td></tr>
<tr><td>diffChangeLog \[diff parameters\]</td><td>Writes Change Log XML to update the base database to the target database to standard out  </td></tr>
</table>


## Documentation Commands ##
<table>
<tr><td>dbDoc &lt;outputDirectory&gt;</td><td>Generates Javadoc-like documentation based on current database and change log  </td></tr>
</table>





## Maintenance Commands ##

<table>
<tr><td>tag &lt;tag&gt;</td><td>'Tags' the current database state for future rollback  </td></tr>
<tr><td>status</td><td>Outputs count (list if --verbose) of unrun change sets</td></tr>
<tr><td>validate</td><td>Checks the changelog for errors</td></tr>
<tr><td>changelogSync</td><td>Mark all changes as executed in the database</td></tr>
<tr><td>changelogSyncSQL</td><td>Writes SQL to mark all changes as executed in the database to STDOUT</td></tr>
<tr><td>markNextChangeSetRan</td><td>Mark the next change set as executed in the database</td></tr>
<tr><td>listLocks</td><td>Lists who currently has locks on the database changelog</td></tr>
<tr><td>releaseLocks</td><td>Releases all locks on the database changelog</td></tr>
<tr><td>dropAll</td><td>Drops all database objects owned by the user. Note that functions, procedures and packages are not dropped (limitation in 1.8.1).</td></tr>
<tr><td>clearCheckSums</td><td>Removes current checksums from database.  On next run checksums will be recomputed</td></tr>
</table>
## Required Parameters ##

<table>
<tr><td>--changeLogFile=&lt;path and filename&gt;</td><td>The changelog file to use  </td></tr>
<tr><td>--username=&lt;value&gt;</td><td>Database username  </td></tr>
<tr><td>--password=&lt;value&gt;</td><td>Database password  </td></tr>
<tr><td>--url=&lt;value&gt;</td><td>Database URL  </td></tr>
<tr><td>--driver=&lt;jdbc.driver.ClassName&gt;</td><td>Database driver class name  </td></tr>
</table>





## Optional Parameters ##

<table>
<tr><td>--classpath=&lt;value&gt;</td><td>Classpath containing migration files and JDBC Driver.  </td></tr>
<tr><td>--contexts=&lt;value&gt;</td><td>ChangeSet contexts to execute  </td></tr>
<tr><td>--defaultSchemaName=&lt;schema&gt;</td><td>Specifies the default schema to use for managed database objects and for Liquibase control tables  </td></tr>
<tr><td>--databaseClass=&lt;custom.DatabaseImpl&gt;</td><td>Specifies a custom [Database](http://www.liquibase.org/api/liquibase/database/Database.html) implementation to use  </td></tr>
<tr><td>--defaultsFile=&lt;/path/to/file&gt;</td><td>File containing default option values (default: ./liquibase.properties)  </td></tr>
<tr><td>--includeSystemClasspath=&lt;true or false&gt;</td><td>Include the system classpath in the Liquibase classpath (default: true)  </td></tr>
<tr><td>--promptForNonLocalDatabase=&lt;true or false&gt;</td><td>Prompt if non-localhost databases (default: false)  </td></tr>
<tr><td>--currentDateTimeFunction=&lt;value&gt;</td><td>Overrides current date time function used in SQL. Useful for unsupported databases  </td></tr>
<tr><td>--logLevel=&lt;level&gt;</td><td>Execution log level (debug, info, warning, severe, off)  </td></tr>
<tr><td>--help</td><td>Output command line parameter help</td></tr>
<tr><td>--exportDataDir</td><td>Directory where insert statement csv files will be kept (required by generateChangeLog command)</td></tr>
</table>
## Required Diff Parameters ##

<table>
<tr><td>--referenceUsername=&lt;value&gt;</td><td>Base Database username  </td></tr>
<tr><td>--referencePassword=&lt;value&gt;</td><td>Base Database password  </td></tr>
<tr><td>--referenceUrl=&lt;value&gt;</td><td>Base Database URL  </td></tr>
<tr><td>--referenceUrl=&lt;value&gt;</td><td>Base Database URL  </td></tr>w
</table>

## Optional Diff Parameters ##

<table>
<tr><td>--referenceDriver=&lt;jdbc.driver.ClassName&gt;</td><td>Base Database driver class name  </td></tr>
</table>

## Change Log Properties ##
<table>
<tr><td>-D&lt;property.name&gt;=&lt;property.value&gt;</td><td>Pass a name/value pair for [substitution of ${} blocks](changelog_parameters.html) in the change log(s)  </td></tr>
</table>

## Using a liquibase.properties file ##

If you do not want to always specify options on the command line, you can create a [properties file](liquibase.properties.html) that contains default values. By default, Liquibase will look for a file called "liquibase.properties" in the current working directory, but you can specify an alternate location with the --defaultsFile flag. If you have specified an option in a properties file and specify the same option on the command line, the value on the command line will override the properties file value.

## Examples ##

### Standard Migrator Run ###

``
java -jar liquibase.jar \
      --driver=oracle.jdbc.OracleDriver \
      --classpath=\path\to\classes:jdbcdriver.jar \
      --changeLogFile=com/example/db.changelog.xml \
      --url="jdbc:oracle:thin:@localhost:1521:oracle" \
      --username=scott \
      --password=tiger \
      update
``

### Run Migrator pulling changelogs from a .WAR file ###

``
java -jar liquibase.jar \
      --driver=oracle.jdbc.OracleDriver \
      --classpath=website.war \
      --changeLogFile=com/example/db.changelog.xml \
      --url=jdbc:oracle:thin:@localhost:1521:oracle \
      --username=scott \
      --password=tiger \
      update
``

### Run Migrator pulling changelogs from an .EAR file ###

``
java -jar liquibase.jar \
      --driver=oracle.jdbc.OracleDriver \
      --classpath=application.ear \
      --changeLogFile=com/example/db.changelog.xml \
      --url=jdbc:oracle:thin:@localhost:1521:oracle \
      --username=scott \
      --password=tiger
``

### Don't execute changesets, save SQL to /tmp/script.sql ###

``
java -jar liquibase.jar \
        --driver=oracle.jdbc.OracleDriver \
        --classpath=jdbcdriver.jar \
        --url=jdbc:oracle:thin:@localhost:1521:oracle \
        --username=scott \
        --password=tiger \
        updateSQL > /tmp/script.sql
``

### List locks on the database change log ###

``
java -jar liquibase.jar \
        --driver=oracle.jdbc.OracleDriver \
        --classpath=jdbcdriver.jar \
        --url=jdbc:oracle:thin:@localhost:1521:oracle \
        --username=scott \
        --password=tiger \
        listLocks
``

### Runs Liquibase using defaults from ./liquibase.properties ###

``
java -jar liquibase.jar update
``

#liquibase.properties
``
driver: oracle.jdbc.OracleDriver
classpath: jdbcdriver.jar
url: jdbc:oracle:thin:@localhost:1521:oracle
username: scott
password: tiger
``

### Export Data from Database ###
This will export the data from the targeted database and put it in a folder "data" in a file name specified with &lt;insert file name&gt;.

``
java -jar liquibase.jar --changeLogFile="./data/<insert file name> " --diffTypes="data" generateChangeLog
``

### Update passing changelog parameters ###
``
liquibase.bat update -Dengine=myisam
``
