# Karaoke Admin Pad Repo

This repository controls **karaoke signup-pad host access only** in LiveSocialVR's **LSVR Karaoke** world. It does not control the music player, monitor pads, camera, or other worlds.

## Add or remove a karaoke host

1. Open [karaoke-admins.json](karaoke-admins.json).
2. Click the pencil (**Edit this file**).
3. Add the player's exact **Meta profile display name** inside the `displayNames` list, or delete their entry to remove access.
4. Keep quotes around every name and commas between entries. Do not put a comma after the last name. Keep `schemaVersion` set to `1`.
5. Click **Commit changes** and commit directly to **main**.

Example with an additional host:

```json
{
  "schemaVersion": 1,
  "displayNames": [
    "CR00K",
    "metasocialite",
    "New Host Name"
  ]
}
```

Names match exactly, ignoring capitalization and surrounding spaces. `CR00K` uses two zeros. Use their Meta display name, not their GitHub username. This version uses display-name matching, so changing a Meta display name requires updating this list.

To remove all hosts, use `"displayNames": []`. There are no permanent built-in admin exceptions; removing CR00K or metasocialite also removes their karaoke host access.

## When changes take effect

The client coordinating each karaoke room checks this file when it takes over and every **60 seconds** while connected. It shares the accepted list with everyone in that room. The same list governs both the host buttons and validation of host commands.

Allow the next refresh and GitHub propagation for additions/removals. Players do not normally need to restart. An APK containing this remote-list feature must be installed once; subsequent edits to this file do not require another APK.

If GitHub is temporarily unavailable or JSON is invalid, the last accepted list remains usable for at most **10 minutes** after its last successful fetch. After that, host access is disabled until a valid list is received. The automatic queue and ordinary player controls continue. A fresh session has no host access until a valid list loads.

This repository is public so headsets can read the list without a GitHub login. Only repository writers can change it. Do not add passwords, access tokens, or other private information to this file.
