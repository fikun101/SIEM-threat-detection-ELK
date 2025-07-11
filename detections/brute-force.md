# Detection: SSH Brute Force Attempts

## Description
Detects repeated failed SSH login attempts in a short time window, commonly indicating a brute force attack.

## Log Source
`/var/log/auth.log`

## Log Event Triggered By
Running brute force with Hydra:
```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://localhost
```

## How to Detect in Kibana
1. Open Kibana at `http://localhost:5601`
2. Go to **Discover** and select index pattern: `authlog-*`
3. Filter the logs:
```
message: "Failed password" AND process: "sshd"
```
4. Add a bar chart to dashboard showing failed attempts by IP or timestamp

## Result
- Multiple `Failed password` log entries from one IP in a short time window
- Clear pattern of brute-force visible in both raw logs and dashboard visualizations

## Notes
This is a common tactic used by attackers to guess passwords over SSH. Regular monitoring of failed login spikes is critical in real environments.
