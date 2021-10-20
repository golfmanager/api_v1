# Plugin Pos 

### Descripción 
Nombre meta: TPV

Terminal punto de venta

Depende del plugin billing 

### Instalación
Desde appCenter - TPV

**buttons** : configuración de botonoes del TPV

**cashregister**: 

Permite a otros plugins hacer cambios 
```
hooks.exec("POS.CashRegisterList", null, { td: td, payment: p })
```
Para llamar al la caja desde otro plugin: 
```
       loadCashRegisterID()
       loadCashRegisterFull(callback: (cr: CashRegister) => void) {}
       loadCashRegister()
       selectCashRegister(callback?: InitCallback)

```
- **escposTicket**

- **htmlTicket**

- **printer**: vistas de addPrinter modal y grid. 

- **textTikect**: configuración del texto del ticket

- **ticketTable**: configuración de la tabla de tickets.

### Opciones avanzadas 

- **pos.showCashierLastSession**  
Value: true/false
Muestra datos de la última sesión de la caja registradora solo en /admin/pos/list

- **pos.printSeparateTaxes**  
Value: true/false
Imprime líneas de tickets sin impuestos y los impuestos al final. 

- **pos.sendTicketByDefault**
Value: true/false
Preseleccionar enviar tickets al correo electrónico del cliente si está disponible


- **pos.showDiscountReasons**
Value: true/false
Muestra las razones del descuento al aplicar un descuento. 

-----
## POS custom commands

Custom commands
-----------

| Command               | Args       | Description                                                              |
| --------------------- | ---------- | ------------------------------------------------------------------------ |
| addProduct            | idProduct  | add a new product to the sale                                            |
| addDiscount           | idDiscount | add a new discount to the sale                                           |
| addComments           |            | add a comment to the current line                                        |
| addPublicComments     |            | add a public comment to the current line. It will be shown in the ticket |
| addDescription        |            | append a text to the description of all or selected lines                |
| splitLine             |            | split a line into multiple lines                                         |
| setClient             |            | assign the client to all or selected lines                               |
| addDescription        |            | add a description to all or selected lines                               |
| addPublicComments     |            | add comments that will be printed on the ticket to all or selected lines |
| setCoupon             |            | set a cupon to the current line                                          |
| splitLine             |            | split a line in multiple amounts                                         |
| generateInvoice       |            | create an invoice from the current sale                                  |
| showLastSales         |            |                                                                          |
| showParkedSales       |            |                                                                          |
| cancelAccountPayments |            |                                                                          |
| printSale             |            |                                                                          |
| parkSale              |            |                                                                          |
| newSale               |            |                                                                          |
| printSale             |            |                                                                          |
| openDrawer            |            | Open the cash register drawer                                            |
| executeAction         |            | Open a url (an action. For a redirect prefix the url with 'URL:')        |





External functions 
----------- 
This functions depend on other plugins


| Command | Args                                          | Description                                         |
| ------- | --------------------------------------------- | --------------------------------------------------- |
| exec    | ["billing.newVoucher", idVoucherType]         |                                                     |
| exec    | ["billing.addTag"*, ["Left handed"]*]         | Add a tag to the selected lines.                    |
| exec    | ["recurring.newMembership", idMembershipType] | Create a new membership                             |
| exec    | ["timetable.newReservation", idReservation]   | Create a new reservation linked to the selected one |
| exec    | ["fandb.sendToPrinter"]                       | Food and Beverage: send to kitchen printer          |
| exec    | ["fandb.moveLines"]                           | Food and Beverage: move lines to another table      |



----
imprimir un texto randon en el tiketprinter: 
```
 let text = `AJUNTAMENT DE BARCELONA 
        BARCELONA 
 
 Cod.FUC : 999999999
 N/S     : 00080029524
 Moneda  : EUR (978)
 
 MasterCard
 A0000000041010
 ******      00
 
 VENTA (OCP)
 
   SIMULADOR ECOPAYNET 
 Fecha: 12/03/19 10:50:56
 Aut: 013295   Oper: 0375
        AUTORIZADA
 Cod. Resp: 00
 
        12,00  EUR
 
    OPERACION CON PIN 
    FIRMA NO NECESARIA
 
    * COPIA CLIENTE * 
 
    `
    
    pos.loadCashRegisterFull((cr: any) => pos.printString(text, cr))
```
