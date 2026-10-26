# Project 1 Troubleshooting

## 1. MAC address tables did not populate across three switches

- **Symptom:** after pings between PCs, the switches' MAC address tables did not list the connected PCs.
- **Tried:** reconnecting every PC-to-switch cable, clearing the tables with `clear mac address-table`, and restarting the simulator.
- **Fix:** closing and reopening Packet Tracer reset its internal processes and the tables populated normally.
- **Lesson:** in a simulator, rule out the tool itself once the configuration has been checked.

## 2. Straight-through cables failed the cable tester

- **Symptom:** the tester reported failures, and the connector's teeth were not gripping the cable jacket.
- **Tried:** stripping less jacket, trimming all eight wires to equal length, and stripping more jacket.
- **Fix:** strip less jacket **and** trim the wires evenly. Even wires all reach the contacts, and the shorter strip lets the connector clamp the jacket.
- **Lesson:** the two common failures (short wires and a loose jacket) pull in opposite directions, so trim first, then strip only as much as needed.

## 3. Crossover cable failed the cable tester

- **Symptom:** the tester showed failed pairs.
- **Checks:** pushed wires further into the connector, checked for damaged wires, then compared the order against the TIA-568A/B diagrams.
- **Cause:** the brown wire was in the wrong position.
- **Fix:** re-terminated with the correct order and the cable passed.
- **Lesson:** check the color order against the standard before re-crimping.
