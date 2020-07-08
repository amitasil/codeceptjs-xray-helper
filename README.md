# codeceptjs-xray-helper

codeceptjs-xray-helper is a [CodeceptJS](https://codecept.io/) helper which can publish tests results on [XRAY api](https://confluence.xpand-it.com/display/XRAYCLOUD/Import+Execution+Results+-+REST) after tests execution.

## Installation

```sh
npm install codeceptjs-xray-helper --save
```

## Configuration

This plugin should be added in `codecept.json/codecept.conf.js`

Example:

```js
{
  ...
   plugins: {
    xrayReport: {
       require: "codeceptjs-xray-helper",
       enabled: true,
       debug:false,
       jira_url: 'https://localhost-jira',
       jira_user: 'root',
       jira_password: 'root',
       test_revison: '001',
       testEnvironments: '["browser:chrome", "linux"]'
    }
  ...
}
```

##### To use this plugin you need to provide the following infos:

##### _jira_url_
Your JIRA host url for exemple: `http://localhost:8080`

##### _jira_user & jira_password_
Your JIRA user keys

##### _test_revison_
You can send your test revision (it could be your feature name for example).
If this config is empty `001` will be sent to xray instead
 ![test_revison_example](./doc/revision.jpeg)
 
 
##### _testEnvironments_
Test environnement that will be set on `Test Environnements` field in `Test Execution` issue
 ![testEnvironments_example](./doc/testEnvironnements.jpeg)

##### _debug_
 to turn on the debug mode for the helper
###### Example:
when debug is `true`

```js

OK  | 1 passed   // 57s
SEND TO XRAY=>{ "testExecutionKey": "PCR-6","info" : {"startDate" : "2020-07-08T15:41:10+02:00", "finishDate" :"2020-07-08T15:41:10+02:00","revision": "001","description" : "Results of test execution ", "testEnvironments": ["browser:chrome", "linux"]},"tests" : [{"testKey":"PCR-1","status":"PASS","comment" : "Successful execution" }]}
XRAY RESPONSE=>{"testExecIssue":{"id":"134806","key":"PCR-6","self":"https://localhost:8080/rest/api/2/issue/134806"},"testIssues":{"success":[{"id":"134801","key":"PCR-1","self":"https://localhost:8080/rest/api/2/issue/134801"}]}}
Tests results sended to XRAY on TestExecution: PCR-6
mtoure@E5450:~/workspace/demo-xray-bdd(master)$ 

```

## Export features files on Xray side
Feature files have to be exported from an `Test Execution` issue.
![Failed tests](./doc/export-execution.jpeg)


## Screenshot on xray side
### `On failure`

![Failed tests](./doc/result-ko.jpeg)

### `On success`
![Succeeded tests](./doc/result-ok.jpeg)
