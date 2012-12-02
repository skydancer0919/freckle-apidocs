---
layout: default
---
Projects
========

List projects
-------------

The projects resource returns all projects accessible by the user. For all roles except freelancer this includes all projects in the account. Freelancers see all projects they have access to.

GET `/api/projects.xml`

Sample request:

    curl -H "X-FreckleToken:lx3gi6pxdjtjn57afp8c2bv1me7g89j" https://apitest.letsfreckle.com/api/projects.xml

Sample XML response:

    <?xml version="1.0" encoding="UTF-8"?>
    <projects type="array">
      <project>
        <account-id type="integer">100</account-id>
        <billable type="boolean">true</billable>
        <budget type="integer" nil="true"></budget>
        <created-at type="datetime">2008-12-19T16:21:34Z</created-at>
        <enabled type="boolean">true</enabled>
        <id type="integer">1343</id>
        <import-id type="integer">6</import-id>
        <invoice-recipient-details nil="true"/>
        <name>TestProject1</name>
        <stepping type="integer">15</stepping>
        <updated-at type="datetime">2008-12-19T16:21:34Z</updated-at>
        <user-id type="integer" nil="true"></user-id>
        <minutes type="integer">900</minutes>
        <budget-minutes nil="true"/>
        <remaining-minutes nil="true"/>
        <unbillable-minutes type="integer">0</unbillable-minutes>
      </project>
      <project>
        <account-id type="integer">100</account-id>
        <billable type="boolean">true</billable>
        <budget type="integer" nil="true"></budget>
        <created-at type="datetime">2008-12-19T16:23:06Z</created-at>
        <enabled type="boolean">true</enabled>
        <id type="integer">1344</id>
        <import-id type="integer" nil="true"/>
        <invoice-recipient-details nil="true"/>        
        <name>TestProject2</name>
        <stepping type="integer">15</stepping>
        <updated-at type="datetime">2008-12-19T16:23:06Z</updated-at>
        <user-id type="integer" nil="true"></user-id>
        <minutes type="integer">615</minutes>
        <budget-minutes type="integer">900</budget-minutes>
        <remaining-minutes type="integer">285</remaining-minutes>
        <unbillable-minutes type="integer">0</unbillable-minutes>
      </project>
    </projects>

### Response codes

* 401 Unauthorized

  The user is not authorized to access this information or the authentication token is not valid.

* 500 Internal Server Error

  An error occurred. The API call was not processed correctly and should be retried later.

### Roles

Everyone has access to this resource.

Show project
-------------

GET `/api/projects/2.xml`

Sample request:

    curl -H "X-FreckleToken:lx3gi6pxdjtjn57afp8c2bv1me7g89j" https://apitest.letsfreckle.com/api/projects/2.xml

Sample XML response:

    <?xml version="1.0" encoding="UTF-8"?>
    <project>
      <account-id type="integer">100</account-id>
      <billable type="boolean">true</billable>
      <budget type="integer" nil="true"></budget>
      <created-at type="datetime">2008-12-19T16:21:34Z</created-at>
      <enabled type="boolean">true</enabled>
      <id type="integer">1343</id>
      <import-id type="integer">6</import-id>
      <invoice-recipient-details nil="true"/>
      <name>TestProject1</name>
      <stepping type="integer">15</stepping>
      <updated-at type="datetime">2008-12-19T16:21:34Z</updated-at>
      <user-id type="integer" nil="true"></user-id>
      <minutes type="integer">615</minutes>
      <budget-minutes type="integer">900</budget-minutes>
      <remaining-minutes type="integer">285</remaining-minutes>
      <unbillable-minutes type="integer">0</unbillable-minutes>
    </project>

### Response codes

* 401 Unauthorized

  The user is not authorized to access this information or the authentication token is not valid.

* 404 Not Found

  An error occurred. Project with given id not exists.

* 500 Internal Server Error

  An error occurred. The API call was not processed correctly and should be retried later.

### Roles

Everyone has access to this resource.

Activate project
-------------

GET `/api/projects/2/active.xml`

Sample request:

    curl -H "X-FreckleToken:lx3gi6pxdjtjn57afp8c2bv1me7g89j" https://apitest.letsfreckle.com/api/projects/2/active.xml

In case the project was successfully activated, you get a `HTTP 200 Ok` back, with the `Location` header containing the URL of the project (e.g. https://apitest.letsfreckle.com/api/project/2).

### Response codes

* 401 Unauthorized

  The user is not authorized to access this information or the authentication token is not valid.

* 404 Not Found

  An error occurred. Project with given id not exists.

* 500 Internal Server Error

  An error occurred. The API call was not processed correctly and should be retried later.

### Roles

Everyone except freelancers can activate projects.

Archive project
-------------

GET `/api/projects/2/archive.xml`

Sample request:

    curl -H "X-FreckleToken:lx3gi6pxdjtjn57afp8c2bv1me7g89j" https://apitest.letsfreckle.com/api/projects/2/archive.xml

In case the project was successfully archived, you get a `HTTP 200 Ok` back, with the `Location` header containing the URL of the project (e.g. https://apitest.letsfreckle.com/api/project/2).

### Response codes

* 401 Unauthorized

  The user is not authorized to access this information or the authentication token is not valid.

* 404 Not Found

  An error occurred. Project with given id not exists.

* 500 Internal Server Error

  An error occurred. The API call was not processed correctly and should be retried later.

### Roles

Everyone except freelancers can archive projects.

Add project
-----------

POST `/api/projects.xml`

Sample request:

    curl -d @data/project.xml -H "Content-type: text/xml" -H "X-FreckleToken:lx3gi6pxdjtjn57afp8c2bv1me7g89j" \
      https://apitest.letsfreckle.com/api/projects.xml

Sample POST body:

    <?xml version="1.0" encoding="UTF-8"?>
    <project>
      <name>foobar</name>
    </project>

In case the project was successfully created, you get a `HTTP 201 Created` back, with the `Location` header containing the URL of the project (e.g. https://apitest.letsfreckle.com/api/project/123).

### Response codes

* 401 Unauthorized

  The user is not authorized to access this information or the authentication token is not valid.

* 422 Unprocessable Entity

  An error occurred. The project already exists or the account project limit has been reached

* 500 Internal Server Error

  An error occurred. The API call was not processed correctly and should be retried later.

### Roles

Everyone except freelancers can create projects.

Remove project
-----------

Removed can be only projects without any entries, expenses and invoices.

DELETE `/api/projects/2.xml`

Sample request:

    curl -X DELETE -H "X-FreckleToken:lx3gi6pxdjtjn57afp8c2bv1me7g89j" https://apitest.letsfreckle.com/api/projects/2.xml


In case the project was successfully removed, you get a `HTTP 200 Ok` back, with the `Location` header containing the URL of the project (e.g. https://apitest.letsfreckle.com/api/project/123).

### Response codes

* 401 Unauthorized

  The user is not authorized to access this information or the authentication token is not valid.

* 404 Not Found

  An error occurred. Project with given id not exists.

* 422 Unprocessable Entity

  An error occurred. The project have some entries, expenses or invoices.

* 500 Internal Server Error

  An error occurred. The API call was not processed correctly and should be retried later.

### Roles

Everyone except freelancers can remove projects.