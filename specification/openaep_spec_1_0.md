Summary
-------------

Open Application Exchange Protocol (OpenAEP) is designed to simplify deals when one appstore (source appstore) licenses its catalog of applications to another appstore (distributor appstore) for distribution via OnePF repository. It is an RESTful protocol with XML based results. [AppDF](http://www.onepf.org/appdf) is used an an application description format.

Methods 
-------------
OpenAEP consists of six methods:

<table>
  <tr>
    <th>Method name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><a href="#applist">applist</a></td>
    <td>List of all applications sorted by last update date with brief information about each (package, version, last update, etc)</td>
  </tr>
  <tr>
    <td><a href="#appdf">appdf</a></td>
    <td>Fetch the actual AppDF file that contains the App Descriptons and other files.</td>
  </tr>
  <tr>
    <td><a href="#reviews">reviews</a></td>
    <td>User review information about the given app(s)</td>
  </tr>
  <tr>
    <td><a href="#downloads">downloads</a></td>
    <td>List of all app downloads with detailed information about each download provided by the distributor appstore</td>
  </tr>
  <tr>
    <td><a href="#purchases">purchases</a></td>
    <td>List of all app purchases with detailed information about each purchase provided by the distributor appstore</td>
  </tr>
  <tr>
    <td><a href="#sign">signReceipt</a></td>
    <td>Sending by destributor store to source store (via repository) to sign InApp purchase.</td>
  </tr>
</table>

Security 
--------------
To secure all comunication between source store, repository and distributor store following requirements must apply:

- all communication is secured with SSL protocol.
- Every store and repository should exchanges authorization Token. Token is a string with 32 alphnumeric characters used to authentificate store in repository and repository in store.
- Also appstore should provide following information to be able work with repository:
	- Unique appstore name (max 100 chars).
	- Root URL to it's openaep protocol realization.
	- Public key to validate <a href="#sign">Sign Receipt</a> requests.
	
Authentification
--------------
Every request are sended to repository should contain "authToken" in it's HTTP headers or as a request parameter. It must be a token provided by repository to appstore. Every request from repository to appstore will contain token that provided by appstore .


Fetch data
-------------
All result must be sorted in newest first and oldest last. This enables user to fetch the last data from a another server without have to crawl the full dataset.

<b>offset</b> The method "App list", "App reviews", "Downloads" and "Purchases" use attribute "offset" (in first element) that is a fully qualified
url to next page of this dataset. Absebse of this attribute means that this piece of data is last. 
This is recommended to split data in pices of 1000 item each except for "App list" that the is recommended to split in price of 5000 apps.

Requests
-------------

All requests (exept <a href="#sign">Sign Receipt</a>) are GET requests in following format:

```
GET https://<ROOT_OPENAEP_URL>/openaep/<METHOD_NAME>?<PARAMETERS>&authToken=<AUTH_TOKEN>
```

- ROOT_OPENAEP_URL - root url to openaep protocol realization, provided by appstore or repository.
- METHOD_NAME - Name of the method.
- PARAMETERS - Parameters for corresponding method.
- AUTH_TOKEN - Authorization token. Can be provided as request parameter or HTTP header


## applist
#####Request
No parameters

```
https://www.sourcestore.com/openaep/applist?authToken=dee0ed6174a894113d5e8f6c98f0e92b
```

#####Response
Response contains list of xml objects with attributes:

- **package** - name of the package contains in appdf file.
- **hash** - MD5 calculated hash of the appdf file

```xml
<?xml version="1.0" encoding="UTF-8"?>
<application-list version="1" offset=https://www.sourcestore.com/openaep/applist_9.xml>
  <application package="com.softspb.flashcards.sv" hash="2AD12A417FB624F4AED9CE0B7D732FD7">
  <application package="ru.yandex.shell" hash="0F229B2805710DD6F4F6779046C889BB">
  <application package="org.onepf.trivialdrive" hash="D10D4E038F0FD379EF074511081F85E6">
</application-list>
```
 
 
## appdf
Get the AppDF file that is described at [AppDF](http://www.onepf.org/appdf).
#####Request
<table>
  <tr>
    <th>Param</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>package</td>
    <td>Y</td>
    <td>Android package name</td>
  </tr>
</table>
```
https://www.sourceappstore.com/openaep/appdf?package=com.mxtech.videoplayer.ad
```
// Absense authToken in request parameters means it is in HTTP header

#####Response
An AppDF file that contains all need APK and images files.
 
## reviews
#####Request
No parameters

```
https://www.sourceappstore.com/openaep/reviews?authToken=dee0ed6174a894113d5e8f6c98f0e92b
```
#####Response
```xml
<?xml version="1.0" encoding="UTF-8"?>
<reviews version="1" offset="https://www.sourceappstore.com/openaep/7j8ad9go.xml">
    <review
    	package="ru.yandex.shell"
     	appstoreId="com.sourceappstore"
      	version="1.3.1"
      	versionCode="81"
     	rating="0.6"
      	datetime="2013-02-22 23:30:30"
      	device-model="SHW-M130K"
      	device-name="Samsung GT-i9082"
      	country="US"
      	user-name="Bill White"
      	title="Greate to learn language"
      	text="Just perfect as it was since Win Mobile times"
      	review-url="https://www.sourceappstore.com/reviews/108973876811345873453"/>
    <review
    	package="org.onepf.trivialdrive"
     	appstoreId="com.sourceappstore"
      	version="1.0"
      	versionCode="50"
     	rating="1.0"
      	datetime="2013-02-22 23:30:10"
      	device-model="SHW-M130K"
      	device-name="Samsung GT-i9082"
      	country="DE"/>
    <review
    	package="org.onepf.trivialdrive"
     	appstoreId="com.sourceappstore"
      	version="1.0"
      	versionCode="50"
     	rating="0.8"
      	datetime="2013-02-22 23:29:10"
      	device-model="HTC One X"
      	device-name="HTC One X"
      	country="US"
      	user-name="Dorian Gray"
      	title="Great Game"
      	text="Great game, but too short. 4 stars because of that."
      	review-url="https://www.sourceappstore.com/reviews/108973873741345873453"/>
    <review
    	package="com.softspb.flashcards.sv"
     	appstoreId="com.sourceappstore"
      	version="2.0.0.1"
      	versionCode="117"
     	rating="0.4"
      	datetime="2013-02-22 23:20:10"
      	device-model="SHW-M130K"
      	device-name="Samsung GT-i9082"
      	country="UK"/>
</reviews>
```

## downloads
#####Request
No parameters

```
https://www.sourceappstore.com/openaep/downloads
```
// Absense authToken in request parameters means it is in HTTP header
#####Response
```xml
<?xml version="1.0" encoding="UTF-8"?>
<downloads version="1" offset="https://www.distributorappstore.com/openaep/6i7zc8fn.xml">
    <download
    	package="com.softspb.geo_game"
     	appstoreId="com.sourceappstore"
      	version="1.0"
      	versionCode="50"
      	datetime="2013-02-22 23:30:30"
      	device-model="SHW-M130K"
      	device-name="Samsung GT-i9082"
      	country="US"
      	is-update="no"/>
   	<download
    	package="com.softspb.flashcards.sv"
     	appstoreId="com.sourceappstore"
      	version="1.3.1"
      	versionCode="81"
      	datetime="2013-02-22 23:20:10"
      	device-model="HTC One X"
      	device-name="HTC One X"
      	country="DE"
      	is-update="yes"/>      	
</downloads>
```

## purchases
#####Request
No parameters

```
https://www.sourceappstore.com/openaep/purchases
```
// Absense authToken in request parameters means it is in HTTP header
#####Response
```xml
<?xml version="1.0" encoding="UTF-8"?>
<purchases version="1">
    <purchase
    	id="90812378"
    	package="com.softspb.geo_game"
     	appstoreId="com.sourceappstore"
      	version="1.0"
      	versionCode="50"
      	datetime="2013-02-22 23:30:30"
      	device-model="SHW-M130K"
      	device-name="Samsung GT-i9082"
      	country="US"
      	user-price="0.99"
      	user-currency="USD"
      	inner-price="0.99"
      	inner-currency="USD"
      	signature="dD80ihBh5jfNpymO5Hg1IdiJIEvHcJpCMiCMnN/RnbI="/>
   	<purchase
   		id="+SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE="
    	package="com.softspb.flashcards.sv"
     	appstoreId="com.sourceappstore"
      	version="1.3.1"
      	versionCode="81"
      	datetime="2013-02-22 23:20:10"
      	device-model="HTC One X"
      	device-name="HTC One X"
      	country="DE"
      	user-price="1.70"
      	user-currency="EUR"
      	inner-price="2.50"
      	inner-currency="USD"
      	signature="+SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE="/> 
</purchases>
```

## signReceipt

This request is used by distributor store to sign inApp purchase in source store. Distributor store sign its request with it's private key and send to repository. Repository validates signature and provide this request to source store. Source appstore sign receipt with application specific key and send it back to repository provides it to distributor store.

#####Request
POST request with XML **receipt** object. It contains three attributes:

 - **receipt-data** - Purchase receipt. String in JSON format with following fields: appstoreId, orderId, packageName, productId, purchaseTime, purchaseToken, developerPayload. 
 <i>Should not contain spaces, newlines, etc. to avoid errors in signature calculation.</i>
 - **distributor-appstore** - unique appstoreId of destributor store.
 - **distributor-signature** - the receipt-data signed with distributors private key
 
request:

```
POST https://www.sourceappstore.com/openaep/signPurchase
```
requestBody:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<receipt version="1" 
	receipt-data='{"appstoreId":"com.destributorstore","orderId":"com.example.app","packageName":"com.example.app","productId":"exampleSku","purchaseTime":1345678900000,"purchaseToken":"122333444455555","developerPayload":"example developer payload"}' 
	distributor-appstore='com.distributorstore' 
	distributor-signature='+SzBm0wi8xECuGkKw97wnkSZ/62sxU+6Hq6a7qojIVE='/>
```

#####Response
 - **receipt-data** - Purchase receipt. String in JSON format with following fields: appstoreId, orderId, packageName, productId, purchaseTime, purchaseToken, developerPayload. 
 <i>Should not contain spaces, newlines, etc. to avoid errors in signature calculation.</i>
 - **developer-appstore** - unique appstoreId of source store.
 - **developer-signature** - the receipt-data signed by source store with application specific key.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<receipt version="1" 
	receipt-data='{"appstoreId":"com.destributorstore","orderId":"com.example.app","packageName":"com.example.app","productId":"exampleSku","purchaseTime":1345678900000,"purchaseToken":"122333444455555","developerPayload":"example developer payload"}' 
	developer-appstore='com.sourcestore' 
	developer-signature='dD80ihBh5jfNpymO5Hg1IdiJIEvHcJpCMiCMnN/RnbI='/>
```

Status
-------------
Current status: draft
Specification version: 0.83
Last update: April 15, 2014  

License
-------------
This file is licensed under the Creative Commons Attribution 2.5 license:  
http://creativecommons.org/licenses/by/2.5/

Source code is licensed under Apache License, Version 2.0:  
http://www.apache.org/licenses/LICENSE-2.0.html


