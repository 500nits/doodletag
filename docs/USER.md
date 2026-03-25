# DoodleTag User Guide

This guide documents the active, user-facing feature set as of the latest changelog updates.

## 1. Canvas Fundamentals
- Infinite-session style drawing on a fixed paper world with pan and zoom.
- Single-tap viewport reset returns to full paper view.
- Long-press viewport reset cycles zoom presets (`view one`, `view two`) for quick framing.
- Drawing input outside the paper is ignored.
- Undo and redo are stack-based and operate on drawing/tool actions. Macro replay itself is one undoable operation that restores the canvas state from just before playback, while air blower and gum keep their own undoable operations.

## 2. Main Controls (Tap vs Long-Press)
| Control | Tap | Long-Press |
| --- | --- | --- |
| `Peers` | Toggle glue discovery/connect/disconnect flow. Entering Glue parks the current solo canvas locally and switches to the pair canvas for that device pair. Leaving Glue restores the parked solo canvas. | Forget last glued peer preference |
| `Menu Toggle` | Open/close the radial menu. | None |
| `Undo` | Undo last local action. | Redo |
| `Clear Canvas` | Confirm and clear current doodle. | While solo: clear saved sessions/snapshots and stored glue-session restore data without wiping the current canvas. While glued: hold-to-request clear flow |
| `Export` | Open export flow and save image output. | Share the last recorded macro directly; if no macro is ready, DoodleTag shouts that out |
| `Reset View` | Reset pan/zoom to full paper. | Cycle zoom presets |
| `Rainbow` | Toggle rainbow drawing mode. | Open the rainbow color editor |
| `Color/Palette` | Open quick palette picker. | Toggle debug overlay |
| `Stroke Width` | Cycle thickness presets. | Open thickness slider dialog |
| `Gum` | Toggle eraser mode. | Open gum-size dialog |
| `Air Blower` | Toggle blower mode. | Open blower settings dialog |
| `Orthogonal` | Toggle directional snapping tool. | None |
| `Square Grid` | Toggle square grid. | Open grid settings |
| `Hex Grid` | Toggle hex grid. | Open hex-grid settings |
| `Macro` | Start/stop/share macro recording flow. Stopping a recording shouts `MACRO RECORDED`. | Reset current macro recording session and remove the currently stored pending macro slot |
| `Welcome Tour (?)` | Play bundled welcome macro in read-only mode. | Reset "tour played" onboarding flag |
| `Tool Shouts` | Cycle banner modes: `all`, `announce-only`, `off`. The button announces the newly selected mode. | Reset all tool settings to their default values |

## 2.1 Reset and Recovery Actions
- DoodleTag does not currently have one single "factory reset" button that makes the app behave exactly like a brand-new install.
- Instead, reset actions are split by domain so you can clear only the part you mean to reset.

### 2.1.1 Reset All Tool Settings
- Long-press the `Tool Shouts` megaphone button.
- This opens `Reset all tool settings?`.
- It restores default values for tool-facing state such as:
  - brush/tool thickness values
  - palette-related tool settings
  - rainbow settings
  - gum / air blower settings
  - grid / hex-grid settings
  - shout-banner mode
- It is the closest thing to "reset my tools back to defaults".
- It does not clear saved macro files, onboarding flags, or saved session/snapshot files.

### 2.1.2 Clear Saved Sessions and Snapshot Restore Data
- While not glued, long-press `Clear Canvas`.
- This opens the saved-session clearing confirmation flow.
- It deletes the persisted snapshot/session storage used for:
  - latest solo canvas restore
  - parked solo restore snapshot
  - glued pair snapshot files
  - stored glue session restore metadata/preferences
- It keeps the current live canvas intact and only removes the stored restore/session data.
- After the wipe, DoodleTag shouts `GLUE SESSIONS CLEARED`.
- Use this when you want to remove remembered canvas/session state, not just erase what is currently visible.

### 2.1.3 Reset the Stored Macro Slot
- Long-press `Macro`.
- DoodleTag asks `Reset recorded macro?` in a bottom sheet before doing anything.
- Choosing `Yes` resets the current macro recording state and removes the previously stored pending macro slot.
- Use this if you want to discard the last recorded macro before starting a new one.
- This does not reset general tool settings or snapshot/session storage.

### 2.1.4 Reset Welcome Tour Onboarding
- Long-press the `Welcome Tour (?)` button.
- This clears the "tour already played" flag.
- Use it when you want the welcome tour to be eligible again like a first-run onboarding prompt.
- This does not change drawing tools, snapshots, or macro storage.
## 3. Glue Rules
- Entering Glue parks the current solo canvas locally.
- Glue always shows the pair canvas for that specific pair.
- Leaving Glue saves the pair canvas and restores the parked solo canvas.
- If the pair has no saved shared canvas yet, Glue starts from a blank shared canvas for that pair.
- While Glue is waiting for a peer, draw input is ignored and the canvas darkens.
- The `GLUE IN PROGRESS` shout follows the current banner mode, but the dimmed in-progress canvas state remains visible even when banners are limited or off.

## 4. Tool Interactions and Exclusivity
- `Square Grid` and `Hex Grid` are mutually exclusive.
- `Gum`, `Air Blower`, and `Orthogonal` are mutually exclusive in direct tool toggles.
- Enabling `Rainbow` turns off incompatible tools where needed and keeps rainbow-specific stroke behavior active.
- Orthogonal snapping behavior depends on guides:
  - If square grid is active: snaps to grid-aligned orthogonal directions.
  - If hex grid is active: snaps along hex-edge directions.
  - If no grid is active: snaps to orthogonal directions in free space.
- While Glue is active or waiting for a peer, actions that would cause local divergence are guarded.

## 5. Drawing and Color Features
- Standard freehand drawing with thickness presets and precise thickness slider.
- Tool-specific feel is preserved: DoodleTag remembers the last thickness used for each drawing context, so switching between modes restores the width that felt right there.
- Example: a bold Rainbow stroke can stay bold while standard drawing stays ultra-thin, letting users jump between looks without re-tuning the brush every time.
- Quick palette includes:
  - `Palette` tab for fast swatch picks.
  - `Wheel` tab for continuous color selection.
  - Recent color history integration.
- Rainbow color editing is opened from the `Rainbow` tool path and uses its own dedicated editor flow.
- Closing the quick palette does not switch tools.
- Recent-color behavior is stable (reselecting colors does not unexpectedly delete history entries).
- Blue/green pair colors are used only for first-time Glue defaults; user-selected colors remain user-owned.

## 6. Rainbow Tool (Complete Option Set)
- Toggle rainbow on/off directly from the menu.
- `Normal` rainbow follows a toothpaste-style model: colors are stored in a fixed internal sequence and come out from the point where the stroke starts. Reversing the draw direction remaps those colors around the shape instead of preserving the same edge-to-color assignment.
- Rainbow color progression is distance-based, not time-based. Moving faster or slower over the same path does not change the internal color order; it only changes how quickly that ordered color stream is laid down along the path.
- Styles:
  - `Normal`
  - `Pop`
  - `Lanes`
- Segment length is adjustable with step controls and displayed in centimeters.
- Palette control:
  - Six editable rainbow palette slots.
  - `Reset` to default rainbow palette.
  - Uses the dedicated rainbow color editor.
- `Lanes` style supports lane-aware turning/join behavior and ongoing geometry refinements.
- Rainbow settings persist across app restarts.

## 7. Gum (Eraser)
- Toggle gum and erase by dragging/tapping across strokes.
- Erase size is configurable via long-press settings dialog.
- Long erases show a progress overlay.
- Canceling a progress erase restores the pre-erase snapshot immediately.
- Supports undo/redo restoration of erasure operations.

## 8. Air Blower
- Toggle blower mode for stroke displacement/removal/mixing effects.
- Long-press settings include:
  - Radius
  - Strength profile
  - Kind:
    - `Displace`
    - `Vortex Remove`
    - `Mix Colors`
- Air blower actions are recorded as undoable operations with snapshot safety, including redo through full snapshots for merged drag actions.
- Remote/glued playback applies blower actions consistently.

## 9. Macro System

### 9.1 Recording and Sharing
- Macro record button starts recording.
- Tapping `Macro` again after stopping a recording does not immediately start a new one if the last recorded macro is still sitting in the slot unshared. Instead, DoodleTag shows an `Unshared macro` dialog with choices such as:
  - `Start anyway`
  - `Share first`
  - `Play current`
- Starting a macro recording never clears the current canvas. Recording begins on top of whatever is already visible.
- Recording captures:
  - Finger-driven drawing/tool events
  - Tool snapshots
  - Timeline events
  - Viewport metadata
- Stopping a recording from the `Macro` button stores that finished macro as the current pending macro and shouts `MACRO RECORDED`.
- Once a macro has been recorded, there are two user-facing share paths:
  - Long-press `Export` to immediately share the last recorded macro.
  - Tap `Export`, then use the export dialog action that shares the last recording.
- If there is no recorded macro ready to share, long-pressing `Export` does not silently fail: DoodleTag shouts `NO MACRO RECORDED`.
- Sharing the last recorded macro clears that pending macro slot after a successful share, so the app no longer treats it as an unshared recording.
- Long-pressing `Macro` resets the current recording state and removes the stored pending macro slot if you want to discard the last recorded macro instead of sharing it.
- `Undo` and `Redo` pressed while recording still affect the live canvas locally, but they are not stored inside the macro.
- `Clear Canvas` pressed while recording behaves like a normal local clear on the live canvas and is stored as a clear-canvas macro event.
- Export/share flow produces `.dtag` macro files.

### 9.2 Macro File Format and Compatibility
- `.dtag` uses password-protected ZIP packaging (`Doodle Tag`) with compatibility handling for legacy payloads.
- Import playback supports bundled assets, local files, and deep-link driven downloads.

### 9.3 Playback Behavior
- Macro playback is globally locked to one active playback at a time.
- Playback runs through a read-only long-task UI.
- Macro playback starts on top of the current canvas and does not clear it automatically.
- If the recorded macro contains `Clear Canvas`, replay treats that event as `restore the canvas to the exact snapshot from before playback started`.
- User controls during playback:
  - `Skip` (fast-forward to end)
  - `Cancel` (restore pre-play snapshot)
- Skip/cancel reset viewport framing consistently.
- Replay completion adds one undoable macro-replay snapshot so undo restores the pre-playback canvas in a single step.

## 10. Welcome Tour
- Dedicated `?` utility button launches the bundled welcome tour macro.
- First-launch autoplay is supported (with local played-flag persistence).
- Tour can be reset by long-pressing `?`.
- Tour playback uses the same read-only macro pipeline with skip/cancel safety.

## 11. Glue (Collaborative Canvas)
- Device discovery/connection for shared drawing sessions.
- Auto-glue session restoration and reconnect behavior with peer/session memory.
- Each device pair has its own shared canvas snapshot, and the same pair restores that shared canvas on reconnect.
- Entering Glue preserves the local solo canvas in a separate restore slot instead of merging solo and shared history.
- Leaving Glue saves the pair snapshot and restores the parked solo snapshot.
- Snapshot metadata/data exchange keeps peers converged on the newest shared state and avoids stale overwrites.
- Long-pressing `Peers` forgets the last preferred peer without deleting snapshots.

## 12. Import, Deep Links, and File Handling
- OS-level `.dtag` opening support on Android and iOS.
- Android intent filters support custom and fallback MIME flows for better "Open with" behavior.
- Universal/App link intake supports macro links and remote macro download/play flow.
- Cold-start macro open is deferred until UI is ready so play dialogs render reliably.

## 13. Export and Long Tasks
- Export uses controlled progress flows to avoid partial/interrupted output.
- Long-running operations use shared long-task overlay patterns for consistent UX.
- Long-task surfaces are integrated with the bottom menu replacement when applicable to reduce canvas obstruction.

## 14. Persistence and Restore
- Persisted settings include:
  - Color, thickness, cap
  - Per-tool/per-context thickness memory so each drawing mode can return to its own preferred stroke feel
  - Recent colors
  - Grid/hex parameters
  - Rainbow settings
  - Gum/blower/tool toggles and related parameters
  - Shout banner preference
  - Glue preferences and session linkage
- Startup restore hardens against malformed settings by falling back safely to defaults.

## 15. Current UX Notes
- Tool shout banners use a 3-level megaphone control: `all banners`, `announce-only`, and `silent`.
- Selecting a tool now emits an announcing banner using the same shout surface as live tool usage.
- Toggle-style tools announce explicit state labels such as `GRID ON`, `GRID OFF`, `HEX GRID ON`, `RAINBOW ON`, and `ORTHO SNAP OFF`.
- Tool shout banners are uppercase-normalized at render time.
- Welcome tour and macro playback surfaces share behavior and controls.
- Some internal diagnostics overlays exist for development/testing and are not part of regular drawing workflows.
