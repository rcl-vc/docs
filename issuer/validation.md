---
title: Validation
description: Learn how to validate an Issuer's identity
parent: Issuer
nav_order: 3
---

# Validating an Issuer's Identity
**V1.0**

In the section, learn to validate an issuer's identity.

# The Problem

An issuer can impersonate another entity or organization and falsely issue credentials. Although the credential may be valid, the issuer's identity is not valid. There must be a mechanism to validate that an issuer is in fact who they claim to be. This is accomplished by a process called **Issuer Validation**. 

# Trust Registry

A **Trust Registry** is an authoritative source that lists approved, recognized, and authorized VC issuers. It functions like a curated corporate phonebook or an official directory. While cryptographic verification proves that a credential has not been altered, a Trust Registry will verify that the issuer is who they claim to be.

# RCL VC Trust Registry

When an issuer creates a credential in the RCL VC Issuer application, the status of the issuer is initially set to ``Unknown Issuer``. The issuer must verify their identity through Issuer Validation from RCL. A valid issuer will be added to the Trust Registry and the status will be changed to ``Valid Issuer``.

# How to Validate an Issuer

To be added to the RCL VC Trust Registry, the issuer must make an application to the [RCL VC Trust Registry](https://trustregistry.vc.rclapp.com) website seeking validation.

Once the application is received, RCL will contact the issuer to verify their identity. Once the identity of the issuer is confirmed, the issuer will receive a **Validation Signature** and a **Valid Until** date signifying when the validation will expire.

The Validation Signature is created  by digitally signing the issuer's name, DID and valid until properties with RCL's private key. 

The RCL VC Verifier and RCL VC Wallet application both contain RCL's public key. These applications will verify the Validation Signature and change the status of the issuer to ``Valid Issuer``. The signature will be valid up to the date specified in the ``Valid Until`` property.

# Applying for Issuer Validation

## Creating an Issuer 

- Navigate to the [RCL VC Trust Registry](https://trustregistry.vc.rclapp.com) website

- Sign in to the website and navigate to the ``Portal``

- On the ``Issuers`` page, add a new issuer

- In the ``Add Issuer`` page, enter the Issuer Name, DID and Logo Image

- The new issuer will be added in the ``Issuers`` page

## Applying for a Validation

- In the ``Issuers`` page, click on the ``Validations`` link from the dropdown menu for a selected issuer

- In the ``Validations`` page, add a new validation

- In the ``Validation Options`` page, click the ``Buy Now`` button for a selected option

- In the ``Add Validation`` page, click on the ``Pay with Stripe`` button

- Complete the stripe payment

{: .information }
Payments and credit card processing is handled solely by [Stripe](https://stripe.com/). Do not enter credit card details on any RCL website pages nor does RCL store, view or process any credit card information during a payment. 

- In the ``Payment Complete`` page, click on the ``Continue`` button

- On the ``Issuers`` page, for the selected issuer, click on the ``Validations`` link in the drop down menu to navigate to the ``Validations`` page. It may take up to 15 mins for the new validation to appear in the validations list, so be patient

- The new validation will initially be in a ``pending`` state

- It may take up to 5 working days for RCL to validate the identity of a new issuer

- When the validation process is completed, click on the ``Details`` link in the dropdown link for a selected validation from the validations list

- In the ``Validations Details`` page, access the ``Validation Signature`` and the ``Valid Until`` property values

# Adding the Validation Properties to the RCL VC Issuer application

Once the values of the ``Validation Signature`` and ``Valid Until`` properties are obtained from the RCL VC Trust Registry, they must be entered in the Issuer application.

- In the RCL VC Issuer application, click on the ``Validation`` link in the left side menu

- Add a new validation

- Enter the values of the ``Validation Signature`` and ``Valid Until`` properties acquired from the RCL VC Trust Registry website. Click the ``Save`` button when completed

- If the ``Validation Signature`` and ``Valid Until`` property values are valid you will see the ``Valid Issuer`` status for the issuer

- After the validation expires, obtain a new validation and updated signature and date with the new values
