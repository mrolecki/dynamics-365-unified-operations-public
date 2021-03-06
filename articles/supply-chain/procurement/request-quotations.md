---
# required metadata

title: Requests for quotation (RFQs)
description: This topic provides an overview of requests for quotation (RFQs). Organizations issue RFQs when they want to receive competitive offers from several vendors for the items or services that they must purchase.
author: mkirknel
manager: AnnBe
ms.date: 06/20/2017
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

ms.search.form: PurchRFQCaseTable, PurchRFQCaseTableListPage, PurchRFQCompare, PurchRFQReplyTable, PurchRFQVendReplyTableListPage
# ROBOTS: 
audience: Application User
# ms.devlang: 
ms.reviewer: yuyus
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 2154
ms.assetid: 3936996e-d943-46ca-8385-84c042990f1d
ms.search.region: Global
# ms.search.industry: 
ms.author: mkirknel
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0

---

# Requests for quotation (RFQs)

[!include[banner](../includes/banner.md)]

This topic provides an overview of requests for quotation (RFQs). Organizations issue RFQs when they want to receive competitive offers from several vendors for the items or services that they must purchase. In an RFQ, you ask vendors to provide the prices and delivery times for the item quantities that you specify. You can also ask vendors to specify whether there are any incidental charges, such as shipping costs, or any discounts for large orders or early payment of the vendor invoice.

The RFQ process consists of the following tasks:

1. Create and send an RFQ to one or more vendors.
2. Receive and register RFQ replies (bids).
3. Transfer bids that you accept to a purchase order, purchase agreement, or purchase requisition.

The following illustration shows an overview of the RFQ process.

[![RFQ process](./media/rfq-process-458x1024.jpg)](./media/rfq-process.jpg)

You can create an RFQ from planned orders, from a purchase requisition, or by manual entry. The RFQ that you create is called an RFQ case. The RFQ case is the base document that you use to issue an RFQ to each vendor.

After you prepare the RFQ case and add vendors, select **Send** on the RFQ case. An RFQ journal is generated for each vendor that you sent the RFQ to. You can configure the Print management settings for the Send action so that it either prints a report for each vendor to an archive or sends a report to each vendor's email address. In addition, you can use the RFQ journal for each vendor to generate a report that you can send or resend to the vendor later. You can also configure the Send action so that it generates a reply sheet that the vendor can fill in.

This topic covers the process for handling RFQs when vendor collaboration isn't used. If your system is set up for vendor collaboration, vendors can enter bids directly in Microsoft Dynamics 365 for Finance and Operations, Enterprise edition. For more information, see [Vendor collaboration with customers](vendor-collaboration-work-customers-dynamics-365-operations.md).
 
If you must amend an RFQ after you send it, you can resend the RFQ to vendors when you've finished by using the two amendment actions: Create and Finalize.

When you receive bids by email, you must enter them on the **Request for quotation replies** page. If you select the **Copy data to reply** option, data such as the quantity and dates from the RFQ case is copied into the reply. You can change this data to reflect the vendor's bid.

If a second iteration of a reply is required for a vendor, select **Return** on the **Request for quotation reply** page. The Return action generates a new journal and a report that will be printed, archived, and sent according to your Print management settings.

If you added scoring criteria to your RFQ case, the RFQ reply will have a scoring panel where you can enter the scores. The total scores will appear when you compare the replies on the **Compare replies** page. On that page, you can also compare other reply data, such as the line price, delivery date, and total price.

After you choose a bid or partial bids, you can accept them and reject the rest. Acceptance journals, rejection journals, and corresponding reports are generated, and will be printed, archived, and sent according to your Print management settings. When you accept a bid or specific lines in a bid, either a purchase agreement or a purchase order is generated, or a purchase requisition is updated, depending on the purchase type of the RFQ. You can create a trade agreement that you can use later for any of the replies, regardless of whether you accepted or rejected them.

The status of an RFQ appears on the RFQ header and depends on the status of the RFQ lines. The status indicates how much you've processed the RFQ. Each RFQ has two values for the status: a lowest status and a highest status. The lowest status is the least advanced stage of any line in the RFQ, and the highest status is the most advanced stage of any line in the RFQ. For example, if the least advanced stage in an RFQ is for a line that has been created, the lowest status for the RFQ is **Created**. If the most advanced stage in the RFQ is for a line that has been sent to vendors, the highest status for the RFQ is **Sent**. The statuses are automatically updated as you process an RFQ.

You can view the lowest and highest statuses for an RFQ header on the **All requests for quotations** page. You can view the lowest and highest statuses for an RFQ line on the **Lines** tab on the **Request for quotations** page.

Here is the sequence of statuses for RFQ processing:

1. **Created**
2. **Sent**
3. **Received**
4. **Accepted**, **Canceled**, or **Rejected**

These statuses will be described in more detail later in this topic.

## Setting up RFQ functionality

Before you can create an RFQ case, you must set up RFQ information on the **Procurement and sourcing parameters** page. When you create an RFQ case, you can specify default values that are copied to the RFQ. You can specify the following default values:

- The purchase type of new RFQs: **Purchase order** or **Purchase agreement**
- The expiration date and time
- Delivery information and payment terms
- Fields that should be included in the RFQ reply

You can override these values for a specific RFQ case.

You should also configure the amendment process. As part of this configuration, you can turn on field locking. When field locking is turned on, a procurement professional who wants to amend an RFQ must first select **Create** in the **Amendment** section of the **Quotation** tab. Then, after the RFQ has been updated with the amendment, the procurement professional must complete the process by selecting **Finalize**. The Finalize action generates an email that notifies the vendors about the amended RFQ.

On the **Procurement and sourcing parameters** page, you select the template to use for the email notification that is sent to vendors. When a template is created, it can contain the following replacement tokens:

- %RFQ case%
- %Reason for bid return%
- %Reason for amendment%
- %Amendment prepared by%
- %Company%
- %RFQ case name%
- %ExpiryDateTime%
- %Date%

The %Reason for bid return% and %Reason for amendment% tokens are replaced by text that the procurement professional can enter when he or she completes the amendment in the **Amendment** wizard. The values for the %Amendment prepared by% and %Company% tokens are automatically taken from the RFQ. The %Date% token is replaced by the current date.

An email template is also required if you cancel an RFQ after it has been sent. This email template is used to send the cancellation notification to the vendor's contact persons. The template must be selected on the **Procurement and sourcing parameters** page. When the template is created, it can contain the following replacements tokens:

- %Reason for cancellation%
- %RFQ case% 
- %RFQ cancelled by%
- %Company%
- %RFQ case name%
- %Date%

The %Reason for cancellation% token is replaced by text that the procurement professional can enter in the **Cancellation** wizard. The %Date% token is replaced by the current date.

If you want to use reason codes on a RFQ reply to indicate why a bid was rejected or accepted, you must set up reason codes on the **Vendor reasons** page.

On the **Form setup** page in Procurement and sourcing, you can configure the appearance of your printed or stored RFQ documents.

> [!NOTE]
> For a public-sector configuration, you must use the amendment process to change an RFQ that has already been sent. When an RFQ is sent, fields are locked. Therefore, to make changes to the RFQ, you must select **Create** to start the amendment process, as described earlier. The locking behavior is controlled by the **Lock RFQ when they are sent** option on the **Procurement and sourcing parameters** page. By default, this parameter is set to **Yes**, and for a public-sector configuration, the default setting can't be changed. Therefore, although the amendment process can be handled manually in a non-public-sector configuration, it must be used for a public-sector configuration.

When you create an RFQ for a purchase order and add an inventory item to the RFQ, an inventory transaction is generated that has a receipt status of **Quotation receipt**. Only RFQ lines that have this status are considered when you use a master plan to calculate supplies. If you want the master plan to include RFQ lines as an expected receipt, you must configure this behavior in the setup of master planning.

A purchasing manager or agent can create and maintain solicitation types to suit the organization's procurement requirements. Each solicitation type can be associated with a scoring method. Scoring methods consist of a set of criteria that can be used when you score bids. You must set up solicitation types, scoring methods, and scoring criteria on the **Solicitation type** and **Scoring method** pages.

## Creating and sending an RFQ

You create an RFQ, select the vendors that you want to bid on the RFQ, and then send the RFQ to the vendors. You can use Print management to route the RFQ report and reply sheet reports to your preferred destination.

You can create an RFQ of either the **Purchase order** purchase type or the **Purchase agreement** purchase type.

If the RFQ is of the **Purchase order** type, the following behavior occurs:

- When RFQ lines are created, inventory transactions are generated that have a receipt status of **Quotation receipt**.
- When you accept a bid, a purchase order is generated.

If the RFQ is of the **Purchase agreement** type, the following behavior occurs:

- The RFQ is used for an agreement to purchase a specific quantity or value of product over time. You must select the date range that applies to the purchase agreement and the name of the person who manages the purchase agreement.
- When you accept a bid, a purchase agreement is generated.

If the RFQ is generated from a purchase requisition, the **Purchase requisition** type is automatically assigned. You can't manually create an RFQ of the **Purchase requisition** type.

You can create an RFQ from a purchase requisition only if the status of the purchase requisition is **In review** and you're assigned to do the next workflow task. The lines in the purchase requisition are automatically updated as you accept lines from RFQ replies (bids) that you received from vendors. You can't complete, reject, approve, or perform any other actions on the purchase requisition while the RFQ is in progress.

When you create an RFQ, you can select a solicitation type. The solicitation type determines the set of scoring criteria that is used to score replies to the RFQ.

You can add a questionnaire to an RFQ case. This questionnaire then appears on all replies after you send the RFQ.

There are three ways to select the vendors to add to an RFQ case:

- Add the vendors one by one.
- Search for all vendors that meet specific criteria.
- Automatically add all vendors that are approved for the procurement categories that are used on the RFQ lines.

When the RFQ case is ready, select **Send**. The Send action generates journals and reports that will be printed, archived, and sent according to your Print management settings.

If you set **Use vendor for recalculating prices** and **Use vendor specific item information** to **Yes** on the **Sending request for quotation** page when you sent the RFQ to vendors, some vendor-specific information is automatically entered. You can modify this information on the **Request for quotation reply** page.

The following table shows how the RFQ status changes when you create an RFQ and send it to vendors.

| Action                             | Lowest RFQ header status | Highest RFQ header status                        | Lowest RFQ line status | Highest RFQ line status |
|------------------------------------|--------------------------|--------------------------------------------------|------------------------|-------------------------|
| Create the RFQ header and line.    | Created                  | Created                                          | Created                | Created |
| Send the RFQ to a specific vendor. | Sent                     | Sent                                             | Sent                   | Sent |
| Add another vendor.                | Created                  | Sent (The RFQ has been sent to only one vendor.) | Created                | Sent |
| Send the RFQ to the second vendor. | Sent                     | Sent                                             | Sent                   | Sent |

> [!NOTE]
> You can add more vendors to an RFQ at any time, and the lowest and highest statuses are updated to reflect the new vendors. For example, if you received bids from all vendors and accepted at least one line on a bid, the lowest status in the RFQ header is **Rejected**, and the highest status is **Accepted**. If you add a new vendor, the lowest status on any line is now **Created**. Therefore, the lowest status in the RFQ header is updated to **Created**, but the highest status remains **Accepted**.

## Amending an RFQ

Occasionally, you must change an RFQ after you send it. You might have to change an RFQ if, for example, the delivery dates have changed, or you want additional products or different quantities of products. You can configure the amendment process so that it's either more restrictive or less restrictive.

If you configure the amendment process so that it's more restrictive, before you can modify the fields on an RFQ case that has already been sent, you must select **Create** on the RFQ case to start an amendment. After you've completed your changes, you must select **Finalize**. You're then guided through the process of adding information for the email that is sent to notify vendors about the amendment. The updated RFQ report, which includes an amendment note, is automatically attached to the email.

If you configure the amendment process so that it's less restrictive, you don't have to select **Create** before you can modify the fields on an RFQ case that has already been sent. However, you must manually add an amendment note on the RFQ and send the case again. Be aware that this approach can be used only if none of the replies (bids) have been edited. If you've entered a reply and it's in a **Received** state, the **Send** button is unavailable. In this case, you must select **Create** and then **Finalize**, as you must do in the more restrictive process. The reply is then reset to reflect the changes to the RFQ case. 

If vendors use the vendor collaboration interface to enter bids, you must always use the amendment process to notify vendors about changes to the RFQ case. This requirement helps prevent the situation where vendors bid on an outdated RFQ case while their bid is in progress. For more information about vendor collaboration, see [Vendor collaboration with external vendors](vendor-collaboration-work-external-vendors.md). 

If you want to invite additional vendors to bid, and no changes have been made to the RFQ case, you can use the **Send** button. The vendors that you added will appear on the **Send** page and will receive the email invitation.

## Receiving and registering RFQ replies

When you send an RFQ, a reply sheet is automatically generated. As you receive replies (bids) to an RFQ, you must enter the information from each vendor on a vendor-specific RFQ reply sheet. If you've added scoring criteria, you can score the replies. You then compare the vendor bids and rank them according to your scoring criteria, such as best total price or best total delivery time.

If a questionnaire is attached to the RFQ case, you must manually enter the answers to the questions on the reply sheet.

You can also enter alternate lines, if the RFQ case allows for alternate lines. On the **Purchase quotation lines** FastTab, select **Add line**. Then enter the product information, such as the item number or procurement category, quantity, price, and discount.

If you've entered a reply but require a new offer from the vendor, you can resend the RFQ. A new journal and report are generated, and you can use them to request changes from the vendor.

You can see an overview of all RFQs and their reply statuses on the **Request for quotation follow-up** page.

The following table shows how the RFQ status changes as you receive bids and register the information on the RFQ reply sheet.

| Action                                         | Lowest bid status | Highest bid status | Lowest RFQ header status | Highest RFQ header status | Lowest RFQ line status | Highest RFQ line status |
|------------------------------------------------|-------------------|--------------------|--------------------------|---------------------------|------------------------|-------------------------|
| Register one vendor's bid, and save it.        | Sent              | Received           | Sent                     | Received                  | Sent                   | Received |
| Register the second vendor's bid, and save it. | Received          | Received           | Received                 | Received                  | Received               | Received |

> [!NOTE]
> If you return a bid to a vendor for additional negotiation, the lowest and highest statuses both remain **Received**.

### Accepting and rejecting bids, and transferring accepted bids to downstream documents

After you've identified the best bid, such as the bid that offers the best total price, you accept the bid. You can accept some lines in a bid and reject others. You can also accept lines from different vendors. Be aware that if you accept some lines, you're prompted to reject all the other lines. Therefore, if you want to accept other lines, you must select **Cancel** when you're prompted. The status of the RFQ reply for each vendor that you accept bids or lines from is updated to **Accepted**. 

When you accept a bid or specific lines in a bid, a purchase order or purchase agreement is automatically generated. You can then reject the bids from all the other vendors.

On the reply, you can add a reason code to explain why you accepted or rejected a bid.

When you accept an RFQ reply of the **Purchase requisition** type, the RFQ reply lines update the purchase requisition lines with the following information:

- Unit price
- Discount percentage
- Discount amount
- Purchase charges
- Line charges
- Vendor
- External number
- External description

The following table shows how the RFQ status changes as you accept and reject bids from vendors.

| Action                      | Lowest bid status | Highest bid status | Lowest RFQ header status | Highest RFQ header status | Lowest RFQ line status | Highest RFQ line status |
|-------------------------    |-------------------|--------------------|--------------------------|---------------------------|------------------------|-------------------------|
| Accept one of the bids.     | Received          | Accepted           | Received                 | Accepted                  | Received               | Accepted |
| Reject all the other bids.  | Rejected          | Accepted           | Rejected                 | Accepted                  | Rejected               | Accepted |
