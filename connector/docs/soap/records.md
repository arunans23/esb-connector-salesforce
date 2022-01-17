# Working with Records in Salesforce

[[  Overview ]](#overview)  [[ Operation details ]](#operation-details) [ [Sample configuration](#sample-configuration) ]

### Overview 

The following operations allow you to work with Records. A Record is an instance of a particular sObject. Click an operation name to see details on how to use it.

| Operation        | Description |
| ------------- |-------------|
| [create](#creating-records)    | Creates records in Salesforce. |
| [update](#updating-records)      | Updates a record in Salesforce. |
| [upsert](#updating-and-inserting-records)    | Updates existing records and inserts a new record in a single operation. |
| [search](#searching-records)    | Search for records in Salesforce. |
| [query](#querying-records)      |  	Retrieves data from a record in Salesforce. |
| [retrieve](#retrieving-specific-records)    | Retrieves data from a record in Salesforce when the record ID is provided. |
| [delete](#deleting-records)    | Deletes a record in Salesforce. |
| [undelete](#restoring-records)      | Restores a record that was previously deleted in Salesforce. |
| [getDeleted](#retrieving-deleted-records)      | Retrieves the list of deleted records within a specified time interval. |
| [getUpdated](#retrieving-updated-records)      | Retrieves the list of updated records within a specified time interval. |
| [findDuplicates](#retrieving-duplicate-records)      | Retrieves the list of duplicate records in one or more sObjects. |
| [findDuplicatesByIds](#retrieving-duplicate-records-by-ids)      | Retrieves the list of duplicate records of given ids. |
| [merge](#merge-records)      | Merges records into one master record. |
| [ConvertLead](#convert-lead)      | Convert a lead into an account. |

### Operation details

This section provides further details on the operations related to records.


#### Creating records

To create one or more record, use salesforce.create-soap and specify the following properties. 

###### create
```xml
<salesforce.create-soap configKey="MySFConfig">
    <allOrNone>0</allOrNone>
    <allowFieldTruncate>0</allowFieldTruncate>
    <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.create-soap>
```
###### Properties
* allOrNone: Whether to rollback changes if an object fails (see Common Parameters).
* allowFieldTruncate: Whether to truncate strings that exceed the field length (see Common Parameters).
* sobjects: XML representation of the records to add.

###### Sample request

Given below is a sample request that can be handled by the create operation.

```xml
<payloadFactory>
    <format>
       <sfdc:sObjects xmlns:sfdc="sfdc" type="Account">
          <sfdc:sObject>
              <sfdc:Name>wso2123</sfdc:Name>
           </sfdc:sObject>
           <sfdc:sObject>
             <sfdc:Name>abc123</sfdc:Name>
           </sfdc:sObject>
        </sfdc:sObjects>
    </format>
    <args/>
</payloadFactory>
 
<salesforce.create-soap>
    <allOrNone>0</allOrNone>
    <allowFieldTruncate>0</allowFieldTruncate>
    <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.create-soap>
```

###### Sample response

Given below is a sample response for the create operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>9</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <createResponse>
            <result>
                <id>0036F00002mdwl2QAA</id>
                <success>true</success>
            </result>
        </createResponse>
    </soapenv:Body>
</soapenv:Envelope>
```

###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_create.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_create.htm)

#### Updating records

To update one or more existing records, use salesforce.update-soap and specify the following properties. 

###### update
```xml
<salesforce.update-soap configKey="MySFConfig">
    <allOrNone>0</allOrNone>
    <allowFieldTruncate>0</allowFieldTruncate>
    <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.update-soap>
```

###### Properties
* allOrNone: Whether to rollback changes if an object fails (see Common Parameters).
* allowFieldTruncate: Whether to truncate strings that exceed the field length (see Common Parameters).
* sobjects: XML representation of the records to add.

###### Sample request

Given below is a sample request that can be handled by the update operation.

```xml
<payloadFactory>
    <format>
        <sfdc:sObjects xmlns:sfdc="sfdc" type="Account">
          <sfdc:sObject>
             <sfdc:Id>0019000000aaMkZ</sfdc:Id>
             <sfdc:Name>newname01</sfdc:Name>
          </sfdc:sObject>
          <sfdc:sObject>
             <sfdc:Id>0019000000aaMkP</sfdc:Id>
             <sfdc:Name>newname02</sfdc:Name>
          </sfdc:sObject>
       </sfdc:sObjects>
    </format>
    <args/>
</payloadFactory>
 
<salesforce.update-soap>
    <allOrNone>0</allOrNone>
    <allowFieldTruncate>0</allowFieldTruncate>
    <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.update-soap>
```
###### Sample response

Given below is a sample response for the update operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>53</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <updateResponse>
            <result>
                <id>0016F00002S4Wj0QAF</id>
                <success>true</success>
            </result>
        </updateResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_update.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_update.htm)

#### Updating and inserting records

To update existing records and insert new records in a single operation, use salesforce.upsert-soap and specify the following properties. 

###### upsert
```xml
<salesforce.upsert-soap configKey="MySFConfig">
    <allOrNone>0</allOrNone>
    <allowFieldTruncate>0</allowFieldTruncate>
    <externalId>Id</externalId>
    <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.upsert-soap>
```

###### Properties
* allOrNone: Whether to rollback changes if an object fails (see Common Parameters).
* allowFieldTruncate: Whether to truncate strings that exceed the field length (see Common Parameters).
* externalId: The field containing the record ID, that is used by Salesforce to determine whether to update an existing record or create a new one. This is done by matching the ID to the record IDs in Salesforce. By default, the field is assumed to be named "Id".
* sObjects: XML representation of the records to update and insert. When inserting a new record, you do not specify sfdc:Id.

---
**Set the externalId field :**
If you need to give any existing externalId field of sObject to externalId then the payload should be with that externalId field and value as follows in sample
---
###### Sample to set ExternalId field and value


```xml
<payloadFactory>
    <format>
        <sfdc:sObjects xmlns:sfdc="sfdc" type="Account">
          <sfdc:sObject>
             <sfdc:sample__c>{any value}</sfdc:sample__c>
             <sfdc:Name>newname001</sfdc:Name>
          </sfdc:sObject>
       </sfdc:sObjects>
    </format>
    <args/>
</payloadFactory>
 
<salesforce.upsert-soap>
    <allOrNone>0</allOrNone>
    <allowFieldTruncate>0</allowFieldTruncate>
    <externalId>sample__c</externalId>
    <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.upsert-soap>
```

###### Sample request

Given below is a sample request that can be handled by the upsert operation.

```xml
<payloadFactory>
    <format>
        <sfdc:sObjects xmlns:sfdc="sfdc" type="Account">
          <sfdc:sObject>
             <sfdc:Id>0019000000aaMkZ</sfdc:Id>
             <sfdc:Name>newname001</sfdc:Name>
          </sfdc:sObject>
          <sfdc:sObject>
             <sfdc:Name>newname002</sfdc:Name>
          </sfdc:sObject>
       </sfdc:sObjects>
    </format>
    <args/>
</payloadFactory>
 
<salesforce.upsert-soap>
    <allOrNone>0</allOrNone>
    <allowFieldTruncate>0</allowFieldTruncate>
    <externalId>Id</externalId>
    <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.upsert-soap>
```

###### Sample response

Given below is a sample response for the upsert operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>54</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <upsertResponse>
            <result>
                <created>false</created>
                <id>0016F00002S4Wj0QAF</id>
                <success>true</success>
            </result>
            <result>
                <created>true</created>
                <id>0016F00002pUVTMQA4</id>
                <success>true</success>
            </result>
        </upsertResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_upsert.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_upsert.htm)

#### Searching records

To search for records, use salesforce.search-soap and specify the search string. If you already know the record IDs, use retrieve instead. 

###### search
```xml
<salesforce.search-soap configKey="MySFConfig">
    <searchString>FIND {map*} IN ALL FIELDS RETURNING Account (Id, Name), Contact, Opportunity, Lead</searchString>
</salesforce.search-soap>
```
###### Properties
* searchString: The SQL query to use to search for records.

###### Sample response

Given below is a sample response for the search operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com" xmlns:sf="urn:sobject.partner.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>56</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <searchResponse>
            <result>
                <searchRecords>
                    <record xsi:type="sf:sObject">
                        <sf:type>Account</sf:type>
                        <sf:Id>0016F00002SN7qiQAD</sf:Id>
                        <sf:Id>0016F00002SN7qiQAD</sf:Id>
                        <sf:Name>GenePoint</sf:Name>
                    </record>
                </searchRecords>
            </result>
        </searchResponse>
    </soapenv:Body>
</soapenv:Envelope>
```

###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_search.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_search.htm)

#### Querying records

To retrieve data from an object, use salesforce.query-soap and specify the following properties. If you already know the record IDs, you can use retrieve instead. 

---
**Note :**
If you want your search results to include deleted records that are available in the Recycle Bin, use salesforce.query-soapAll in place of salesforce.query-soap.
---

###### query
```xml
<salesforce.query-soap configKey="MySFConfig">
    <batchSize>200</batchSize>
    <queryString>select id,name from Account</queryString>
</salesforce.query-soap>
```

###### Properties
* batchSize: The number of records to return. If more records are available than the batch size, you can use the queryMore operation to get additional results.
* queryString: The SQL query to use to search for records.

###### Sample request

Following is a sample configuration to query records. It also illustrates the use of queryMore operation to get additional results:

```xml
<salesforce.query-soap>
    <batchSize>200</batchSize>
    <queryString>select id,name from Account</queryString>
</salesforce.query-soap>
<!-- Execute the following to get the other batches -->
<iterate xmlns:sfdc="http://wso2.org/salesforce/adaptor" continueParent="true" expression="//sfdc:iterator">
    <target>
        <sequence>
            <salesforce.queryMore-soap>
                <batchSize>200</batchSize>
            </salesforce.queryMore-soap>
        </sequence>
    </target>
</iterate>
```

###### Sample response

Given below is a sample response for the query operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com" xmlns:sf="urn:sobject.partner.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>58</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <queryResponse>
            <result xsi:type="QueryResult">
                <done>true</done>
                <queryLocator xsi:nil="true"/>
                <records xsi:type="sf:sObject">
                    <sf:type>Account</sf:type>
                    <sf:Id>0016F00002SasNYQAZ</sf:Id>
                    <sf:Id>0016F00002SasNYQAZ</sf:Id>
                    <sf:Name>wso2New</sf:Name>
                </records>
                .
                .
                <size>129</size>
            </result>
        </queryResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_query.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_query.htm)

#### Retrieving specific records

If you know the IDs of the records you want to retrieve, use salesforce.retrieve-soap and specify the following properties. If you do not know the record IDs, use query instead.

###### retrieve
```xml
<salesforce.retrieve-soap configKey="MySFConfig">
    <fieldList>id,name</fieldList>
    <objectType>Account</objectType>
    <objectIDS xmlns:sfdc="sfdc">{//sfdc:sObjects}</objectIDS>
</salesforce.retrieve-soap>
```

###### Properties
* fieldList: A comma-separated list of the fields you want to retrieve from the records.
* objectType: The object type of the records.
* sobjects: XML representation of the records to retrieve.

###### Sample request

Given below is a sample request that can be handled by the retrieve operation.

```xml
<payloadFactory>
   <format>
      <sfdc:sObjects xmlns:sfdc="sfdc">
         <sfdc:Ids>0019000000aaMkK</sfdc:Ids>
         <sfdc:Ids>0019000000aaMjl</sfdc:Ids>
      </sfdc:sObjects>
   </format>
   <args/>
</payloadFactory>
 
<salesforce.retrieve-soap configKey="MySFConfig">
    <fieldList>id,name</fieldList>
    <objectType>Account</objectType>
    <objectIDS xmlns:sfdc="sfdc">{//sfdc:sObjects}</objectIDS>
</salesforce.retrieve-soap>
```

###### Sample response

Given below is a sample response for the retrieve operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com" xmlns:sf="urn:sobject.partner.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>60</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <retrieveResponse>
            <result xsi:type="sf:sObject">
                <sf:type>Account</sf:type>
                <sf:Id>0016F00002S4Wj0QAF</sf:Id>
                <sf:Id>0016F00002S4Wj0QAF</sf:Id>
                <sf:Name>newname01</sf:Name>
            </result>
        </retrieveResponse>
    </soapenv:Body>
</soapenv:Envelope>
```

###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_retrieve.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_retrieve.htm)

#### Deleting records

To delete one or more records, use salesforce.delete-soap and specify the following properties. 

###### delete
```xml
<salesforce.delete-soap configKey="MySFConfig">
   <allOrNone>0</allOrNone>
   <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.delete-soap>
```

###### Properties
* allOrNone: Whether to rollback changes if an object fails (see Common Parameters).
* sobjects: XML representation of the records to delete, as shown in the following example.

###### Sample request

Given below is a sample request that can be handled by the delete operation.

```xml
<payloadFactory>
   <format>
     <sfdc:sObjects xmlns:sfdc="sfdc">
         <sfdc:Ids>0019000000aaMkZ</sfdc:Ids>
         <sfdc:Ids>0019000000aaMkP</sfdc:Ids>
      </sfdc:sObjects>
   </format>
   <args/>
</payloadFactory>
 
<salesforce.delete-soap>
   <allOrNone>0</allOrNone>
   <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.delete-soap>
```
###### Sample response

Given below is a sample response for the delete operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>63</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <deleteResponse>
            <result>
                <id>0016F00002S4Wj0QAF</id>
                <success>true</success>
            </result>
        </deleteResponse>
    </soapenv:Body>
</soapenv:Envelope>
```

###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_delete.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_delete.htm)

#### Restoring records

To restore records that were previously deleted, use salesforce.undelete-soap and specify the following properties. 

###### undelete
```xml
<salesforce.undelete-soap configKey="MySFConfig">
    <allOrNone>0</allOrNone>
    <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.undelete-soap>
```

###### Properties
* allOrNone: Whether to rollback changes if an object fails (see Common Parameters).
* sobjects: XML representation of the records to restore, as shown in the following example.

###### Sample request

Given below is a sample request that can be handled by the undelete operation.

```xml
<payloadFactory>
   <format>
      <sfdc:sObjects xmlns:sfdc="sfdc">
         <sfdc:Ids>0019000000aaMkZ</sfdc:Ids>
         <sfdc:Ids>0019000000aaMkP</sfdc:Ids>
      </sfdc:sObjects>
    </format>
    <args/>
</payloadFactory>
 
<salesforce.undelete-soap>
    <allOrNone>0</allOrNone>
    <sobjects xmlns:sfdc="sfdc">{//sfdc:sObjects}</sobjects>
</salesforce.undelete-soap>
```
###### Sample response

Given below is a sample response for the undelete operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>64</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <undeleteResponse>
            <result>
                <id>0016F00002S4Wj0QAF</id>
                <success>true</success>
            </result>
        </undeleteResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_undelete.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_undelete.htm)

#### Retrieving Deleted records

To retrieve the list of records that were previously deleted, use salesforce.getDeleted-soap and specify the following properties. 

###### getDeleted
```xml
<salesforce.getDeleted-soap configKey="MySFConfig">
    <sObjectType>{$ctx:sObjectType}</sObjectType>
    <startDate>{$ctx:startDate}</startDate>
    <endDate>{$ctx:endDate}</endDate>
</salesforce.getDeleted>
```

###### Properties
* sObjectType: sObjectType from which we need to retrieve deleted records
* startDate: start date and time for deleted records lookup
* endDate: end date and time for deleted records lookup

###### Sample request

Given below is a sample request that can be handled by the getDeleted operation.

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:urn="wso2.connector.salesforce">
    <soapenv:Header/>
    <soapenv:Body>
        <urn:loginUrl>https://login.salesforce.com/services/Soap/u/30.0</urn:loginUrl>
        <urn:username>XXXXXXXXXX</urn:username>
        <urn:password>XXXXXXXXXX</urn:password>
        <urn:blocking>false</urn:blocking>
        <urn:sObjectType>Account</urn:sObjectType>
        <urn:startDate>2020-06-15T05:05:53+0000</urn:startDate>
        <urn:endDate>2020-06-30T05:05:53+0000</urn:endDate>
    </soapenv:Body>
</soapenv:Envelope> 
```
###### Sample response

Given below is a sample response for the getDeleted operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>55</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <getDeletedResponse>
            <result>
                <deletedRecords>
                    <deletedDate>2020-06-18T04:10:20.000Z</deletedDate>
                    <id>0012x000007RqnHAAS</id>
                </deletedRecords>
                <earliestDateAvailable>2020-04-27T13:43:00.000Z</earliestDateAvailable>
                <latestDateCovered>2020-06-30T05:05:00.000Z</latestDateCovered>
            </result>
        </getDeletedResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_getdeleted.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_getdeleted.htm)

#### Retrieving Updated records

To retrieve the list of records that were previously updated, use salesforce.getUpdated-soap and specify the following properties. 

###### getUpdated
```xml
<salesforce.getUpdated-soap configKey="MySFConfig">
    <sObjectType>{$ctx:sObjectType}</sObjectType>
    <startDate>{$ctx:startDate}</startDate>
    <endDate>{$ctx:endDate}</endDate>
</salesforce.getUpdated-soap>
```

###### Properties
* sObjectType: sObjectType from which we need to retrieve deleted records
* startDate: start date and time for deleted records lookup
* endDate: end date and time for deleted records lookup

###### Sample request

Given below is a sample request that can be handled by the getUpdated operation.

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:urn="wso2.connector.salesforce">
    <soapenv:Header/>
    <soapenv:Body>
        <urn:loginUrl>https://login.salesforce.com/services/Soap/u/30.0</urn:loginUrl>
        <urn:username>XXXXXXXXXX</urn:username>
        <urn:password>XXXXXXXXXX</urn:password>
        <urn:blocking>false</urn:blocking>
        <urn:sObjectType>Account</urn:sObjectType>
        <urn:startDate>2020-06-15T05:05:53+0000</urn:startDate>
        <urn:endDate>2020-06-30T05:05:53+0000</urn:endDate>
    </soapenv:Body>
</soapenv:Envelope> 
```
###### Sample response

Given below is a sample response for the getUpdated operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>66</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <getUpdatedResponse>
            <result>
                <ids>0012x000007RVCcAAO</ids>
                <ids>0012x000007RVD1AAO</ids>
                <ids>0012x000007RVG8AAO</ids>
                <ids>0012x000007RVw7AAG</ids>
                <ids>0012x000007RW3uAAG</ids>
                <latestDateCovered>2020-06-30T05:05:00.000Z</latestDateCovered>
            </result>
        </getUpdatedResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_getupdated.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_getupdated.htm)


#### Retrieving Duplicate records

To retrieve the list of records that are duplicate entries, use salesforce.findDuplicates-soap and specify the following properties. 

###### findDuplicates
```xml
<salesforce.findDuplicates-soap configKey="MySFConfig">
    <sobjects xmlns:ns="wso2.connector.salesforce">{//ns:sObjects}</sobjects>
</salesforce.findDuplicates-soap>
```

###### Properties
* sobjects: sObjectType from which we need to retrieve duplicate records

###### Sample request

Given below is a sample request that can be handled by the findDuplicates operation.

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:urn="wso2.connector.salesforce">
    <soapenv:Header/>
    <soapenv:Body>
        <urn:loginUrl>https://login.salesforce.com/services/Soap/u/48.0</urn:loginUrl>
        <urn:username>XXXXXXXXXXXX</urn:username>
        <urn:password>XXXXXXXXXXXX</urn:password>
        <urn:blocking>false</urn:blocking>
        <urn:sObjects>
        	<urn:sObject>
        		<urn:type>Account</urn:type>
        		<urn:fieldsToNull>name</urn:fieldsToNull>
        		<urn:fieldsToNull>id</urn:fieldsToNull>
        	</urn:sObject>
        </urn:sObjects>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Sample response

Given below is a sample response for the findDuplicates operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>11</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <findDuplicatesResponse>
            <result>
                <duplicateResults>
                    <allowSave>false</allowSave>
                    <duplicateRule>Standard_Account_Duplicate_Rule</duplicateRule>
                    <duplicateRuleEntityType>Account</duplicateRuleEntityType>
                    <errorMessage xsi:nil="true"/>
                    <matchResults>
                        <entityType>Account</entityType>
                        <matchEngine>FuzzyMatchEngine</matchEngine>
                        <rule>Standard_Account_Match_Rule_v1_0</rule>
                        <size>0</size>
                        <success>true</success>
                    </matchResults>
                </duplicateResults>
                <success>true</success>
            </result>
        </findDuplicatesResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_findduplicates.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_findduplicates.htm)


#### Retrieving Duplicate records by IDs

To retrieve the list of records that are duplicate entries by using ids, use salesforce.findDuplicatesByIds-soap and specify the following properties. 

###### findDuplicatesByIds
```xml
<salesforce.findDuplicatesByIds-soap configKey="MySFConfig">
    <ids xmlns:ns="wso2.connector.salesforce">{//ns:ids}</ids>
</salesforce.findDuplicatesByIds-soap>
```

###### Properties
* ids: ids for which duplicate records need to be found

###### Sample request

Given below is a sample request that can be handled by the findDuplicatesByIds operation.

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:urn="wso2.connector.salesforce">
    <soapenv:Header/>
    <soapenv:Body>
        <urn:loginUrl>https://login.salesforce.com/services/Soap/u/48.0</urn:loginUrl>
        <urn:username>XXXXXXXXXX</urn:username>
        <urn:password>XXXXXXXXXX</urn:password>
        <urn:blocking>false</urn:blocking>
        <urn:ids>
        	<urn:id>0012x000005mqKuAAI</urn:id>
        	<urn:id>0012x000005orjlAAA</urn:id>
        </urn:ids>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Sample response

Given below is a sample response for the findDuplicates operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>53</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <findDuplicatesByIdsResponse>
            <result>
                <duplicateResults>
                    <allowSave>false</allowSave>
                    <duplicateRule>Standard_Account_Duplicate_Rule</duplicateRule>
                    <duplicateRuleEntityType>Account</duplicateRuleEntityType>
                    <errorMessage xsi:nil="true"/>
                    <matchResults>
                        <entityType>Account</entityType>
                        <matchEngine>FuzzyMatchEngine</matchEngine>
                        <rule>Standard_Account_Match_Rule_v1_0</rule>
                        <size>0</size>
                        <success>true</success>
                    </matchResults>
                </duplicateResults>
                <success>true</success>
            </result>
        </findDuplicatesByIdsResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_findduplicatesbyids.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_findduplicatesbyids.htm)


#### Merge Records

To merge records into one master record, use salesforce.merge-soap and specify the following properties. 

###### merge
```xml
<salesforce.merge-soap configKey="MySFConfig">
    <mergerequests xmlns:ns="wso2.connector.salesforce">{//ns:requests}</mergerequests>
</salesforce.merge-soap>
```

###### Properties
* mergerequests: The merge requests according to the format defined in to Salesforce docs (See Related Salesforce documentation section)

###### Sample request

Given below is a sample request that can be handled by the merge operation.

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:urn="wso2.connector.salesforce">
    <soapenv:Header/>
    <soapenv:Body>
        <urn:loginUrl>https://login.salesforce.com/services/Soap/u/48.0</urn:loginUrl>
        <urn:username>XXXXXXXXXXX</urn:username>
        <urn:password>XXXXXXXXXXX</urn:password>
        <urn:blocking>false</urn:blocking>
        <urn:requests>
            <urn:request>
                <urn:masterRecord>
                    <urn:type>Account</urn:type>
                    <urn:Id>0012x000008un5bAAA</urn:Id>
                </urn:masterRecord>
                <urn:recordToMergeIds>0012x000008un5lAAA</urn:recordToMergeIds>
            </urn:request>
        </urn:requests>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Sample response

Given below is a sample response for the findDuplicates operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>70</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <mergeResponse>
            <result>
                <id>0012x000008un5bAAA</id>
                <mergedRecordIds>0012x000008un5lAAA</mergedRecordIds>
                <success>true</success>
            </result>
        </mergeResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_merge.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_merge.htm)


#### Convert Lead

To convert a lead into an account, use salesforce.ConvertLead-soap and specify the following properties. 

###### convertLead
```xml
<salesforce.ConvertLead-soap configKey="MySFConfig">
     <leadconvertrequests xmlns:ns="wso2.connector.salesforce">{//ns:leadconvertrequests}</leadconvertrequests>
</salesforce.ConvertLead-soap>
```

###### Properties
* leadconvertrequests: The lead convert requests according to the format defined in to Salesforce docs (See Related Salesforce documentation section)

###### Sample request

Given below is a sample request that can be handled by the convertLead operation.

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:urn="wso2.connector.salesforce">
    <soapenv:Header/>
    <soapenv:Body>
        <urn:loginUrl>https://login.salesforce.com/services/Soap/u/48.0</urn:loginUrl>
        <urn:username>XXXXXXXXXX</urn:username>
        <urn:password>XXXXXXXXXX</urn:password>
        <urn:blocking>false</urn:blocking>
        <urn:leadconvertrequests>
        	<urn:leadConverts>
        		<urn:accountId>0012x000005mqKuAAI</urn:accountId>
        		<urn:leadId>00Q2x00000AH981EAD</urn:leadId>
        		<urn:convertedStatus>Closed - Converted</urn:convertedStatus>
        	</urn:leadConverts>
        </urn:leadconvertrequests>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Sample response

Given below is a sample response for the convertLead operation.

```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>128</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <convertLeadResponse>
            <result>
                <accountId>0012x000005mqKuAAI</accountId>
                <contactId>0032x000006I2xYAAS</contactId>
                <leadId>00Q2x00000AH981EAD</leadId>
                <opportunityId>0062x0000053r8FAAQ</opportunityId>
                <success>true</success>
            </result>
        </convertLeadResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
###### Related Salesforce documentation

[https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_merge.htm](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_calls_merge.htm)


### Sample configuration

Following example illustrates how to connect to Salesforce with the init operation and query operation.

1. Create a sample proxy as below :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxy xmlns="http://ws.apache.org/ns/synapse"
       name="salesforce_query"
       startOnLoad="true"
       statistics="disable"
       trace="disable"
       transports="http,https">
   <target>
      <inSequence>
         <property xmlns:ns="wso2.connector.salesforce"
                   expression="//ns:loginUrl/text()"
                   name="loginUrl"/>
         <property xmlns:ns="wso2.connector.salesforce"
                   expression="//ns:username/text()"
                   name="username"/>
         <property xmlns:ns="wso2.connector.salesforce"
                   expression="//ns:password/text()"
                   name="password"/>
         <property xmlns:ns="wso2.connector.salesforce"
                   expression="//ns:blocking/text()"
                   name="blocking"/>
         <property xmlns:ns="wso2.connector.salesforce"
                   expression="//ns:batchSize/text()"
                   name="batchSize"/>
         <property xmlns:ns="wso2.connector.salesforce"
                   expression="//ns:queryString/text()"
                   name="queryString"/>
         <salesforce.init>
            <loginUrl>{$ctx:loginUrl}</loginUrl>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
            <blocking>{$ctx:blocking}</blocking>
            <connectionType>basicAuth</connectionType>
         </salesforce.init>
         <salesforce.query-soap>
            <batchSize>{$ctx:batchSize}</batchSize>
            <queryString>{$ctx:queryString}</queryString>
         </salesforce.query-soap>
         <respond/>
      </inSequence>
      <outSequence>
         <send/>
      </outSequence>
   </target>
   <description/>
</proxy>
                                                             
```
2. Create an XML file named query.xml and copy the XML configurations given below:

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:urn="wso2.connector.salesforce">
    <soapenv:Header/>
    <soapenv:Body>
        <urn:loginUrl>https://login.salesforce.com/services/Soap/u/30.0</urn:loginUrl>
        <urn:username>john@gmail.com</urn:username>
        <urn:password>john@123CtGoiPE3mCdjgUHlto8HJ3</urn:password>
        <urn:blocking>false</urn:blocking>
        <urn:queryString>select id,name from Account</urn:queryString>
        <urn:batchSize>2000</urn:batchSize>
    </soapenv:Body>
</soapenv:Envelope>                           
```
3. Replace the credentials with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/salesforce_query -H "Content-Type: text/xml" -d @query.xml
```
5. Salesforce returns an XML response similar to the response given below:
 
```xml
<?xml version='1.0' encoding='utf-8'?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com" xmlns:sf="urn:sobject.partner.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <soapenv:Header>
        <LimitInfoHeader>
            <limitInfo>
                <current>58</current>
                <limit>15000</limit>
                <type>API REQUESTS</type>
            </limitInfo>
        </LimitInfoHeader>
    </soapenv:Header>
    <soapenv:Body>
        <queryResponse>
            <result xsi:type="QueryResult">
                <done>true</done>
                <queryLocator xsi:nil="true"/>
                <records xsi:type="sf:sObject">
                    <sf:type>Account</sf:type>
                    <sf:Id>0016F00002SasNYQAZ</sf:Id>
                    <sf:Id>0016F00002SasNYQAZ</sf:Id>
                    <sf:Name>wso2New</sf:Name>
                </records>
                .
                .
                <size>129</size>
            </result>
        </queryResponse>
    </soapenv:Body>
</soapenv:Envelope>
```
