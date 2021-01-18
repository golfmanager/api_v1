
Advanced Settings
============================

**bookings.rememberType**  
Value: true/false  
Prevent remember the reservation type for a client in the timetable

**bookings.preventPastDates**  
Value: true/false  
Prevent making reservations on past dates

**bookings.allowAnyName**  
Value: true/false  
Allow anonymous reservations in admin

**bookings.salesPendingPaymentAlert**  
Value: true/false  
Show an alert when there are past sales pending payment

-----

**ebookings.membershipMode**  
Value: true/false  
Show the bookings view in membership mode.

**ebookings.showPastHours**  
Value: true/false  
Show past hours when browsing the current day.

**ebookings.hideHomePagePrices**
Value: true/false
Plugin: consumer
Hides reservations prices in the main ebookings page

-----

**billing.preventPastChanges**  
Value: true/false  
Prevent changing past sales (past refers to useDate)

**billing.dueDateAsUseDate**  
Value: true/false              
Set saleline dueDate as createDate or useDate by default

**billing.cancelInvoiceTickets**   
Value: true/false  
If the system cancels existing tickets when generating an invoice.

**billing.autoSetOnCredit**  
Value: true/false  
Automatically add a line as on credit when a client has onCredit enabled.

**billing.requirePermissionToUpdatePastSales**  
Value: true/false  
Require changePastUsedateSales permission to update sales with useDate in the past.

**billing.requirePermissionToUpdatePastCreatedSales**  
Value: true/false  
Require changePastCreateDateSales permission to update sales with createDate in the past.

**billing.paymentAfterUseDate**  
Value: true/false  
Don't generate a payment when any line has useDate in the future. They payment will be saved as a payment on account.
When the date comes and you try to pay again (with the partial or full payment on account) the payment will be generated.

**billing.skipTicketOnPayment**  
Value: true/false  
Skip creating a ticket when paying for salelines set in the future.

**billing.generateInvoiceAndTicket**  
Value: Series Id
Automatically generate an invoice and a ticket/receipt when making a payment.

**billing.idDefaultClient**  
Value: Client Id  
Use this client by default on sales where the client is null. Required by billing.generateInvoiceAndTicket.

**billing.idOnlineCashRegister**  
Value: Cash Register Id  
Use this cash register for online sales. Required by billing.generateInvoiceAndTicket.

**billing.enableTipping**
Value: true/false
Allow adding tips to every sale in the POS

**billing.multiCurrencyPOS**
Value: true/false
Show multi-currency options in the POS

-----

**eshop.thankyouPage**  
Value: a url  
Plugin: consumer  
The url to redirect to after a successful purchase.  

**selectRowsByPage**  
Value: true/false   
Plugin: slib   
Public: true   
Select rows all rows int the page versus all rows in the search.

**ebookings.membershipClientTag**  
Value: string  
Show a list of clients (with that tag) to pick one or a just a text box to enter free form text.

-----

**pos.showCashierLastSession**  
Value: true/false
Show data from the last cash register session only in /admin/pos/list

**pos.showCashierLastSession**  
Value: true/false
Show data from the last cash register session only in /admin/pos/list

-----

**school.filterClassTypeByTeacher**
Value: true/false
Filter class types by teacher when creating a new class

-----

**stock.autoUpdateAverageCost**
Value: true/false
Recalculates the average cost of a product after every transaction 