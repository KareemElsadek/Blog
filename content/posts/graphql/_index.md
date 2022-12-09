

![](/graph.png)
# What is GraphQL?

GraphQL is a data query language developed by Facebook. It acts as an alternative to the [REST API](https://www.ibm.com/cloud/learn/rest-apis).

| REST API      | GraphQL |
| ----------- | ----------- |
|• Require the client to send multiple requests to different endpoints on the API to query data from the database.    | • you only need to send one request to query the backend.
  • You need to know the URL of each resource, the HTTP methods used on each resource, and the schema of each resource.       | • you need to know only the URL of the API and the schema.

![](/restvsgraph.jpeg)

**REST API call:**\
• Regiter a user: send request to [/api/v1/register].\
• sign-in: send a request to [/api/v1/login].\
• Reset the password: send another request to [/api/v1/reset-password].\
**Every resource has its own schema and own method.**

**GraphQL call:**\
• There is only one endpoint that you can send all requests to it! (/graphql?q=)

**Components of the GraphQL:**
| server-side      | client-side |
| ----------- | ----------- |
| it resolves the operations and provides the requested data/operation.      | application that wants to interact with the GraphQL API       |



**GraphQL has 3 main operations:**\
• Query: fetching data using specifically defined query operations.\
• Mutations: for modifying any data (creating, updating, or deleting) in a database using operations.\
• Subscriptions: for receiving real-time messages from the back-end.


---

# GraphQL Pentesting
• **Endpoint of the GraphQL:**\
[\
"/graphql", "/graphiql", "/graphql/console", "/graphql.php", "/graphiql.php", "/explorer", "/altair", "/playground", "/graphql-explorer", "/graphiql/"\
]

• You can test queries through [Swapi-GrapthQL](http://graphql.org/swapi-graphql)

### __Introspection__
• allows to query all information related to the supported schema and queries on a GraphQL server instance like: fields, types, sub-fields and more.\
•The introspection system is enabled by default, but it can be disabled.\
__Simple examples:__\
• {__schema{types{name,fields{name}}}} #getting fields and subfields ![](/graphql-1.png)\
• { __schema{types{name,fields{name,args{name,description,type{name,kind,ofType{name,kind}}}}}}} #extracting all the types, it’s fields, and it’s arguments ![](/graphql-2.png)

• __At this point, there is no vulnerability!__\
• After knowing the fields and subfields we need to query them to get the data :D\
__EX:__ /graphql?q={Users{id,name,nickname}}

**• If the introspection is off!**\
•  So we try to get information about the schema from the resulted errors, such as the following:\
query: query={users} ![](/graph-errors1.png)\
So now we got 2 fields :D\
query: query={imUsers{ids}} ![](/graphid.png)\
we got a subfield of imUsers field\
query: query={imUsers{id,username}} ![](/graphuser.png)\
got another 2 subfiles and so on, reaching to the dumping.

**Possible attacks on GraphQL**\
There are many vulnerabilities that can be raised from GraphQL mis-configuration, such as the following:\
• Information Disclosure.\
• IDOR.\
• SQL Injection.\
• CUD “creating, updating, and deleting” data via abusing mutations.\
• Authorization bypass.\
• Broken access control.

**Some attacks senarios**\
• [SSRF from GraphQL with enabled Introspection](https://0xdf.gitlab.io/2021/05/29/htb-cereal.html#graphql-enumeration)

---

## **Refrences:**
+ https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/graphql
+ https://owasp.org/www-chapter-pune/meetups/2021/June/Attacking%20GraphQL%20APIs.pptx
+ https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/12-API_Testing/01-Testing_GraphQL
+ https://exzandar.home.blog/2022/06/22/graphql-the-graphql/

<script>
	    document.querySelector("title").textContent = "GraphQL";
</script>
<head>
 <meta property="og:image" content="/graph.png" />
 <meta property="og:type" content="website" />
 <meta property="og:url" content="https://kareemelsadek.github.io/posts/graphql"/>
 <meta property="og:title" content="GraphQL" />
 <meta property="og:description" content="Intro to GraphQL Pentesting"/>	
</head>