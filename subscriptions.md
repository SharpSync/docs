# Subscriptions
SharpSync is free to register and try, but you will be unable to submit any of the final data to a datasource.

The functionality matrix below details the difference between the versions

|Function|Free Version|Paid Version|
|:--|:--:|:--:|
| <li>Configure datasources (see our available datasources)|:white_check_mark:|:white_check_mark:|
| <li>Configure property mappings| :white_check_mark: |:white_check_mark:|
| <li>Configure rule mappings|:white_check_mark:|:white_check_mark:|
| <li>Pull data from online datasources|:white_check_mark:|:white_check_mark:|
| <li>Use data from static files (csv)|:white_check_mark:|:white_check_mark:|
| <li>View the data in the BOM compare |:white_check_mark:|:white_check_mark:|
| <li>Refresh / reload data in the BOM compare |:white_check_mark:|:white_check_mark:|
| <li> Submit the data to datasource|  |:white_check_mark:|

<br/><br/>
Subscriptions are a way for a customer to make full use of the software after trialing it. Sometimes your not ready to commit to a payment yet - that's ok. Reach out to us on slack and we'll gladly assist with any queries

## Subscription scenarios

To explain what the different options are, below you will find some scenarios to illustrate how a customer may make use of subscriptions. Note that a subscription is a recurring payment that is made on an annual basis for the maintenance and use of the software.

### Scenario: Free trial - no subscription
You have registered with SharpSync and have tried out some of the features. No payment is required, but you have an upper limit of 5 BOMs that you can submit and play around with.

### Scenario: Signup
You have registered with SharpSync, tested the features to your heart's content, and wish to subscribe to the application.
* Navigate to Organization > Fill in the required billing details
* Navigate to Billing > The base plan is already chosen (this includes a single user)
* Choose the number of users in addition to the base plan (e.g. if you pick 2 here, you'll have access to 3 users total)
* Click the subscribe button
* Confirm your details
* Make a payment
* Result: You're all set 

Let's say that you signed up on January 1st. The software will include the paid for functions from Jan 1st to December 31st. On Dec 31st your subscription renewal is due should you wish to continue. Subscription is done through Stripe, so renewals are automatic unless you explicitly cancel
 

### Scenario:  Renewal
You have registered with SharpSync on the base plan as shown above.
Result: On Jan 1 of next year the subscription automatically renews, no need to do anything

###  Scenario: Addition of more users
You have registered with SharpSync on the base plan as shown above.
In June you require access for an additional 2 users on top of the initial single user. You make the change in the app using Billing > modify.

Result: The new users are added and your maximum number of simultaneous users is incremented to 3. Your customer profile is billed upfront for the difference till the end of the base plan interval, so the equation is

`{additional user price per month}` x `{number of users}` x `{months remaining in the interval}`

Considering that you started in Jan,  and your entitlement ends in Dec, and current date is the beginning of June, and your adding 2 more users, the equation is then

If you make the additions in June, you'll be billed for June - Dec x 2 users, therefore

`{price}` x `2` x `{12-6 + 1 (the current month)}` =  `{price}` x `2` x `{7}` 

At then end of Dec, when renewal is due, you will be automatically billed for 3 users going forward (1 Baseplan + 2 users) on an annual basis.

### Scenario: Cancellation
You have registered with SharpSync on the base plan as shown above and added 2 additional users.
In June you require the removal of the additional 2 users.
You request the cancellation of the users using Billing > modify.

Result: The subscription for the 2 additional users are immediately cancelled. Your users _still_ has access to the application since the users were paid for on an annual basis. The users can still make use of the software. In December the plan will renew with only 1 seat (part of the default base plan), at which point the maximum number of simultaneous users will be reduced to 1 again.

### Scenario: Refunds
Should you find yourself in position where you made an incorrect payment, login on your customer profile and request a refund.

Please note that refunds are not processed after 24hrs have elapsed. Anything after that is non-refundable. We believe that this is a significant investment in a company and should not be taken lightly. There is ample time to test the software and play around with it, therefore refunds are purely in case there are problems with accidental payments and should not be considered a regular exercise.

