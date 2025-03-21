# Improper Assets Management  

>[Testing for Improper Assets Management](https://university.apisec.ai/products/api-penetration-testing/categories/2150251354/posts/2157505650)  

>Bill of material also relates to versions of software develoipment releases of application.  
>API provider will update services and the newer version of the API will be available over a new path.  

Examples of paths:

```
api.target.com/v3
/api/v2/accounts
/api/v3/accounts
/v2/accounts
```  

>API versioning could also be maintained as a header:

```
Accept: version=2.0
Accept api-version=3
```  

>In addition versioning could also be set within a query parameter or request body.

```
/api/accounts?ver=2
POST /api/accounts

{
"ver":1.0,
"user":"hapihacker"
}
```  

>Earlier versions of the API may no longer be patched or updated. Since the older versions lack this support, they may expose the API to additional vulnerabilities.  
>For example, if `v3` of an API was updated to fix a vulnerability to injection attacks, then there are good odds that requests that involve v1 and v2 may still be vulnerable. 

>Non-production versions of an API include any version of the API that was not meant for end-user consumption. Non-production versions could include:  

```
api.test.target.com
api.uat.target.com
beta.api.com
/api/private
/api/partner
/api/test
```  

## Find Improper Assets Management Vulnerabilities  

>Authenticated web directory discovery to find different undocument versions that is possible vulnerable endpoints.

>Using Burp repeat get valid `Authorization: Bearer` header token cookie.  

```
ffuf -ic -c -w /home/kali/Downloads/apisec/api-version-wordlist.txt:FUZZ -u http://127.0.0.1:8888/FUZZ -H 'Authorization: Bearer <token>'

3. Use POST method:

gobuster dir -k -U vdaisley -P calculus20 -u http://dev.topology.htb/ -w /home/kali/Downloads/apisec/api-version-wordlist.txt

```  

>Authenticated Directory scan, recursive depth set, to identify API versions.  

```
ffuf -ic -c -recursion -recursion-depth 6 -v -w /home/kali/Downloads/apisec/api-version-wordlist.txt:FUZZ -u http://127.0.0.1:8888/FUZZ -H 'Authorization: Bearer eyJhbGciOiJSUzI<snip>DKmr4ChPLUcQ'
```

![crapi-inproper-assets-management.png](/images/crapi-inproper-assets-management.png)  

## Improper Assets Management Assessment  

>Which version of the vAPI/API9 endpoint was recently launched?  

* v2

>What status code is sent back to /vapi/api9/v2/user/login using an incorrect pin?

* 200

>What HTTP status code is sent after six consecutive incorrect requests to /vapi/api9/v2/user/login?

* 500

>Which headers are included in responses to /vapi/api9/v2/user/login that are missing from /vapi/api9/v1/user/login?

* X-RateLimit-Limit: 5
* X-RateLimit-Limit-Remaining: 4

>What is the flag for successfully discovering richardbranson's pin?

* api9_81e306bdd20a7734e244  

----  

>API:2019 Improper Assets Management is most like which other common vulnerability?

* OWASP AO6:2021 Vulnerable and Outdated Components.  

>Improper Assets Management vulnerability primarily involves what?

* Exposed and unsupported API versions  

>The crAPI Improper Assets Management vulnerability affected which endpoint?

* identity/api/auth/  

>The Improper Assets Management vulnerability affecting crAPI allows you to perform which attack?

* Brute Force  

>Which of the following are methods used for API versioning?

* Request parameters
* Request Headers
* URL path  

>Which security controls would NOT have helped reduce the risk of the crAPI Improper Assets Management vulnerability?

* By increasing the number of API versions  

----  
