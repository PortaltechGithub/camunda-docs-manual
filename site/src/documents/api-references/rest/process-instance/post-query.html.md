---

title: 'Get Instances (POST)'
category: 'Process Instance'

keywords: 'post query list'

---


Query for process instances that fulfill given parameters through a json object.
This method is slightly more powerful than the [GET query](ref:#process-instance-get-instances), because it allows
to filter by multiple process variables of types `String`, `Number` or `Boolean`.


Method
------

POST `/process-instance`


Parameters
----------

#### Query Parameters

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>firstResult</td>
    <td>Pagination of results. Specifies the index of the first result to return.</td>
  </tr>
  <tr>
    <td>maxResults</td>
    <td>Pagination of results. Specifies the maximum number of results to return. Will return less results, if there are no more results left.</td>
  </tr>
</table>  

#### Request Body

<p>
  A json object with the following properties:
</p>
<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>processInstanceIds</td>
    <td>Filter by a list of process instance ids. Must be a json array of Strings.</td>
  </tr>
  <tr>
    <td>businessKey</td>
    <td>Filter by process instance business key.</td>
  </tr>
  <tr>
    <td>processDefinitionId</td>
    <td>Filter by the process definition the instances run on.</td>
  </tr>
  <tr>
    <td>processDefinitionKey</td>
    <td>Filter by the key of the process definition the instances run on.</td>
  </tr>
  <tr>
    <td>superProcessInstance</td>
    <td>Restrict query to all process instances that are sub process instances of the given process instance. Takes a process instance id.</td>
  </tr>
  <tr>
    <td>subProcessInstance</td>
    <td>Restrict query to all process instances that have the given process instance as a sub process instance. Takes a process instance id.</td>
  </tr>
  <tr>
    <td>active</td>
    <td>Only include active process instances. Values may be <code>true</code> or <code>false</code>.</td>
  </tr>
  <tr>
    <td>suspended</td>
    <td>Only include suspended process instances. Values may be <code>true</code> or <code>false</code>.</td>
  </tr>
  <tr>
    <td>incidentId</td>
    <td>Filter by the incident id.</td>
  </tr>
  <tr>
    <td>incidentType</td>
    <td>Filter by the incident type.</td>
  </tr>
  <tr>
    <td>incidentMessage</td>
    <td>Filter by the incident message. Exact match.</td>
  </tr>
  <tr>
    <td>incidentMessageLike</td>
    <td>Filter by the incident message that the parameter is a substring of.</td>
  </tr>
  <tr>
    <td>variables</td>
    <td>A json array to only include process instances that have variables with certain values. <br/>
    The array consists of objects with the three properties <code>name</code>, <code>operator</code> and <code>value</code>.
    <code>name (String)</code> is the variable name, <code>operator (String)</code> is the comparison operator to be used and <code>value</code> the variable value.<br/>
    <code>value</code> may be <code>String</code>, <code>Number</code> or <code>Boolean</code>.
    <br/>
    Valid operator values are: <code>eq</code> - equals; <code>neq</code> - not equals; <code>gt</code> - greater than;
    <code>gteq</code> - greater than or equals; <code>lt</code> - lower than; <code>lteq</code> - lower than or equals;
    <code>like</code>.<br/>
    </td>
  </tr>
  <tr>
    <td>sortBy</td>
    <td>Sort the results lexicographically by a given criterion. Valid values are
    <code>instanceId</code>, <code>definitionKey</code> and <code>definitionId</code>.
    Must be used in conjunction with the <code>sortOrder</code> parameter.</td>
  </tr>
  <tr>
    <td>sortOrder</td>
    <td>Sort the results in a given order. Values may be <code>asc</code> for ascending order or <code>desc</code> for descending order.
    Must be used in conjunction with the <code>sortBy</code> parameter.</td>
  </tr>
</table>


Result
------

A json array of process instance objects.
Each process instance object has the following properties:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>String</td>
    <td>The id of the process instance.</td>
  </tr>
  <tr>
    <td>definitionId</td>
    <td>String</td>
    <td>The id of the process definition that this process instance belongs to.</td>
  </tr>
  <tr>
    <td>businessKey</td>
    <td>String</td>
    <td>The business key of the process instance.</td>
  </tr>
  <tr>
    <td>ended</td>
    <td>Boolean</td>
    <td>
      A flag indicating whether the process instance has ended.
      <em>Deprecated: will always be false!</em>
    </td>
  </tr>
  <tr>
    <td>suspended</td>
    <td>Boolean</td>
    <td>A flag indicating whether the process instance is suspended.</td>
  </tr>
</table>


Response codes
--------------

<table class="table table-striped">
  <tr>
    <th>Code</th>
    <th>Media type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>200</td>
    <td>application/json</td>
    <td>Request successful.</td>
  </tr>
  <tr>
    <td>400</td>
    <td>application/json</td>
    <td>Returned if some of the query parameters are invalid, for example if a <code>sortOrder</code> parameter is supplied, but no <code>sortBy</code>
    or if an invalid operator for variable comparison is used. See the <a href="ref:#overview-introduction">Introduction</a> for the error response format.</td>
  </tr>
</table>


Example
-------

#### Request

POST `/process-instance`

Request body:

    {"variables": 
        [{"name": "myVariable",
         "operator": "eq",
         "value": "camunda"
        },
        {"name": "mySecondVariable",
         "operator": "neq",
         "value": 124}],
    "processDefinitionId":"aProcessDefinitionId"}

#### Response

    [{"links":[],
     "id":"anId",
     "definitionId":"aProcessDefinitionId",
     "businessKey":"aKey",
     "ended":false,
     "suspended":false}]