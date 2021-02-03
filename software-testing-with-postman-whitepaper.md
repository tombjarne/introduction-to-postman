# API Testing with Postman Whitepaper

**Author: Tom Bjarne Seidel**, ***2020***

## What is Postman? 

Postman is a software that allows developers to test API interfaces and internal interfaces holistically and  quickly. Postman convinces  with  its multiple  possibilities  to  check  systems for  integrity and completeness and to share these results with a team. 

Furthermore, the Postman development and test environment allows the creation of documentation, mocks and automated test suites. 

## Working with Postman 

### 1. working in a team

Postman allows teams to work on a single project and give non-developers visibility into the current development state. For example, a manager does not need to do anything other than triggering a test  or  monitor  a  test  collection.  The  developers  can  then  make  adjustments  and  update  the Postman project. 

#### 1.1 Version Control 

Developers are enabled to create a snapshot of the current state by creating a fork. A fork creates a new branch in the current project, which can also be shared with the team. Forking allows Postman to work on different features and tests. A fork is particularly useful for larger development teams and when there are a large number of tests. 

![](./images/software-testing-with-postman-whitepaper.002.png)![](./images/software-testing-with-postman-whitepaper.003.png)

Each fork can either be merged with the project immediately via a merge or a pull request. It is recommended to always work with a pull request to avoid damage to the current project. A pull request helps the developers understand the code of a collaborator or check it for correctness. 

![](./images/software-testing-with-postman-whitepaper.004.png)

A title and a meaningful description should always be defined per pull request. Up to 50 reviewers can be added per PR. Each reviewer can approve the changes  or reject them if they have concerns. In the case of detailed descriptions, this also helps managers and project leaders gain a better insight into the current development status and comment on the changes. 

## Postman features

### 1. Requests 

In  Postman  it  is  straightforward  to  create  a  new  request.  Each  request  has  two  mandatory parameters that must be specified. On the one hand, the correct method must be chosen and an accessible URL. If these factors are given, the developer has additional setting options, which are especially useful for protected or complex requests. 

![](./images/software-testing-with-postman-whitepaper.005.png)

### 1.1 Authentication 

Password-protected endpoints require valid credentials; otherwise, the request fails and a  corresponding  status  code  is  returned.  For  this  reason,  Postman  supports  the authentication feature internally. Various options are offered for this. 

Particularly interesting are the authentication options via an API key, OAuth, AWS signature or the classic username-password pair. Depending on the selected method, the required information can be entered in a text field. If activated the authentication data is sent with the next request. 

![](./images/software-testing-with-postman-whitepaper.006.png)

### 1.2 Header 

Each Postman request can take specific values in the header. Postman natively supports various generic and often used parameters such as host, accept or accept encoding. However, you can also define your own headers, which can be transferred to the server when sending the request. 

The key-value pairs defined in the Headers tab are applied when the request is saved and can therefore be used again and again. It does not have to be created again from scratch. 

### 1.2 Body

The request body is particularly suitable for requests whose transmitted data should not be publicly visible. In contrast to the transmission via URL, the data is sent to the server in a JSON body. Since the body is only explicitly forbidden in the TRACE method according to the HTTP documentation, this function offers a lot of room for free play. 

However, the body can be sent in formats other than JSON. Postman also supports form data, x- www-form-urlencoded, binary and GraphQL. The raw option supports JSON, text, HTML, XML or even JavaScript format. 

![](./images/software-testing-with-postman-whitepaper.007.png)

### 1.4 Settings

The Settings tab in Postman allows advanced settings regarding the current request. Among them, options such as the use of SSL can be set. Furthermore, the settings allow even better mimicking of different scenarios and end devices. 

## 2. Environments

An environment in Postman is a self-contained system of variables. The visibility and usability of variables is limited to the use of the environment. Each environment can hold any number of variables to which source values can be assigned. This is especially helpful in different test cases where other variables or values are needed. 

![](./images/software-testing-with-postman-whitepaper.008.png)

Environments are essential when testing interfaces and their reactions to specific values or, for example,  the  absence  of  a  required  variable.  Especially  for  contract  tests  and  unit  tests,  it  is recommended to create different environments for the test. Environments can also be exported or divided in order to be able to use them in other cases. Previously created environments can also be imported. 

## 3. Globals

Globals in Postman are variables that can be used by any request in any project. If a global variable is active, it can be read at any time and used in a request. This is especially useful for values that are needed in every request and almost never change. 

![](./images/software-testing-with-postman-whitepaper.009.png)

Otherwise, it is recommended to always create an environment to perform the test. Care must also be taken when overwriting environment variables. A global variable still has priority over an environment variable. So it makes sense to assign different names and to reduce the number of globals to a minimum. 

## 4. Tests

Postman tests are written in vanilla Javascript. The Postman Sandbox supports the latest ECMA standard and offers a lot of flexibility and possibilities in handling request and response data. 

Basically, two types of tests can be created per request. A pre-request script and a test. The difference is when the code is executed. The pre-request script is executed before the request is actually  sent.  The  test  deals  with  the  response  of  the  request  and  is  performed  after  the complete receipt of an answer. 

### 4.1 PM API

Postman provides with the PM API an internal JavaScript programming interface. It has its own syntax and supports the developer in receiving and processing response data. In principle, each Postman test begins in the same way and is also recognized as such during runtime. In the later test evaluation, each of these pm functions is executed and displayed as a separate subtest. 

This significantly simplifies debugging and guarantees clarity with regard to testing. Furthermore, the Postman Sandbox contains a small library of frequently used code snippets that can be inserted simply at the push of a button. 

The procedure and syntax of a pm test is similar to that of a Cypress test. However, it is essential to note that no UI is tested, but only data and variables are checked. 

### 4.2 Pre-request Script

The  pre-request  script  is  beneficial  when  certain  operations  are  to  be  imitated.  Instead  of  a function  that  is  executed  when  a  button  is  clicked,  the  corresponding  values  can  simply  be specified.  

This is particularly helpful when an extensive test such as an integration test is to be performed. In the pre-request script, the developer could, for example, process and modify variables that have already been received. In general, it is a good idea to perform operations that have to be executed before specific requests here. 

![](./images/software-testing-with-postman-whitepaper.010.png)

This allows a complete project with existing code to be perfectly imitated and a specific scenario to be faithfully recreated. Without a pre-request script, the developer would always have to rely on static values that could only be changed in a cumbersome way. This slows down the workflow and significantly limits the possibilities. 

It is always recommended to use a pre-request script if existing values have to be transferred to another interface. These values can be saved from a previous request into the current environment. In this way, existing variables can be used in the best possible way, as in a "real" project. 

### 4.3 Tests ( Post-request )

Any  conceivable  test  cases  can  be  executed  in  the  test  area.  Tests  are  to  be  completed  after receiving the response data. Either conventional JavaScript code can be written, or a pm test can be created. 

It is recommended to wrap the code in meaningful pm tests as often as possible to be able to act faster  when  debugging  later.  In  these  tests,  it  is  effortless  to  set  environment  variables  and extract their values. 

![](./images/software-testing-with-postman-whitepaper.011.png)

For more extensive tests, such as an end-to-end test, the developer can add additional code in the tests tab for specific requests to extract necessary data. These variables can then be accessed in the next request, provided they have been stored in the environment  or as global. 

## 5. Collections
### 5.1 Collection variables

Collections expose a third type of Postman variable. The collection variable is only visible in the current collection and cannot be used by any other collection. It is recommended to use a mixture of Environment and Collection variables, depending on the data. 

### 5.2 Creating a collection

A collection is a collection of created requests. It is stored in a folder and can be viewed by Postman as a single entity. When creating a collection, a meaningful description and title should always be added. Furthermore, an authentication method can be created for the entire collection without the code having to be present in each request itself. 

![](./images/software-testing-with-postman-whitepaper.012.png)

Generic and reusable tests can also be stored in the collection. A pre-request script or a test added to a collection is executed after or before each current request collection (depending on the test type). Furthermore, collection variables can be created and initialized with values. 

### 5.3 Collection Runner

To test one or more collections, Postman provides the Collection Runner. In this overview, different requests and collections can be selected. 

Furthermore, the Collection Runner allows direct access to the console, as well as running the tests from the command line. Additionally, the runner can use different environments and run through a certain number of iterations. Positive test results are marked in green, the failed ones in red. The runner can be accessed at the top left of the screen. 

![](./images/software-testing-with-postman-whitepaper.013.png)

## 6. APIs

One of the newest and most exciting features of Postman is the creation of custom API schemas. With this feature, existing API specifications can be imported and automatically integrated. During this process, collections can even be created from the specified schema. 

Excitingly, Postman also supports the OpanAPI 3.0 standard. For example, a developer can create a specification with Swagger, export it as a YAML file and import it into Postman. After the import, collection and requests are already available, so the tedious work of creating them manually can be saved. 

Otherwise, a repository can be connected that holds a current version of a YAML file, which is then automatically updated when changes are made. 

An API in Postman can also be specific to an environment, which facilitates testing under different circumstances. The API schema can also be edited and versioned in Postman. 

![](./images/software-testing-with-postman-whitepaper.014.png)

Test suites, integration tests, contract tests, monitors, mocks and documentation can be created per API. A comment function is also available. Especially for a team, this is a straightforward solution to test APIs before they are programmed and to be prepared for any problems that may occur. 

## 7. Mocking

A mock is an imitation of a working server, but without having to write any code. Postman has the ability to create a mock to mimic a constructed API scheme. Postman automatically generates a link to the mock server. 

If a request is now sent from a specified request of the mocked collection, a corresponding response can be extracted. Mock servers can also be versioned, similar to the APIs. It is recommended to version mock servers and APIs equally to avoid confusion. 

### 7.1 Mock examples

For  a  mock  server  to  return  a  meaningful  response,  some  manual  work  is  required.  So-called examples must be created for each request. Each example must be mapped to a specific URL with a particular HTTP method. 

As soon as this assignment exists, a corresponding status code and a response can be created, which is to be returned for a specified scenario. If no example exists for a request, no correct answer can be returned. 

![](./images/software-testing-with-postman-whitepaper.015.png)Developers must take special care when creating examples so that each example is returned only in     the desired scenario and no confusion arises. With the help  of examples, mocks can be validated directly in Postman and checked for errors. 

Unfortunately, it is not possible to assign examples based on their request body. It always requires a specific header value that must be uniquely assigned to the example. This is unfortunately very cumbersome and inflexible. 

The creation of examples for requests that require a request body is therefore somewhat more complicated. If an example returns an unexpected value, the validation throws an error and indicates problems in the project. This way you can write good specs and find errors in the API. 

## 8. Documentation

Similar  to  Swagger,  Postman  can  generate  documentation  of  the  existing  interfaces  and  their requests from a given API schema. This is especially recommended when working in larger teams so that the interfaces are clearly described and misunderstandings can be prevented. 

A Postman documentation can also be set as publicly available. Other Internet users can then also access this and use it if necessary when working with the API (if the API is publicly accessible). 

## 9. Test suites

A test suite is created based on the collection used in the API and includes all requests and their examples. A test suite is needed to automate the tests and to monitor the test results. 

## 10. Monitors

Monitors in Postman are listeners that perform a specific Test Collection after a specified time. When a monitor is active, notifications can be enabled. A monitor lists all tests and provides information about the success or failure of the tests. 

A different environment can be defined or specified for each monitor. Versioning is also possible. For example, developers can create multiple monitors for an API that run specific test suites under the conditions of the respective environments. 

Thus, different scenarios can be tested simultaneously and managed in one project. In addition to the possibility to call up the individual tests in the monitor, the required time is recorded. 

Monitors help developers and managers to monitor the project and point out problems. It also makes it easy to run contract tests, integration tests or end-to-end tests. 

## 11. Code generator

Postman has the function to generate the request code for any request. Headers, authentication and other settings of the request are taken into account and converted into valid code. Postman supports more than 10 different languages, including Node.js, PHP, Perl, JavaScript and C. 

![](./images/software-testing-with-postman-whitepaper.017.png)

## 12. Newman

In addition to automating the tests with the help of test suites, Postman tests can also be executed via the command line with Newman. Individual requests can be retrieved using cURL commands, for example. Each collection and environment can also be exported and included in a test via command line or Jenkins. 

Developers must keep in mind that the respective export of environments and collections can be tedious and, depending on the project, may cost more time than it benefits. 

# Examples

**Status checking**

```JavaScript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

**Response code checking**
```JavaScript
pm.test("Successful request", function () {
    pm.expect(pm.response.code).to.be.oneOf([200,204]);
});
```

**Validating responses**
```JavaScript
pm.test("Successfully retrieved id", function () {
    pm.globals.set("butterbrotId",pm.response.json().item[0].id);
});

pm.test("Valid response", function () {
    if(pm.response.to.have.status(200)){
        if (pm.response.to.be.json) {
            console.log("valid json retrieved with " + pm.response.status);
        }
    } else if(pm.response.to.have.status(400)){
        console.log("invalid json following status " + pm.response.status);
    }
});
```

**Setting variables**

```JavaScript
pm.globals.set("bookId", response[Number(index.toString())].id);
pm.globals.set("invalidBookId", parseInt(pm.globals.get("bookId")) + 10);
```

**Getting variables**

```JavaScript
pm.globals.get("url");
```

# Combined Examples

**Switch-case**

```JavaScript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Found book ids", function () {

    let response = pm.response.json().books;
    let index = Math.floor((Math.random() * 10) + 1);

    switch (index) {
        case 0:
            index = 1;
            break;
        case 1:
            index = 1;
            break;
        case 2:
            index = 1;
            break;
        default:
            index = 0;
            break;
    }

    pm.globals.set("bookId", response[Number(index.toString())].id);
});
```

**Picking random ids**

```JavaScript
pm.test("Retrieved profile link", function () {
    let response = pm.response.json().videos[0].user.url;
    console.log(response);
    pm.globals.set("profileLink", response);
});

pm.test("Valid response", function () {
    if(pm.response.to.have.status(200)){
        if (pm.response.to.be.json) {
            console.log("valid json retrieved with " + pm.response.status);
        }
    } else if(pm.response.to.have.status(400)){
        console.log("invalid json following status " + pm.response.status);
    }
});

pm.test("Got random video id", function () {
    let randomVideo = Math.floor(Math.random() * 1000000);
    pm.environment.set("randomVideoId", randomVideo);
});

pm.test("Got random video id", function () {
    let randomVideo = Math.floor(Math.random() * 10);
    console.log(pm.response.json().videos[randomVideo]);
    pm.environment.set("randomVideo", randomVideo);
});
```

**Validating and variables**

```JavaScript
pm.test("Response has valid json body", function () {
    if (pm.response.to.have.body && pm.response.to.be.json) {
        pm.test("id plus one", function () {
    pm.environment.set("inhabitantId", parseInt(pm.environment.get("inhabitantId")+1));
});
    } else {
        console.log(request.name);
    }
});
```

# Advantages of Postman

- Easy testing in all development phases 
- Easy testing of new integrations or microservices 
- Testing authentication methods 
- Automate tests 
- Mocking from Collections 
- Create different environments 
- Different test types for before and after sending the request 
- Team management and sharing 
- Versioning and comment function 
- Integrated code generator 
- Helpful and active community 
- Available for Linux, Windows and macOS 

# Disadvantages of Postman

- Little flexibility when testing a mock example with request body 
- Only to a lesser extent free of charge, yet inexpensive and extensive 
