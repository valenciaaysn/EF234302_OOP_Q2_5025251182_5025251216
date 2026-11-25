# Q075 — Your answer

## (a) The trace

TODO(Q075): for each of the ten events, the rows shown, or "no update".

Step 0 – Attach View-Model
A2 Budi WDI READY 11:00
A4 Dewi WF READY 12:00
A5 Rahmat WDI WASHING 13:00
A1 Sari WF WASHING 14:00
A6 Citra WF DRYING 15:00
A3 Ayu IR RECEIVED 16:00

Step 1 – Filter "ra"
A5 Rahmat WDI WASHING 13:00
A6 Citra WF DRYING 15:00

Step 2 – Sort by customer
A6 Citra WF DRYING 15:00
A5 Rahmat WDI WASHING 13:00

Step 3 – Add A7 Budi
No update

Step 4 – Advance A5
A6 Citra WF DRYING 15:00
A5 Rahmat WDI DRYING 13:00

Step 5 – Filter "RA"
No update

Step 6 – Only DRYING
No update

Step 7 – Advance A6
A5 Rahmat WDI DRYING 13:00

Step 8 – Filter cleared
No update

Step 9 – Only READY
A2 Budi WDI READY 11:00
A6 Citra WF READY 15:00
A4 Dewi WF READY 12:00

## (c) Why compare

TODO(Q075): why compare the new rows with the old ones, and why is the view-model easy to
test?
The view-model compares the new rows with the previous rows to avoid unnecessary notifications when an event does not change the displayed data. This makes the application more efficient because the view is only updated when the rows actually change.
The view-model is easy to test because its filtering and sorting logic is separated from the GUI. It can be tested using sample data and a simple callback without creating a window.

## (d) Chapter 9 ideas

TODO(Q075): which collection and generics ideas of Chapter 9 does the design use?
The design uses Java collections such as ArrayList and List to store orders and displayed rows. It also uses generics, including List<Order>, List<String>, Comparator<Order>, and Consumer<List<String>>, to ensure type safety.
Additionally, comparator chaining is used to sort orders by ready time or customer name, with order ID as the tie-breaker. List.copyOf() provides an unmodifiable copy of the order list.