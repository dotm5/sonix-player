# Smart Mix — simulator evidence (PR 2)

Run on the host build (`make host` → `sonix_player_host`) inside WSL, drawn in an
SDL window under WSLg at 480x720 — the R3 Pro II panel, taken from
`sonix-packer/assets/R3PII/`.

Card: a copy of the real library index (2264 tracks) and the real similarity graph,
at `/mnt/sd_0/.local/{library,genius}.db`. The audio files are not on this machine,
so nothing plays; the index and the graph are real, and that is what the interface
walks and what the mix is built from.

Driven with `xdotool` synthetic clicks on the SDL window, captured with
`xwd | convert`. The player blanks its screen after 30 s idle; in the host build a
mouse click does not wake it, so `p` (the power key) was pressed between steps.

## The log, for the run these were taken from

```
library: /mnt/sd_0/.local/library.db open, 2264 tracks indexed
library: Smart Mix phase at SCHED_OTHER / nice 10 (thread_set_background_level(true))
geniusbuild: result 1, 2264 tracks, retained peak 2241700 bytes
genius: mix saved as 'Smart Mix - Bach No Senritsu Wo Yoru Ni Kiita Seidesu'
genius: mix saved as 'Smart Mix - Bach No Senritsu Wo Yoru Ni Kiita Seidesu (2)'
```

## Browsing the playlists — the seed is chosen on the library's own lists

| file | what it shows |
|---|---|
| `E1-playlists-empty.png` | The Playlist page with nothing in it: the two creation rows, and the empty note **below both of them**. The note used to be pinned at a fixed height and sat on top of the second row. |
| `E2-seed-picker.png` | "Create Smart Mix" opens the seed picker — the album list, chevrons to drill down, and **no corner buttons**: none of "play all", sort or the album/records swap has anything to do with the one track being looked for. |
| `E3-album-tracks.png` | Drilled into an album. Tapping a track picks it as the seed. The per-track ellipsis is **gone** here — its menu is about playing and filing a track, not choosing one. A long press does not start selection mode either. |
| `E4-saved-toast.png` | The mix is written and the player goes **straight to the new playlist's own track list**, named after the seed. |
| `E5-new-playlist.png` | That list: the seed first, then the sequence the graph walk produced. |
| `E6-playlists.png` | Back on the Playlist page: the generated playlist is an ordinary row with its track count and its own ellipsis — Rename, Delete, Backup, the same as any playlist made by hand. |

## Adding a track to a playlist — the seed is the track in hand

| file | what it shows |
|---|---|
| `E7-all-tracks.png` | A track list, entered the ordinary way. |
| `E8-selection.png` | One track selected in the library's own selection mode and sent to "Add to playlist": the page offers both "New playlist" and "Create Smart Mix", the seed being the track that was selected. |
| `E9-pick-toast.png` | Generated from that track. |
| `E10-pick-playlist.png` | The new playlist's track list, seed first. |

## Not covered here

No audio files, so nothing plays: playback, next/previous over an ordered mix, and
card removal or USB export were not exercised. Only the R3 Pro II profile was run;
the R1 was not.
