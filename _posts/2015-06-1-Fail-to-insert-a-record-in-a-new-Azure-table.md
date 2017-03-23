---
layout: post
title: Fail to insert a record in a new Azure table
image: /img/blog/azuredb.jpg
tags: [Azure,sql, database]
---
<p>Recently I came across an issue that I try to deploy a script generated from my local server, but fail to run it in the Azure SQL. I would like to share some resolutions here. </p>
<h3>The Issue:</h3>
<p>I try to  create a table with below:</p>
<pre><code>//Create a simple table<br />CREATE TABLE [dbo].[person](<br /> firstName [nvarchar](50) NOT NULL,<br /> lastName [nvarchar](50) NOT NULL<br />)<br />//Insert record<br /></code><code>Insert into [dbo].[] values('smith','D')</code></pre>
<p>Then try to run this script to insert the record in Azure SQL, surprisingly it will come across an error message:</p>
<pre><strong>//Error: Tables without a clustered index are not supported in this version of SQL Server. Please create a clustered index and try again.</strong></pre>
<p>It turns out that creating a new table will required the clustered index. Found out that there are some limitations in Azure server in the <em><strong><a href="https://msdn.microsoft.com/en-us/library/azure/ee336245.aspx#cir">Azure SQL Database General Guidelines and Limitations</a> </strong></em>reference:</p>
<pre><span>Tables in Microsoft Azure SQL Database versions prior to V12 must have a clustered index before insert operations are allowed on the table.</span></pre>
<h3>There are two solutions to Resolve this issue:</h3>
<p>1. Create the cluster index</p>
<pre><code> CREATE UNIQUE CLUSTERED INDEX Idx_Person ON person(firstName,lastname);<br /></code></pre>
<p> 2. Or simple just add a Primary Key Id column, which is also a good practice to have a primary key for each table.</p>
<pre><code>ALTER TABLE [person]<br />ADD [pId] UNIQUEIDENTIFIER NOT NULL DEFAULT(NEWID()) PRIMARY KEY </code></pre>