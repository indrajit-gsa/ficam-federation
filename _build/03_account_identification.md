---
layout: default
navtitle: Account Identification 
title: Account Identification 
permalink: build/account_identification/
---

- Audience: Engineer/Architect
- Define all the aspects of account identification and linking.
- Relying Party Section 7.2 - Account Management.

Account management will vary depending on the relationship between the user and the RP. This relationship will define the extent to which the RP will have predetermined information about the user. Five provisioning scenarios that describe these relationships include: 

> * Business-Entity Relationship with a Known User Base

> * Business-Entity Relationship with Indeterminate User Base 

> * Relationship with an Individual, Known User

> * Relationship with an Individual, Unknown User

> * Temporary Access Session

In the first two scenarios, where there is an existing relationship with a business entity, it’s likely that the credential being used for federation was issued by the business entity. Since these scenarios fall outside of accepting FICAM-approved third-party credentials, this playbook does not provide specific guidance on them.

The remaining three scenarios involve an individual user, in this case a non-federal user, and his/her relationship with an RP. These scenarios are discussed further in the following sections.

<div id="accordion" markdown="1">

### Relationship with an Individual, Known User
<div markdown="1">

This type of account management scenario requires that the user have a pre-existing relationship with the RP application and/or agency. That is, the user has interacted with the agency and the agency has a record of the user and certain attributes about the user. An example of this scenario is an agency that provides grants to a user. When the user requests a grant, he/she will provide information about himself/herself to the agency. This could result in the creation of an account at the RP application or the storage of the user’s information in a repository within the agency. In either of these cases, the agency retains the information about the user requesting a grant. Later when the user attempts to access the RP with a third-party credential, the RP can use this information to assist in account linking.

Provisioning of the RP account will occur prior to the user’s initial visit to the application with his/her third-party credential. This provisioning may occur during an out-of-band process such as the creation of the record for the user when he/she requested the grant in the example above; or by having the user manually visit the application and create an RP account using local credentials (e.g., username and password). Account linking occurs when the user visits the application with his/her third-party credential. If the assertion passed to the RP does not contain the attributes required to link the user’s identity from the CSP to the RP account, the RP will need to identity proof the user. After the RP identity proofs the user, unique attributes from the assertion are associated with the RP account. This association, or linking, will be persistent at the RP, which allows future access attempts with the given credential to succeed without requiring the identity proofing step.

The chart below provides a summary of the known user account management activities.

<br>

| <center> Activity </center> | <center> Description </center> |
|:---------------------------:|--------------------------------|
| **Provisioning** | Occurs prior to the user’s first attempt to access the application with a third-party credential. The Relying Party (RP) account is created, but no credential, or only a local credential, is associated with the account. |
| **Account Linking** | Upon the first attempt to access the application, the user’s credential is associated with his/her RP account. Additional credentials can be associated with an RP account at any time, if the application employs the single account multiple credentials pattern. |
| **Account Maintenance** | The implementation of these activities is at the discretion of the RP. |

<br>

</div>

### Relationship with an Individual, Unknown User
<div markdown="1">

This type of account management scenario does not require the RP account to be provisioned before the user’s initial visit to the application with his/her third-party credential. An example of this scenario is a user that attempts to access the application without being known by the agency. The RP application will receive an assertion from a CSP about the user. At this time, the RP will create a “shadow account”, which is an RP account that is created for the purpose of maintaining a persistent association with an external user. The unique identifier within the assertion is linked to the shadow account.

<br>

<div style="background-color: #edf1f3;color: black;margin: 10px;padding: 10px">

<h3><span>Lesson Learned</span></h3>
<p><span>Research.gov, National Science Foundation’s (NSF) grants management system, successfully allows first-time visitors to use an OpenID credential (e.g. Google) to access NSF visitor services. By provisioning the user’s account to the application, NSF allows the user to personalize his/her experience for future visits, including a personalized homepage, up-to-date Research.gov news, and information through Rich Site Summary (RSS) feeds and email alerts.</span></p>

</div>

<br>

In this scenario, if the RP received enough information from the assertion to uniquely identify the user, the RP will create a local RP account. Since this activity happens dynamically as the assertion is received, it’s referred to as just-in-time provisioning. If the RP requires additional information to uniquely identify the user, then provisioning does not occur when the assertion is received. Instead, the RP will collect this information using either automatic collection, prompted collection, deferred collection, or a hybrid collection approach. 

The RP should only collect the minimum amount of information that is required for the user to perform a transaction with the RP. The RP will perform a level of identity proofing to vet the information obtained about the user. This can be achieved by leveraging a trusted third party or by conducting identity proofing in person. Upon completion of the identity proofing, the RP will provision an RP account for the user. This is referred to as deferred provisioning, since the provisioning activities occur at a time later than when the initial assertion is received.

Account linking takes place immediately after provisioning, associating unique attributes contained in the assertion from the CSP to the RP account that was just created. Similar to the known user scenario described earlier, the association of the CSP account to the RP account is persistent; allowing future access attempts with the given credential to succeed without requiring the identity proofing step. The chart below provides a summary of the known user account management activities.

</div>

### Temporary Access Station 
<div markdown="1">

This type of account management scenario does not require provisioning of a permanent RP account. Some applications can provide access to the user without provisioning an account. Other applications, however, may need to provision a temporary account for the user, which will be removed when the user terminates his/her session with the application. The key difference between the temporary access scenario and other scenarios is that the user’s information does not persist from session to session for the user.

<br>

| <center> Activity </center> | <center> Description </center> |
|:---------------------------:|--------------------------------|
| **Provisioning** | Depending on the application implementation, a temporary account may or may not be created. If it’s created, the account only exists for the duration of the user’s session. |
| **Account Linking** | N/A |
| **Account Maintenance** | The implementation of these activities is at the discretion of the RP. |

<br>

</div>
</div>
















