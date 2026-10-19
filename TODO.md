# TODO

## Chests / coins
- [ ] Tie chest creation to actual tracking. `claim_tracking_chests` currently
  creates the current-window chest (`TRACKING_MORNING/EVENING_CHEST_V1`)
  unconditionally, so the daily cron mints up to 2 chests/day (20 DIAMOND) even
  with no food logged. Before creating a chest, check that the day/window actually
  has consumed items (GET `/user/consumed-items?date=…`), and only create+claim
  when the user really tracked. (Not urgent — server caps it at one chest per
  window per day, so it is not farmable.)
- [ ] Wire the other collectables found in the APK dex
  (`yazio/claimables/api/model/Claimable$CollectableType`): `daily_app_start`
  chest, `saturday_flavor` / `comeback` chests, and the `streak_freeze` /
  `streak_shield` collectables.

## Streak
- [ ] `freeze_count` is copied from the previous day when registering a streak
  day; the app earns freezes on milestones. Derive the real value if it ever
  matters for display.

## Notes
- Offline-first: server writes (food, streak, coins) only show in the Yazio app
  after a full resync (logout/login); the app renders from its local store.
