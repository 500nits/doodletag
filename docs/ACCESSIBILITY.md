# DoodleTag Accessibility Research

This document is not a marketing statement and not a compliance badge draft.

Its purpose is to answer a practical product question:

- what should accessibility mean for DoodleTag,
- what should the team care about first,
- and how can DoodleTag become reasonably accessible for the kind of app it is

DoodleTag is a casual collaborative drawing app. That matters because accessibility here is not only about reading
screens or filling forms. It is about whether people with different abilities can meaningfully participate in a playful,
gesture-heavy, visual drawing experience.

## Why Accessibility Is Different For DoodleTag

DoodleTag is not:

- a document viewer
- a checkout flow
- a settings-heavy utility app
- or a structured data-entry app

It is:

- a freeform drawing surface
- a collaborative doodling tool
- a playful "passatempo" app
- a gesture-driven creative space

That means the right accessibility bar is not "does every screen behave like a standard productivity app?"

The right bar is:

- can users discover the controls,
- can users understand the state of the app,
- can users perform the major flows,
- and can users participate in the experience with reasonable independence even if some parts remain inherently visual

## Research Lens: The Right Questions

Accessibility work for DoodleTag should be driven by these questions:

- Can users discover and understand the controls?
- Can users with screen readers or low vision operate the major app flows?
- Can users with limited dexterity reliably hit controls and avoid accidental destructive actions?
- Can users understand collaborative state such as Glue, recording, replay, export, and session recovery?
- Can users recover from mistakes without confusion?
- Which parts of the app are inherently visual or spatial, and therefore cannot be made fully equivalent for every user?

These questions are more useful for DoodleTag than chasing a vague generic label such as "accessible app".

## What To Care About In DoodleTag

### 1. Control Discoverability

Users need to be able to find and identify the controls before they can use the app.

For DoodleTag, this means caring about:

- semantic labels for menu buttons
- labels and hints for utility buttons
- not relying on icon shape alone
- not relying on color alone
- keeping the control model stable over time

The current app depends heavily on icon-only controls, so discoverability is one of the highest-value accessibility
areas to improve.

### 2. State Awareness

DoodleTag has many modes and transient states:

- solo vs Glue
- recording vs not recording
- replaying vs idle
- tool modes such as rainbow, gum, orthogonal, air blower
- banner mode changes
- export readiness
- waiting / connecting / sharing flows

For accessibility, state awareness is critical.

Users should be able to tell:

- what mode they are in now
- what just changed
- what action succeeded or failed
- and what the app expects next

This is why shouts, confirmations, and explicit feedback matter in DoodleTag more than in a simpler app.

### 3. Touch and Motor Accessibility

Because the app is gesture-heavy, motor accessibility has two different layers:

- control-surface accessibility
- drawing-surface accessibility

Control-surface accessibility is very improvable:

- make buttons easy to hit
- avoid tiny effective hit targets
- confirm destructive actions
- avoid requiring long-press as the only route to critical functionality when possible

Drawing-surface accessibility is harder:

- freehand drawing requires precision
- long drags and continuous motion can be tiring
- some tools depend on geometric control

The team should still improve what can be improved, but should be honest that not all freeform drawing interactions can
be made equally easy for all users.

### 4. Visual Accessibility

DoodleTag is visually expressive, so visual accessibility should focus on:

- non-color cues for tool identity and state
- sufficient contrast in controls and status overlays
- readable feedback banners
- compatibility with display scaling where possible
- not making important distinctions depend only on hue

Particular risk areas:

- rainbow and color-heavy modes
- subtle active/inactive differences
- low-contrast icon treatments
- overlay text against dynamic backgrounds

### 5. Cognitive Accessibility

DoodleTag should remain understandable as a playful app.

That means accessibility work should also reduce confusion:

- clear confirmation text
- explicit failure messages
- fewer ambiguous mode transitions
- clearer relationship between tap and long-press actions
- understandable reset behavior

An accessible playful app is still playful, but not cryptic.

### 6. Collaboration Accessibility

Glue is a defining feature of DoodleTag, so accessibility work must include collaboration-specific concerns.

Users need understandable feedback for:

- entering Glue
- waiting for a peer
- connecting
- disconnecting
- restoring solo state
- clearing saved shared session state

This is one of the places where DoodleTag can become more accessible without changing the drawing experience itself:
clear collaboration feedback helps all users, including those relying on screen readers or reduced visual attention.

## Concrete Accessibility Areas To Audit

If the team wants a practical audit checklist, these are the most important areas.

### A. Screen Reader Audit

Test with VoiceOver and TalkBack for these flows:

- launch the app and identify the main controls
- open and close the menu
- identify each tool and utility button
- undo, clear, reset view, and export
- start and stop macro recording
- share the last macro
- enter and exit Glue
- understand waiting / connection / failure states

Questions:

- Are controls labeled?
- Are important state changes announced?
- Does focus remain stable when menus animate?
- Are long-press-only actions discoverable?

### B. Touch Target Audit

Check whether all important controls have comfortable effective hit targets.

Questions:

- Can the buttons be hit without precision tapping?
- Do compact controls keep a larger invisible tap area?
- Are destructive actions separated well enough from nearby controls?

### C. Color and Contrast Audit

Questions:

- Can users identify controls without depending only on color?
- Are active states distinguishable in grayscale or low-saturation conditions?
- Are banners and overlays readable against the current backgrounds?

### D. Dynamic Type / Scaling Audit

Questions:

- Does the control surface still work under larger font or display scaling?
- Do confirmation sheets remain readable and tappable?
- Do important buttons get clipped or pushed off-screen?

### E. Error Recovery Audit

Questions:

- Are failed actions announced clearly?
- Are destructive flows confirmed?
- Are resets scoped clearly so the user understands what will and will not be removed?

## Practical Accessibility Strategy For DoodleTag

The most realistic path is not to chase "perfect accessibility" all at once.

The better strategy is to improve accessibility in layers.

### Layer 1: Make The Control Surface Accessible

This is the highest-value first layer.

It includes:

- explicit semantics for controls
- meaningful control labels
- larger effective touch targets
- clearer confirmations
- consistent announcements for mode and state changes

This work is highly worthwhile because it improves the app for almost everyone and is technically achievable.

### Layer 2: Make App State Understandable

This includes:

- announcing success, failure, and waiting states
- making Glue state easy to understand
- making macro state easy to understand
- keeping reset and export flows explicit

This is especially important in DoodleTag because the app has many invisible internal modes.

### Layer 3: Reduce Visual-Only Dependencies

This includes:

- avoiding color-only meaning where possible
- using labels and feedback for tool identity
- making active states clearer
- improving readability of overlays and banners

### Layer 4: Improve Participation In The Drawing Experience

This is the hardest layer and should be approached pragmatically.

Possible directions:

- tool presets that reduce precision demand
- more snap-assisted interactions
- more forgiving gesture interpretation where it helps
- alternative ways to trigger some actions without fine motor control

This layer will likely always remain partial, because freeform drawing is inherently spatial.

## Current Research-Based Recommendations

Based on the current state of the app and the nature of the product, the team should prioritize:

1. semantics and discoverability for all main controls
2. stable, explicit feedback for mode and state changes
3. comfortable hit targets for all important controls
4. clear confirmation and recovery behavior
5. Glue accessibility as a first-class concern
6. reduced dependence on color alone for important meaning

Only after those are in good shape should the team spend energy on formal public claims or compliance paperwork.

## Standards As Supporting Tools, Not The Main Goal

Standards still matter, but they should support the research above rather than replace it.

Useful references:

- `WCAG 2.2` for semantics, focus, contrast, understandable interactions, and error prevention
- Apple accessibility disclosures for store-facing claims once real support is tested
- `VPAT` / Accessibility Conformance Reports only if formal external reporting is ever needed

There is no single public accessibility score that solves this for DoodleTag.

## What Is Accessible Now

At the current level of implementation, DoodleTag can reasonably say that it is improving accessibility in the control
surface and feedback systems.

Concrete areas of progress include:

- explicit accessibility semantics for the main menu and utility controls
- clearer naming of icon-driven controls
- compact utility buttons with a larger effective tap target
- more explicit confirmations for destructive or state-changing actions
- shout/banner feedback that makes hidden app state more visible

This is meaningful progress, but it should be understood as control and state accessibility progress, not as proof that
the entire creative drawing experience is equally accessible for every user profile.

## What The App Is Designed For

DoodleTag is designed for:

- casual drawing
- playful collaborative doodling
- expressive gesture-based creation
- solo and Glue-based shared drawing sessions

This purpose should guide the accessibility effort.

The goal is not to force the app into the mold of a generic form-based utility. The goal is to make its real creative
and collaborative flows as understandable and operable as reasonably possible.

## What Limitations Remain Because It Is A Visual Collaborative Drawing Tool

Some limitations are structural.

These include:

- freeform spatial drawing is inherently difficult to translate into a fully equivalent non-visual experience
- collaborative drawing results remain primarily visual even when state changes can be announced clearly
- some creative tools depend on geometry, layering, motion, and color relationships
- long continuous gestures and precision drawing will remain harder for some users even if the controls around them are
  accessible

This does not mean accessibility work is optional. It means the right goal is reasonable accessibility, honest support,
and good participation, not a misleading promise of universal equivalence.

## Recommended Next Steps

1. Audit all main controls with VoiceOver and TalkBack on real devices.
2. Verify that all important controls have labels, hints where needed, and stable focus behavior.
3. Audit hit targets across the whole control surface, not only the menu.
4. Review color-only tool states and add non-color cues where practical.
5. Audit all Glue, macro, export, and reset flows for clear announcements and recovery behavior.
6. Test larger display and text scaling for dialogs, confirmations, and menu flows.
7. Keep public positioning secondary until the actual user flows are tested thoroughly.

## Summary

For DoodleTag, accessibility should be treated as a concrete product-research and product-design problem.

The main goal is:

- make the control surface understandable
- make state changes explicit
- make collaboration flows clearer
- make controls easier to hit
- reduce visual-only dependencies where possible
- and accept that some parts of freeform collaborative drawing will remain inherently visual

That is the right path for making DoodleTag reasonably accessible.
