# Q060 — Your answer

## (a) The trace

TODO(Q060): give the label and `handled` after each of the nine steps.

0. start             handled=0  label: (no quote yet)
1. type 4.2          handled=0  label: (no quote yet)
2. click Quote       handled=1  label: WF 4.5 kg: Rp31,500, ready in 48 h
3. tick Express      handled=2  label: WF 4.5 kg express: Rp47,250, ready in 12 h
4. choose WDI        handled=3  label: WDI 4.5 kg express: Rp67,500, ready in 18 h
5. type abc          handled=3  label: WDI 4.5 kg express: Rp67,500, ready in 18 h
6. press Enter       handled=4  label: Invalid weight: enter a number.
7. untick Express    handled=5  label: Invalid weight: enter a number.
8. choose IR         handled=6  label: Invalid weight: enter a number.
9. type 0.4, click   handled=7  label: IR 2.0 kg: Rp10,000, ready in 24 h

## (b) The stale label

TODO(Q060): why does step 5 leave a label that contradicts the field, and what event would
you listen to in order to fix it?
Step 5 leaves the old label because typing in a text field does not trigger an ActionListener. The listener only runs when Enter is pressed. To fix this, a DocumentListener should be added to the text field so that the quote is updated whenever its content changes.
