# Project 4 Troubleshooting

## 1. A Cisco 3750 port would not accept switchport commands

- **Symptom:** on SW1, `switchport mode trunk` and `switchport mode access` were rejected on one GigabitEthernet port.
- **Tried:** resetting the switch and re-entering the interface configuration.
- **Cause:** the port was operating as a Layer 3 (routed) port, which does not accept Layer 2 switchport commands.
- **Fix:** enter `switchport` on the interface to return it to Layer 2, then apply the trunk or access settings.
- **Lesson:** multilayer switches can run a port at Layer 2 or Layer 3. Check `show interfaces <port> switchport` when switchport commands fail.

## 2. SSH from a router to a switch failed

- **Symptom:** SSH sessions from either router to the switches failed during the handshake.
- **Cause:** the router and switch could not agree on an encryption cipher.
- **Fix:** specify the cipher and port explicitly from the router, for example:

  ```
  ssh -l <user> -c aes256-cbc -p 22 <switch-ip>
  ```

- **Lesson:** devices of different ages support different SSH algorithms. When a handshake fails, compare the supported ciphers on both ends. In production, update firmware rather than fall back to older ciphers.

## 3. A Cisco 3750 switch would not reset or enter ROMmon

- **Symptom:** SW1 ignored every attempt to enter ROMmon or reset to defaults.
- **Tried:** power cycling into ROMmon and the front-panel MODE button reset.
- **Fix:** replaced the switch. The replacement entered ROMmon normally and was reset.
- **Lesson:** after exhausting the documented recovery methods, suspect hardware and swap it rather than keep losing time.
