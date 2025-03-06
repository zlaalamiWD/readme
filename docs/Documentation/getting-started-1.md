---
title: Getting Started
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
# Context of this guide

This API Guide is an instruction manual for using HealthDyne API and building functional integration quickly and  
easily. The document contains examples of commonly used API, how they work and behave, and best practices  
for integrating into developer code.

# Intended audience

The API Guide is for internal and external use. The primary audience is HealthDyne client software development  
teams and the HealthDyne Common Services Delivery team as well as prospective and current clients.

# Support Contact

Your Client Account team will serve as the point of contact and will be responsible for facilitating communication  
between you and our IT team.

# HIPAA and Security

HealthDyne is committed to the security and confidentiality of Personal Health Information (PHI). As part of the API requests, through the shipping and fulfillment of the medication, HealthDyne ensures that data integrity is secure.

HealthDyne has established a set of policies and procedures to protect itsphysical and technical infrastructure to maintain compliance with the HIPAA Privacy Rule, Security Rule, Transactions and Code Sets Rule, and necessary implementation requirements.

The HealthDyne privacy policy is published and available on its corporate website at HealthDyne.com. HealthDyne uses trusted HIPAA compliance cloud infrastructure. All API requests are transmitted over TLS1.2 protocol and all data is encrypted.

# Testing Environment

HealthDyne has a separate private network for Production and Testing environments where clients can test API URL requests in a secure environment without impacting any Production data. The test environment uses non-production simulated data and error events which our partners can use to test the end-to-end experience. Clients should not send any PHI/Production data to lower environments. Lower environments are intended for sample data only.

# API Authentication and Authorization

HealthDyne secures access to pharmacy APIs via a subscription key which is to be used for authentication and authorization.