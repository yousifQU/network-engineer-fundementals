# Project 5 Troubleshooting

## 1. OSPF mismatch errors on R1

- **Symptom:** after OSPF was configured on R1, mismatch errors appeared and R1 showed no neighbors and an incomplete database.
- **Tried:** power cycling the router, re-entering the OSPF configuration, and applying the OSPF area directly to the uplink interface.
- **Fix:** apply the area on the uplink interface (`ip ospf 1 area 0`). The errors cleared and adjacencies formed.
- **Lesson:** check `show ip ospf interface` and `show ip ospf neighbor`. Both sides of a link must agree on area, subnet, and timers.

## 2. Traffic from the VyOS access point never reached R1

- **Symptom:** wireless clients, and the VyOS router itself, could not reach R1.
- **Checks:** restarted VyOS, then traced the path hop by hop through SW1.
- **Cause:** VLAN 40 was not in the allowed VLAN list on the trunk between SW1 and R1, so the switch dropped all VLAN 40 frames.
- **Fix:** add VLAN 40 to the trunk (`switchport trunk allowed vlan add 40`).
- **Lesson:** `show interfaces trunk` lists which VLANs each trunk actually forwards. Use `allowed vlan add` so existing VLANs are not removed.

## 3. VyOS kept its previous configuration after re-flashing

- **Symptom:** after a fresh install, settings from earlier use of the device were still present.
- **Fix:** in configuration mode, load the factory default file, then commit and save:

  ```
  configure
  load /opt/vyatta/etc/config.boot.default
  commit
  save
  ```

- **Lesson:** start every build from a known-clean configuration.
