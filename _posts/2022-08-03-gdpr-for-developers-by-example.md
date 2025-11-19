---
layout: post
title: GDPR For Developers By Example
authors: [iain]
categories: [Privacy, GDPR]
date: "2022-08-03"
---
GDPR has been in place for years now, and we’re starting to learn more and more about how it’s going to be enforced and what it really means. The many questions people had that could only be answered by court decisions have now been answered. Over the past years, I’ve seen systems try and fail to correct implement GDPR. Here are the things I’ve learnt from court decisions and from mistakes made.

<!--truncate-->
## The right to deletion

One of the most well-known rights GDPR provides is the right to be deleted. This is where you must delete data relating to a user on demand.

### Void if they’ve used a paid service

One big thing with this right is that it does not override other laws or legal rights of the company. Countries such as Germany have a legal requirement to keep all data relating to financial transactions. GDPR also gives an exemption when it’s being held for legal defence purposes. What this means, in reality, is once a user has paid you the money, you need to keep their data. Their right to demand their data be deleted doesn’t matter as the other legal rights override it.

#### Examples:

**Scenario:** A user who has paid for a subscription then cancels it wishes their data to be deleted.  
**Outcome:** The information is not deleted as it is required to defend any possible future legal action.  
**Why:** The user then forgets they used the service and months later does a chargeback. Without the information, you’re unable to prove they used the service. This legal right overrides the GDPR requirement.

**Scenario:** A user who has only used the free plan wishes their data to be deleted.  
**Outcome:** The information is to be deleted.  
**Why:** There is no legal requirement overriding the GDPR right to deletion.  

**Scenario:** A user who hasn’t bought anything themselves but is a member of a paid service for another user requests to be deleted.  
**Outcome:** The information is not deleted as it is required in relation to the user who has paid.  
**Why:** The user who has paid may request more information about services the deleted user uses, and when you can’t provide any, they’ll refuse to pay. This legal right overrides the GDPR requirement.  

### Delete from newsletters list and other third parties as well.

The right to be deleted when executed also includes the third-party data processors you have processing data on your behalf when technically feasible. This may be one of the most forgotten aspects of deleting user data. In many systems, they only focus on deleting data they have and processing and forget about their data processors.

#### Examples

**Scenario:** You use a newsletter system.  
**Outcome:** The user should be removed from the newsletter system.  
**Why:** You no longer have consent to send them emails or process their personal data.

**Scenario:** You use a logging system  
**Outcome:** The logs are not affected by the deletion request  
**Why:** It is often not technically feasible to delete logs, and you have a legitimate need to maintain the historical accuracy of your logs.

**Scenario:** You have backups  
**Outcome:** The backups are not affected by the deletion request. However, you have to be able to ensure if a backup is restored, the data is removed upon restoration.  
**Why:** It is not technically feasible to remove the data from backups. And if you restore the data, the user’s deletion request is still valid.

### Can be done via a request - does not have to be automated.

Many of the major sites allow you to delete your data at the click of a button. It is possible that you make it a manual action that is done when the user clicks a button within the system. While this is the most user-friendly way, if you’re just starting out and don’t have the time and resources to focus on building this, then it can be done manually. The act of requesting of the deletion must be easy and not have hurdles, as making the process harder and more time-consuming would breach this right.

#### Examples

**Scenario:** The user clicks a button within their account settings  
**Outcome:** Compliant  
**Why:** It was processed without undue delay

**Scenario:** The user emails customer support, and customer support click a button in the admin system.  
**Outcome:** Compliant  
**Why:** It was processed without undue delay

**Scenario:** The user has to write a letter to customer support, and customer support clicks a button in the admin system.  
**Outcome:** Not Compliant  
**Why:** There was an undue delay in the customer being able to request the deletion.

**Scenario:** The user emails customer support, and then customer support creates a ticket for the technical team to delete the data, and it’s processed that week.  
**Outcome:** Compliant  
**Why:** It was processed without undue delay

**Scenario:** The user emails customer support, and then customer support creates a ticket for the technical team to delete the data, and it’s processed a month later.  
**Outcome:** Not Compliant  
**Why:** It was not processed without undue delay.

## Cookie Law

The cookie law is a requirement to get consent to use cookies on a website for anything that isn’t functionally required and inform the user about the data that is being written and retrieved from their computer.
The cookie law consent isn’t GDPR.

One of the things many people complain about in relation to GDPR is that sites ask for consent and have popups for cookies. The requirement to get consent for cookies is not part of GDPR. It’s actually a separate law, which is known as the cookie law.

### The Cookie consent isn’t just for cookies.

While it’s commonly called the cookie law, it actually covers anything where you’re storing and/or retrieving data on the user’s computer. This includes localStorage and other methods of storing and retrieving data from the user's computer.

So switching over to using localStorage isn’t a valid loophole that some believe it is.

#### Examples:

**Scenario:** You have an app that stores data in a cookie  
**Outcome:** You need consent if not functionally required  
**Why:** You are writing data to the user's computer

**Scenario:** You have a flash app that stores high scores on the user's computer  
**Outcome:** You need consent  
**Why:** You’re writing data to the user’s computer

**Scenario:** You have an app that only stores data in the cloud  
**Outcome:** No consent is required  
**Why:** You’re not storing data on the user’s computer but on your own computer.

### If technically required to fulfil the user's actions, no consent is required.

While creating the cookie law, lawmakers understood that some cookies are literally required in order for the site to function properly. For this reason, they created exemptions that cookies that are functionally required don’t need to be consented to in order to be used.

#### Example of functionality required cookies:

* Keeping track of cookie consent
* Loadbalancing cookies
* Cookies to keep track of the user session when they’ve logged in
* Cookies to keep track of a user's shopping cart

Analytics is explicitly defined as not a valid functional requirement, and Analytic cookies must be consented to.

#### Examples:

**Scenario:** You have a login system and use cookies to keep track of the logged-in user.  
**Outcome:** No consent is required  
**Why:** It is required in order to know who is logged in, and the user has implicitly agreed when logging in.

**Scenario:** You have a checkout basket, and you need cookies to track the user's basket  
**Outcome:** No consent is required  
**Why:** It is required to ensure the user keeps their basket between requests.

**Scenario:** You have a cookie for getting track of independent user sessions  
**Outcome:** Consent is required  
**Why:** Because analytics is not required in order for the site to function.

## Consent Banners

One of the main things with GDPR is the informed consent of the user on how their data will be processed, and with the cookie law, this means if you’re using a third party tool to add extra value to your business flow, then you need to allow the user to make an informed decision on if it is added or not.

### You must get consent before they’re included.

You must get consent before you activate the features you need to get consent for. This is probably the most common mistake when using consent banners. They have a consent banner, but they’ve already loaded everything before you’ve even clicked anything.

#### Examples

**Scenario:** You want consent to use Google Fonts  
**Outcome:** You can’t include the Google Font CSS until you have consent  
**Why:** You don’t have consent to allow Google to process the IP, which is considered personal data

**Scenario:** You want to use a service that uses cookies  
**Outcome:** The cookies must not be set until you have consent to store and retrieve data from the user’s computer
You must be able to allow them to reject

### You must allow them to refuse consent

A user must be able to reject whatever you wish then to consent to. Consent must be given willingly and refusing consent must not lead to negative consequences.

#### Examples

**Scenario:** You only provide an ok button on your consent banner  
**Outcome:** You’re not compliant with GDPR  
**Why:** The user must be able to refuse consent

**Scenario:** You provide an ok button and a reject button that the user needs to navigate and find  
**Outcome:** You’re not compliant with GDPR  
**Why:** The ability to reject but be allowed with undue delay, making it harder to reject than accept, is creating an undue delay.

**Scenario:** You provide an ok button, and next to it is a reject all button  
**Outcome:** You’re compliant with GDPR  
**Why:** You can accept and reject without undue delay

### The user must be able to understand what they’re consenting to

The user must be provided in clear language who is going to process the data, what data they will be processing and for which reasons the data will be processed for.

#### Examples

**Scenario:** You give a confusing unclear explanation of what data is used and by whom  
**Outcome:** You’re not compliant  
**Why:** You must provide a clear and unambiguous explanation of what is used and by whom.

**Scenario:** You provide a list of companies who will be processing data, listing what data they will get and the reason they need that data.  
**Outcome:** You’re compliant  
**Why:** You have provided who will be processing the data, what data they will be processing, and why they will be processing the data.


### The user must be able to withdraw consent.

You must gain the user’s consent, but an important aspect is the user must be able to change their minds and withdraw consent. If you only allow a user to give or deny consent once but don’t allow them to change their preferences, you would fail to allow the user to withdraw consent for how their personal data is used.

#### Examples

**Scenario:** You allow people to sign up for a newsletter but don’t allow them to unsubscribe  
**Outcome:** You’re not compliant  
**Why:** You don’t allow the user to withdraw their consent to use their email for marketing purposes.

**Scenario:** You have a consent banner that is only viewable when the user first arrives  
**Outcome:** You’re not compliant  
**Why:** You don’t allow the user to withdraw consent to use their personal data for analytic purposes.

### Not everything requires consent.

There are many cases where you don’t actually have to gain the consent of the user to process their personal data or to do something. GDPR has quite a few exceptions. If you need something because otherwise, your application won’t work, then consent isn’t required. If you need to do something because you have a contract with their employer and to fulfil the contract with their employer you.

#### Examples

**Scenario:** You have a contract with the person’s employer to provide them with a service  
**Outcome:** You don’t need the person’s consent to process their data  
**Why:** You need to process their data to fulfil the contractual obligations with the employer

**Scenario:** You need to process the personal data of employees to ensure they’re taking time off  
**Outcome:** You don’t need the person’s consent to process their data  
**Why:** You have a legitimate need and need to process the data to fulfil a legal obligation

**Scenario:** You want to process the personal data to know how many employees have an A as the second letter of their first name.  
**Outcome:** You need their consent  
**Why:** You don’t have a legitimate need

**Scenario:** You need to process a customer's personal data for fraud prevention  
**Outcome:** You don’t need their consent  
**Why:** You have a legitimate need

**Scenario:** You want to process a customer’s data to know when to send the coupons  
**Outcome:** You need consent  
**Why:** The need is not essential to the running of the business

### An invalid consent banner may as well not exist.

Having a consent banner that is invalid doesn’t protect you or reduce your fines. There isn’t a percentage of complying with the law. Amazon got fined €35 million because their cookie consent banner was invalid. If your consent banner isn’t 100% compliant, you’re liable for fines. This is why major companies outsource the compliance banner to another company, so the other company handles the pain of ensuring compliance while the original company focuses on what they’re in the business to do.

#### Examples

**Scenario:** You include third-party code that needs consent before you get consent  
**Outcome:** You’re not compliant and can be fined  
**Why:** Because you didn’t get consent before you applied the third-party code that needed consent

**Scenario:** You only allow people to accept  
**Outcome:** You are not compliant and can be fined  
**Why:** Because people are not able to refuse consent

**Scenario:** You send people away from your site if they refuse consent  
**Outcome:** You are not compliant and can be fined  
**Why:** They must be able to refuse consent without any downsides. Consent must be freely given

**Scenario:** You don’t allow people to change their consent status  
**Outcome:** You are not compliant and can be fined  
**Why:** Because you don’t allow people to withdraw consent after it’s given

**Scenario:** You make it harder to refuse consent  
**Outcome:** You are not compliant and can be fined   
**Why:** Because there should not be negative consequences for refusing consent

## Conclusion

This is just a small part of the GDPR requirements. I will follow up with the rest in the near future.

Last thing, I am not a lawyer, if you're wanting to be 100% safe always ask for the opinion of the lawyer you would use to defend you.

If you're wondering how Parthenon helps with GDPR, it has build in user export and deletion functionality.
