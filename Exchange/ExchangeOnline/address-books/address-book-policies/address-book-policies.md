---
localization_priority: Normal
description: Learn how to use address book policies (ABPs) to create separate virtual organizations with a segmented global address list in Exchange Online.
ms.topic: overview
author: chrisda
ms.author: chrisda
ms.assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms.date: 
ms.reviewer: 
title: Address book policies in Exchange Online
ms.collection: 
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
manager: dansimp

---

# Address book policies in Exchange Online

Address book policies (ABPs) lets admins segment users into specific groups to provide customized views of the organization's global address list (GAL). The goal of an ABP is to provide a simpler mechanism for GAL segmentation (also known as *GAL segregation*) in organizations that require multiple GALs.

An ABP contains these elements:

- One GAL. For more information about GALs, see [Default address lists in Exchange Online](../address-lists/address-lists.md#default-address-lists).

- One offline address book (OAB). For more information about OABs, see [Offline address books in Exchange Online](../offline-address-books/offline-address-books.md).

- One room list. Note that this room list is a custom address list that specifies rooms (contains the filter `RecipientDisplayType -eq 'ConferenceRoomMailbox'`). It's not a room finder that you create with the _RoomList_ switch on the **New-DistributionGroup** or **Set-DistributionGroup** cmdlet. For more information, see [Create and manage room mailboxes in Exchange Online](../../recipients-in-exchange-online/manage-room-mailboxes.md).

- One or more address lists. For more information about address lists, see [Custom Address Lists in Exchange Online](../address-lists/address-lists.md#custom-address-lists).

For procedures involving ABPs, see [Address book policy procedures in Exchange Online](address-book-policy-procedures.md).

 **Notes**:

- ABPs create only a virtual separation of users from a directory perspective, not a legal separation.

- Implementing an ABP is a multi-step process that requires planning. For more information, see [Scenario: Deploying Address Book Policies](https://technet.microsoft.com/library/6ac3c87d-161f-447b-afb2-149ae7e3f1dc.aspx).

## How ABPs Work

The following diagram shows how ABPs work. The user is assigned Address Book Policy A that contains a subset of address lists that are available in the organization. When the ABP is created and assigned to the user, the ABP becomes the scope of the address lists that the user is able to view.

![Overview of Address Book Policies](../../media/ITPro_Mailbox_ABPOverall.gif)

To turn on ABP email routing in your Exchange Online organization, see [Turn on address book policy routing in Exchange Online](turn-on-address-book-policy-routing.md).

To assign ABPs to users, see [Assign an address book policy to users in Exchange Online](assign-an-address-book-policy-to-mail-users.md).

APBs take effect when a user connects to their Exchange Online Mailbox. If you change an ABP, the updated APB takes effect when a user restarts or reconnects their email client app.

## ABP example

In the following diagram, Fabrikam and Tailspin Toys share the same Exchange Online organization and the same CEO. The CEO is the only employee common to both companies.

![Two Companies One CEO](../../media/ITPro_.gif)

The suggested configuration includes three ABPs:

- One ABP is assigned to Fabrikam employees. The GAL and address lists in the ABP include Fabrikam employees and the CEO.

- One ABP is assigned to Tailspin Toys employees. The GAL and address lists in the ABP include Tailspin Toys employees and the CEO.

- One ABP is assigned to only the CEO. The (default) GAL and address lists in the ABP include all employees (Fabrikam, Tailspin Toys, and the CEO).

Based on this configuration, the ABPs help to enforce these requirements:

- The users in Tailspin Toys can only see Tailspin Toys employees and the CEO when they browse the GAL.

- The users in Fabrikam can only see Fabrikam employees and the CEO when they browse the GAL.

- The CEO can see all Fabrikam and Tailspin Toys employees when she browses the GAL.

- Users who view the CEO's group membership can see only groups that belong to their company. They can't see groups that belong to the other company.

## ABPs for Entourage and Outlook for Mac users

Entourage and Outlook for Mac clients that connect to their Exchange Online mailboxes can use an OAB or Exchange Web Services (EWS), which allows them to search the GAL based on the assigned ABP.

In hybrid environments where the user account is in your on-premises organization and the mailbox is in Exchange Online, ABPs won't function for Entourage and Outlook for Mac users who connect to their mailboxes from inside the corporate network, because Entourage and Outlook for Mac connect directly to global a catalog server to query Active Directory (which bypasses the ABPs). Outside the corporate network, they can use an OAB or Exchange Web Services (EWS), which allows them to search the GAL based on the assigned ABP.

To learn more about administering Outlook for Mac 2011, see [Planning for Outlook for Mac 2011](https://go.microsoft.com/fwlink/p/?LinkId=231878).
