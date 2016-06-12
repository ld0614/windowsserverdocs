---
title: Deploy the applocker Policy into Production
ms.custom: na
ms.prod: windows-server-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 26fd78e0-393d-4dec-b96a-66fe81c366c3
---
# Deploy the applocker Policy into Production
This topic for the IT professional describes the tasks that should be completed before you deploy applocker application control settings.

After successfully testing and modifying the applocker policy for each Group Policy Object \(GPO\), you are ready to deploy the enforcement settings into production. For most organizations, this means switching the applocker enforcement setting from **Audit only** to **Enforce rules**. However, it is important to follow the deployment plan that you created earlier. For more information, see the [applocker Policies Design Guide](). Depending on the needs of different business groups in your organization, you might deploy different enforcement settings for linked GPOs.

### Understand your design decisions
Before you deploy an applocker policy, you should determine:

-   For each business group, which applications will be controlled and in what manner. For more information, see [Create List of Applications Deployed to Each Business Group]().

-   How to handle requests for application access. For information about what to consider when developing your support policies, see [Plan for applocker Policy Management]().

-   How to manage events, including forwarding events. For information about event management in applocker, see [Monitor Application Usage with applocker]().

-   Your GPO structure, including how to include policies generated by Software Restriction Policies and applocker policies. For more information, see [Determine Group Policy Structure and Rule Enforcement]().

For information about how applocker deployment is dependent on design decisions, see [Understand applocker Policy Design Decisions]().

### applocker deployment methods
If you have configured a reference computer, you can create and update your applocker policies on this computer, test the policies, and then export the policies to the appropriate GPO for distribution. Another method is to create the policies and set the enforcement setting on **Audit only**, then observe the events that are generated.

-   [Use a Reference Computer to Create and Maintain applocker Policies]()

    This topic describes the steps to use an applocker reference computer to prepare application control policies for deployment by using Group Policy or other means.

-   [Deploy applocker Policies by Using the Enforce Rules Setting]()

    This topic describes the steps to deploy the applocker policy by changing the enforcement setting to **Audit only** or to **Enforce rules**.

## See also
[applocker Policies Deployment Guide]()

