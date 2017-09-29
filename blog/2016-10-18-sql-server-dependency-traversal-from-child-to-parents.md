---
id: 91
title: 'SQL Server: Dependency Traversal from Child to Parents'
date: 2016-10-18T22:56:06+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=91
permalink: /2016/10/18/sql-server-dependency-traversal-from-child-to-parents/
categories:
  - how-to
  - sql
---
<pre class="lang:tsql decode:true ">--Find Db Artifacts that uses the following Db Object
DECLARE @DbArtifactToLookUp AS VARCHAR(500) = 'DB_OBJECT_NAME_TO_SEARCH_GOES_HERE'; 
DECLARE @DbArtifactSchemaToLookUp AS VARCHAR(100) = 'dbo';

;
WITH    dependencies_cte
          AS ( SELECT   ParentSchema = OBJECT_SCHEMA_NAME(d.referencing_id) ,
                        ParentObjectName = OBJECT_NAME(d.referencing_id) ,
                        ChildSchema = d.referenced_schema_name ,
                        ChildObjectName = d.referenced_entity_name ,
                        TreeStructureList = CAST(d.referenced_schema_name
                        + '.' + d.referenced_entity_name + ' -&gt; '
                        + OBJECT_SCHEMA_NAME(d.referencing_id) + '.'
                        + OBJECT_NAME(d.referencing_id) AS VARCHAR(5000))
               FROM     sys.sql_expression_dependencies d
               WHERE    OBJECT_NAME(d.referenced_id) = @DbArtifactToLookUp
                        AND d.referenced_schema_name = @DbArtifactSchemaToLookUp
               UNION ALL
               SELECT   ParentSchema = OBJECT_SCHEMA_NAME(d.referencing_id) ,
                        ParentObjectName = OBJECT_NAME(d.referencing_id) ,
                        ChildSchema = d.referenced_schema_name ,
                        ChildObjectName = d.referenced_entity_name ,
                        TreeStructureList = CAST(dc.TreeStructureList + ' -&gt; '
                        + OBJECT_SCHEMA_NAME(d.referencing_id) + '.'
                        + OBJECT_NAME(d.referencing_id) AS VARCHAR(5000))
               FROM     sys.sql_expression_dependencies d
                        JOIN dependencies_cte dc ON OBJECT_NAME(d.referenced_id) = dc.ParentObjectName
                                                    AND d.referenced_schema_name = dc.ParentSchema
             )
    SELECT  dct.TreeStructureList
    FROM    dependencies_cte AS dct
    ORDER BY dct.TreeStructureList;    
</pre>

&nbsp;
