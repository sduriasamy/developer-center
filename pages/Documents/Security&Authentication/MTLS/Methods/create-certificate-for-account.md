---
pagename: Create certificate for account
keywords:
sitesection: Documents
categoryname: "Security & Authentication"
documentname: MTLS 
subfoldername: Methods
permalink: mtls-methods-create-certificate-for-account.html
---

{: .note}
Currently, these methods cannot be used to create certificates. To get started with a certificate, please contact LivePerson Support.

This API creates a certificate for a specific account ID.

### Request

|Method|      URL|  
|:--------  |:---  |
|POST|  https://[{domain}]/mtls/account/{accountId}/certificates |

**Request Headers**

|Header         |Description  |
|:------|        :--------  |
|Authorization|    Contains token string to allow request authentication and authorization.  |

**Request Body**

```json
[
  {
  	"name":"myCert1",
  	"p12":[98,121,116,101,115,…],
  	"password":"paw1"
  }
]
```

**Path Parameters**

|Parameter|  Description|  Type/Value |
|:------    |:--------    |:--------|
|accountId|  LP site ID |   String |

### Response

**Response Codes**

| Code | Description           |
|------|-----------------------|
| 201  | Created               |
| 401  | Not Authenticated     |
| 403  | Not Authorized        |
| 500  | Internal Server Error |

**Response Body**

For example:

```json
{  
   "successfulySavedCertificates":[  
      {  
         "id":2628739923,
         "deleted":false,
         "name":"{certificateName}",
         "displayName":"{certificateName}",
         "siteId":"{accountId}",
         "status":"Available",
	 "expirationDate": null
      }
   ],
   "failedSaveToVaultCertificates":[  

   ]
}
```

**Entity Structure:**

| Attribute | Description  | Type/Value | Required | Notes |
| :------   | :--------    | :-------- | :--- | :--- |
| id | A certificate's unique object ID in the account config table. | long number | Read only | |
| deleted   | Indicates whether the certificate is deleted or not. | Boolean | Read only | |
| name | A certificate's unique name. | unique string | Required | |
| displayName    | A certificate's display name.  | string | Required | |
| siteId | The account ID the certificate is associated with. | string | Required | |
| status | Indicates if the certificate is available/not available/expired | string | Required | (the certificate is available if it exists at both HashiCorp Vault and LivePerson's Data Base and if isn't expired)|
| expirationDate | certificate's expiration date. | string | Not Required | |
