### Hotel California
## ER Diagram
## Relational Design
## Interfaces
```
Reservation:
The reservation interface prompts the user for their name and hotel details that are specific to the
reservation the user would like to make.
```
```
Check In:
The check in interface propts a user for their resvation ID. This ID corresponds to a reservation
with the correct hotel ID and room type and assigns the user to an available room with the type the
user has specified. The hotel desk agent then marks the room as dirty.
```
```
Check Out:
The check out interface takes the reservation ID and the room number and marks the room as unoccupied.
The room is marked as dirty for housekeeping and the guest pays for their reservation
```
```
Housekeeping:
The housekeeping initerface takes a room number and a hotel ID. The houskeeping interface then goes to
a room with that is dirty and marks it as clean after housekeeping has visited.
```
## Limitations
```
FGP Table:
Upon joining the frequent guest program (FGP), a user should be automatically added to the customer
table. In order to do this, I attempted to write a trigger with the following code:

create or replace TRIGGER IN FGP TR1
AFTER INSERT OR UPDATE OF FGP NUM,NAME,PHONE ON FGP
DECLARE
alr exists number(2);
BEGIN
select count (*)
into alr exists
from customer
where customer.name = fgp.name and customer.phone = fgp.phone;

if alr exists=0 then
    insert into customer
    (name, address, phone)
    values
    (new.fgp.name, new.fgp.address, new.fgp.phone);
end if;
END;

However, PL/SQL was ignoring the statements and I did not have time to debug the trigger. Thus,
it has been excluded and is being noted as a limitation of the database I have created.
```
```
Reservation Interface:
The reservation interface should also have a trigger that adds a customer to the customer database upon
making a reservation. I did not have time to implement this feature.
```