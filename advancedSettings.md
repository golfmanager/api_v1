# System

## Descripción
Nombre meta: Sistema

Funcionalidades básicas del sistema

## Instalación
Instalado por defecto con la inicialización de la aplicación.
## Entidades
* Country

* Región

* Templates

* TemplateTypes

* EmailAcount:

    Puertos habituales: 587, 465 y 25

* SentEmail

* AdvancedSetting

* Settings

* VirtualSettings:
    Formatos de texto, ejemplo:

```
    S.buildFlash("info", `Format examples:
                        DecimalSeparator: .
                        ThousandSeparator: ,
                        Currency: USD
                        CurrencySymbol: $
                        CurrencyPattern: $0:00
                        FloatPattern: 0:00
                        ShortDatePattern: MM-dd-yyyy
                        LongDatePattern: ddd MMM dd yyyy
                        DateTimePattern: MM-dd-yyyy HH:mm
                        LongDateTimePattern: ddd MMM dd yyyy HH:mm
                        FirstDayOfWeek: Sunday`)
```

* Plugin

* CustomPage

* Apps: system a su vez maneja la sección de App Center para instalar o desinstalar los plugins.

## Opciones avanzadas

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

**bookings.onlyPrintIfCheckin**
Value: true/false
Only allow reservations to be printed if they've been set as checked in

**bookings.checkinCountryReminder**
Value: true/false
Display a message if the reservation client doesn't have a country when doing a check in

**bookings.crossoversInTemplates**
Value: true/false
Include crossovers in templates

**bookings.dontAutoConfirm**
Value: true/false
Don't auto confirm reservations with price zero.

-----

**contacts.insertIdAsCenterCard**
Value: true/false
When creating a client, set the Center Card with the same value as the ID

-----

**ebookings.membershipMode**
Value: true/false
Plugin: consumer
Show the bookings view in membership mode.

**ebookings.membershipModeGroup**
Value: Client group ID
Plugin: consumer
Only clients from this group will have their names displayed in /consumer

**ebookings.showPastHours**
Value: true/false
Show past hours when browsing the current day.

**ebookings.hideHomePagePrices**
Value: true/false
Plugin: consumer
Hides reservations prices in the main ebookings page

**ebookings.showPriceName**
Value: true/false
Show price name in consumer/ebookings

**ebookings.showFullPrice**
Value: true/false
When a reservation type has the same min/max restriction, show the price of the entire package.

**ebookings.membershipClientTag**
Value: string
Show a list of clients (with that tag) to pick one or a just a text box to enter free form text.

**ebookings.requireReservation**
Value: true/false
Require a reservation. If the user tries to book an extra only, an error message will be shown.

**ebookings.includeOnlineCashRegister**
Value: true/false
Include the billing.idOnlineCashRegister in online salelines

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

**billing.idCurrencyPaymentMethod**
Value: Payment Method Id
A payment method with a cash gateway, enabled, not deleted, not secondary currency and available in the POS.

**billing.payPastUsedateSales**
Value: true/false
Allows you to pay sales from the past

**billing.alwaysGenerateTicket**
Value: true/false
Always generate ticket (including total paid zero & all virtual payments)

**billing.idDownPaymentProduct**
Value: Product Id
Generate a sale line instead of a payment on account (incompatible with billing.skipTicketOnPayment)

**billing.createZeroPayment**
Value: true/false
Creates a payment with amount zero when the lines being paid add up to zero.

**billing.requireTimeoutOnPayByEmail**
Value: true/false
Makes expiration date a required field when sending payments by email

**billing.addVoucherPaymentsInInvoice**
Value: true/false
Voucher payments are excluded when printing an invoice. Set this option to true to include them. 

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

-----

**pos.showCashierLastSession**
Value: true/false
Show data from the last cash register session only in /admin/pos/list

**pos.showCashierLastSession**
Value: true/false
Show data from the last cash register session only in /admin/pos/list

**pos.sendTicketByDefault**
Value: true/false
Pre-select send tickets to the client's email if available

**pos.showDiscountReasons**
Value: true/false
Show discount reasons when applying a discount

**pos.customPrinterUrl**
Value: string
The full URL including protocol and port where the printing jobs will be sent to

-----

**school.filterClassTypeByTeacher**
Value: true/false
Filter class types by teacher when creating a new class

**school.showVouchersInPopup**
Value: true/false
Show the client's vouchers in the class detail popup

-----

**stock.autoUpdateAverageCost**
Value: true/false
Recalculates the average cost of a product after every transaction

-----

**barcodelabels.hidePriceInLabels**
Value: true/false
Hide prices in barcode labels

**barcodelabels.convertPriceInLabels**
Value: true/false
Convert prices in barcode labels to secondary currency

-----

**fandb.requireDinerCount**
Value: true/false
Require diner count when creating a new sale from the tables map

**fandb.masterPrinter**
Value: Printer ID
Send every saleline to this printer
