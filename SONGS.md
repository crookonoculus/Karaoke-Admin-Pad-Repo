# Karaoke song catalog

The LSVR Karaoke Up Next Pad reads this repository's song list separately from `karaoke-admins.json`. Changing songs does not change admin access.

The initial catalog contains 34,266 eligible public video listings imported from Sing King (6,134), Party Tyme (23,142), and EasyKaraoke (4,990). These are video links and metadata, not downloaded videos. Promotional entries, compilations and videos outside 30 seconds to 15 minutes were excluded. Availability and playback can change; a listing is not a guarantee that every headset can play it.

## Add a song without another APK

Edit [karaoke-song-updates.json](https://github.com/crookonoculus/Karaoke-Admin-Pad-Repo/edit/main/karaoke-song-updates.json), add an entry inside `add`, and commit to `main`:

```json
{
  "schemaVersion": 1,
  "add": [
    {
      "url": "https://www.youtube.com/watch?v=VIDEO_ID_HERE",
      "title": "Song title - Artist (Karaoke)",
      "channel": "Channel name"
    }
  ],
  "removeVideoIds": []
}
```

Replace the example URL with a real YouTube watch link. Separate entries with commas. Titles must be nonempty and at most 200 characters. The pad checks the actual YouTube title when a player selects a video. No GitHub token goes into the APK.

To hide a song, add its 11-character video ID (the part after `v=`) to `removeVideoIds`. Remove that ID to restore it. Removing a custom entry from `add` removes that custom addition after the next refresh. Removing a song from the catalog affects future choices; an already-confirmed singer keeps their selected song.

The private picker checks for updates when opened, at most once every five minutes. GitHub caching can add delay. The full `karaoke-songs.json` is a large imported file; use the small updates file for routine edits in GitHub's browser editor. New channel uploads are not automatically imported by this initial setup.

## Signup and playback

Choose Song & Join opens a local song browser. Choose from the catalog or Search Other on YouTube, then Confirm Song & Join. Searching never navigates the live Global Player. Only confirmed video selections enter the shared FIFO queue.

The selected singer receives a personal prompt to head to the stage. Start My Song begins loading their video. The performance clock starts when the room authority's player has loaded the matching video, and allows the track's duration plus 15 seconds. Tracks longer than 15 minutes and live streams are not accepted for an automated performance. Ordinary music browsing outside performances is unaffected.

After two minutes without starting, the singer gets a Still Coming check. They have one minute to start, pass, or request one two-minute extension. No response skips the turn. Queue pause freezes this waiting period. The song never starts because of a countdown.

Use the existing Up Next Pad prefab together with one active Global Player Desktop in the same LSVR Karaoke scene and Normcore room. The pad binds automatically. No new stage button is required. The original YouTube player is not part of this integration.
