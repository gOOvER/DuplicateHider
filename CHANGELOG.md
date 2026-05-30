## v1.0.0 (2026-05-30)

### Rebrand

- Renamed to DuplicateHiderNG
- Crowdin project migrated to https://crowdin.com/project/playnite-duplicate-hider-ng
- Project migrated to SDK-style `.csproj`; NuGet packages updated to current versions

### Fix

- **#127**: Plugin no longer fails to load when `settings.json` is corrupted; falls back to defaults and shows a Playnite notification
- **#93**: Platform icon now has priority over library/source plugin icon in the icon priority chain (relevant when `game.Source != null`)
- `RemoveSelectedFromIgnoreEntry`: was reading from `PlayniteApi.MainView.SelectedGames` instead of the action context — selected games were ignored (B1)
- `ResolveGroupConflicts`: `anyMoved` flag was never set when games were only moved between groups, causing the method to incorrectly report no changes (B2)
- `IconCache.GetOrGenerate`: replaced non-atomic `TryGetValue`/assign with `ConcurrentDictionary.GetOrAdd` to prevent a race condition under concurrent access (B3)
- `Settings_OnSettingsChangedAsync`: added `try/finally` to guarantee `ItemUpdated` is always re-subscribed even if an exception occurs during the settings-changed handler (B4)
- Regex in replacement filter rules: added `MatchTimeout` to prevent ReDoS on user-supplied patterns (S1)
- Regex in replacement filter rules: `ArgumentException` on invalid patterns is now caught gracefully instead of crashing (S2)
- `ReplaceFilter.ApplySingle`: `RegexMatchTimeoutException` is now caught and treated as a non-match instead of propagating (S1 follow-up)
- `catch (Exception) {}` in `IconCache` silently swallowed errors; now logs a warning with the exception details (BP1)
- `iconWatcher` was not disposed on plugin shutdown; `Dispose()` is now called in `OnApplicationStopped` (BP2)
- Three `if (game is Game)` null-checks replaced with `if (game != null)` — the `is`-pattern always returned `true` for non-null `Game` instances (BP3)
- Removed dead `CompareOld` method that was never called (BP4)

### Feat

- **#133**: New setting "Include All Platforms" — bypasses the platform allowlist entirely, future platforms are included automatically
- **#121**: New setting "Never Hide Installed" — installed copies are never hidden regardless of source priority
- **#145**: New `{Library}` display string placeholder — resolves to the human-readable name of the importing library plugin (e.g. `Steam`, `GOG`); falls back to `{Source}` for manual entries
- **#141**: New setting "Sort Custom Groups by Name" — custom groups in the game context menu are sorted alphabetically when enabled

### Perf

- `GetResourceNames()`: result is now cached in `_resourceNamesCache`; previously re-enumerated assembly resources on every icon lookup (O3)
- `typeof(Game).GetProperties()`: result cached in a `static readonly` field; previously called via reflection on every display string expansion (O4)
- `foundThemeIcons.Count() > 0` replaced with `.Any()` to avoid full enumeration (O1)
- Four `Where().Count()` calls replaced with `Count(predicate)` to avoid intermediate allocations (O2)

## v3.9.0 (2021-12-29)

### Fix

- fix crash if games name are null

## v3.8.1 (2021-12-18)

### Fix

- init progress to 0

### Feat

- use global progress dialog for copying

## v3.8.0 (2021-11-07)

### Feat

- added priority overwrite tags

## v3.7.1 (2021-10-24)

### Fix

- hiding games using the menu function does not update ui integration

## v3.7.0 (2021-10-24)

### Feat

- custom groups overwrite black/white lists

### Fix

- Undefined Platform not matched on empty platform list

## v3.6.0 (2021-10-20)

### Feat

- updated localization and links

## v3.5.2 (2021-10-18)

### Fix

- include games that have at least one enabled platform

## v3.5.1 (2021-10-18)

### Fix

- crashing if game's TagId list is null

## v3.5.0 (2021-10-18)

### Feat

- italian translation by MaxRally
- italian translation by MaxRally

### Fix

- automatic update not working in some cases

## v3.4.2 (2021-10-18)

### Fix

- ui integration not reflecting changes correctly
- triggering game updates too often in some cases fix: ui integration not reflecting changes correctly

## v3.4.1 (2021-10-06)

### Fix

- check if TagId List exists before adding or removing tags

## v3.4.0 (2021-10-06)

### Feat

- add tag to games hidden by duplicate hider

## v3.3.0 (2021-10-05)

### Feat

- updated to QuickSearchSDK 2.0.0

## v3.2.3 (2021-09-23)

### Fix

- default SourceSelector caused crashes in some cases
- updated to new QuickSearchSDK

## v3.2.2 (2021-09-21)

### Fix

- customs groups not being saved correctly in some cases

## v3.2.1 (2021-09-17)

### Fix

- crash if group item is dragged to the last spot

## v3.2.0 (2021-09-17)

### Refactor

- removed unused variables
- changed loc strings
- changed loc string

### Fix

- items disappearing after being dropped

### Feat

- added custom groups

## v3.1.6 (2021-09-15)

### Fix

- platform icons only were cached once per source

## v3.1.5 (2021-09-15)

### Fix

- platform locaization string spelled incorrrctly

## v3.1.4 (2021-09-08)

### Fix

- check for resource existence before setting it as a reference
- no tooltip for default SourceSelector Style in Fullscreen mode
- still change icon opacity if no style is applied

## v3.1.3 (2021-09-07)

### Fix

- catch error when library icon path is null
- icon opacity is not changed based on installation status using code behind, it is only handled by each theme

### Perf

- ListData objects are properly being reused to save time wasted on their innitialization
- store dictionary that keeps a list of copies for each game

### Refactor

- fixed release date
- added new package
- cz init

## v3.1.2 (2021-09-07)

### Fix

- theme icons can be found using either lower case or capitalized
- use pluginId to retrieve icons of builtin sources

### Refactor

- added extension function to capitalize strings

## v3.1.1 (2021-09-05)

## v3.1.0 (2021-09-04)

## v3.0.0 (2021-09-03)

## v2.5.4 (2021-06-13)

## v2.5.3 (2021-05-29)

## v2.5.2 (2021-05-26)

## v2.5.0 (2021-04-28)

## v2.5.1 (2021-04-26)

## v2.3.2 (2021-01-08)

## v2.3.1 (2021-01-06)
