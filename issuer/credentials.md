---
title: Credentials
description: Learn how to create and issue verifiable credentials using the RCL VC Issuer application
parent: Issuer
nav_order: 2
---

# Creating and Issuing Verifiable Credentials
**V1.0**

In the section, you will learn how to create and issue Verifiable Credentials (VCs) using the RCL VC Issuer application.

# What is a Verifiable Credential

Verifiable Credentials (VCs) are tamper-proof, cryptographically secure digital credentials that can be instantly checked and validated. Standardized by the World Wide Web Consortium (W3C), they act as the digital equivalent of physical documents like driver's licenses, academic diplomas, or passports. Unlike static PDF documents, VCs contain built-in cryptographic signatures that allow anyone to verify their authenticity automatically without needing a central database.

# Credential Formats

There are two credential formats as described below.

## PNG Image

A VC is issued as a .PNG image file displaying the details of the credential. The credential data is embedded as **metadata** in the image. In addition, a QR code is placed in the image. The QR code also contains the credential data.

## PDF Document

The QR code containing the credential data will be placed on a PDF document created by the Issuer. The PDF document can be a license, certificate, deed or any type of official document to be issued to a holder. The PDF document is uploaded in the RCL VC Issuer application. The application will allow the QR code to be placed anywhere in the document. 

# Credential Data

Credential data is presented in JSON format. The table below list the properties and objects contained in a credential.

## Verifiable Credential Object

| Property    | Type                 | Required |
| --------    | -------              | -------  |
| context     | List of string         | yes      |
| id          | string               | yes      |
| type        | List of string         | yes      |
| name        | string               | yes      |
| issuer      | Issuer object        | yes      |
| validFrom *1 | string               | yes      |
| validUntil *1| string               | yes      |
| credentialSubject | Credential Subject object | yes      |

## Issuer Object

| Property    | Type                 | Required |
| --------    | -------              | -------  |
| id *3       | string               | yes      |
| name        | string               | yes      |
| image *2    | string               | no       |
| validationSignature        | string               | no      |
| validUntil *1| string               | no      |

## CredentialSubject Object

| Property    | Type                 | Required |
| --------    | -------              | -------  |
| id          | string               | yes      |
| name        | string               | yes      |
| email       | string               | yes      |
| image *2    | string               | no       |
| dateOfBirth *1 | string               | no      |

Notes:
- *1 Dates as string (dd-mm-yyyy)
- *2 An image as a Base64 string 
- *3 The DID of the issuer

``Example of a Verifiable Credential in JSON format``

```Json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2"
  ],
  "id": "urn:id:C134",
  "type": [
    "VerifiableCredential"
  ],
  "issuer": {
    "id": "did:key:zDnaeoR83noBrm6PicyaAvSyNf8xBsUNL31vcAQyQhKVM3xQp",
    "name": "Ray Consulting Limited",
    "image": "data:image/png;base64,iVBORw0KGgoAAA...."
  },
  "validFrom": "08-07-2026",
  "name": "Sample Credential",
  "credentialSubject": {
    "id": "urn:id:ID1234",
    "name": "John Doe",
    "email": "john.doe@gmail.com",
    "dateOfBirth": "05-02-2003",
    "image": "data:image/png;base64,iVBORw0KGgoAAAANSUh....."
  },
  "validUntil": "08-07-2076"
}
```

# Create a Credential

- In the RCL VC Issuer application, open the the ``Credentials`` page from the left menu

- Click the ``Create Credential`` button

- In the ``Issue Credential`` page, add the Credential and Recipient information

- Click the ``Save`` button when you are done

- The newly created credential will be displayed in the credentials list

# Issue a Credential

- In the credentials list, select a credential by clicking on it

- On the ``Credential`` page, click the ``Email`` icon

- Ensure your email application, such as Microsoft Outlook is open

{: .information }
Your email application, such as Microsoft Outlook, must be open to send an email.

- Edit the default email if necessary and send the .PNG credential image as an attachment to the recipient

# Download a Credential

- On the ``Credential`` page, click the ``Download`` icon

- Download and save the .PNG image file on your PC

- You can manually send the file to the recipient via email or other means

# Credentials are transmitted as a JWT

Credentials are transmitted in the QR code and .PNG image files are a [JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519). The JWT is **encoded** in the QR code and **embedded** as **metadata** in the .PNG image file.

A JWT is a compact, URL-safe string composed of three parts separated by dots (.): 

```
Header.Payload.Signature
```
## Header

Contains metadata about the token, such as the type of token (JWT) and the cryptographic algorithm used to secure it (ES256).

## Payload

 Contains the actual data being transmitted, the credential data in JSON format.

 ## Signature

  Created by combining the encoded header, payload and signed with the issuer's private key. This guarantees the integrity of the token and ensures that the information was not tampered with during transmission.

  ``Example of a JWT``

  ```
eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCIsImp3ayI6eyJjcnYiOiJQLTI1NiIsImt0eSI6IkVDIiwieCI6IlZZVmwzZXVrWnk1Mm1FQ3diTEk2eV8yQmNPNVVDd1BsUVNBalptbUFIckUiLCJ5IjoiRk9qVl9xbTVDVEhxRFRMNXBKa0RXVnVOT3JTZmlDT3h3TGRsdjhSZFhJTSJ9fQ.eyJAY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvbnMvY3JlZGVudGlhbHMvdjIiXSwiaWQiOiJ1cm46aWQ6QzEzNCIsInR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiXSwiaXNzdWVyIjp7ImlkIjoiZGlkOmtleTp6RG5hZW9SODNub0JybTZQaWN5YUF2U3lOZjh4QnNVTkwzMXZjQVF5UWhLVk0zeFFwIiwibmFtZSI6IlJheSBDb25zdWx0aW5nIExpbWl0ZWQifSwidmFsaWRGcm9tIjoiMDgtMDctMjAyNiIsIm5hbWUiOiJTYW1wbGUgQ3JlZGVudGlhbCIsImNyZWRlbnRpYWxTdWJqZWN0Ijp7ImlkIjoidXJuOmlkOklEMTIzNCIsIm5hbWUiOiJKb2huIERvZSIsImVtYWlsIjoiam9obmRvZUBtYWlsLmNvbSIsImRhdGVPZkJpcnRoIjoiMDUtMDItMjAwMyJ9LCJ2YWxpZFVudGlsIjoiMDgtMDctMjA3NiJ9.qyuhwhstDBipohcijO6dFCahA1xWyf_JoU6g2e5lBqx3xfsxlGBfXnAMWAbxJai1KBYgxaxIDL1mw6dcrZlO8Q
  ```

  # Decoding a JWT

  A JWT can be decoded into it constituent parts. You can use the following website to decode a JWT, [jwt.io](https://www.jwt.io/)

  ## Header in JSON format

  Here you can see the cryptographic algorithm used and the issuer's public key presented as a JSON Web Key (JWK)

  ``Example Decoded JWT Header``

  ```json
  {
  "alg": "ES256",
  "typ": "JWT",
  "jwk": {
    "crv": "P-256",
    "kty": "EC",
    "x": "VYVl3eukZy52mECwbLI6y_2BcO5UCwPlQSAjZmmAHrE",
    "y": "FOjV_qm5CTHqDTL5pJkDWVuNOrSfiCOxwLdlv8RdXIM"
  }
  ```

  ## Payload in JSON format

  This is the actual credential data

``Example Decoded JWT Payload``

  ```json
  {
  "@context": [
    "https://www.w3.org/ns/credentials/v2"
  ],
  "id": "urn:id:C134",
  "type": [
    "VerifiableCredential"
  ],
  "issuer": {
    "id": "did:key:zDnaeoR83noBrm6PicyaAvSyNf8xBsUNL31vcAQyQhKVM3xQp",
    "name": "Ray Consulting Limited"
  },
  "validFrom": "08-07-2026",
  "name": "Sample Credential",
  "credentialSubject": {
    "id": "urn:id:ID1234",
    "name": "John Doe",
    "email": "johndoe@mail.com",
    "dateOfBirth": "05-02-2003"
  },
  "validUntil": "08-07-2076"
}
```

## Signature as a Base64 string

This is the signature for the credential presented as a base64 url-encoded string

``Example JWT Signature``

```
qyuhwhstDBipohcijO6dFCahA1xWyf_JoU6g2e5lBqx3xfsxlGBfXnAMWAbxJai1KBYgxaxIDL1mw6dcrZlO8Q
```

# Verifying the Signature of a Credential

The public key that is contained in the credential is matched with the issuer's DID. Once there is a positive match, the public key is used to verify the signature. Once the signature is verified, the credential is deemed to be valid.


