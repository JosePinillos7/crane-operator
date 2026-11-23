
# Crane Operator - Web App Specification

## Overview

Crane Operator is an educational, isometric tower-crane simulator for construction management and engineering students. Users operate the jib, trolley, and hook with keyboard or touch controls to pick up and deliver four loads at fixed locations. The app displays crane position, target, attached load, and an illustrative load chart; calculates chart-based capacity utilization; and provides safety warnings, a risk indicator, timer, score, load history, and simulation states. It is not a real crane specification, engineering tool, operator-training replacement, or source for real-world lifting or safety decisions.

## 1. Purpose

Crane Operator is an interactive tower crane simulator for construction management and engineering students. Users operate a tower crane to pick up loads and place them on a building while staying within the crane's rated lifting capacity.

The app helps users understand how load weight and lifting radius affect chart-based capacity utilization. It is an educational simulator, not a real crane specification, engineering tool, operator-training replacement, or guarantee of construction-site safety.

## 2. Inputs

The user can control the crane using keyboard controls:

- Left and Right arrow keys: swing the jib.
- Up and Down arrow keys: move the trolley outward and inward.
- W and S keys: raise and lower the hook.
- Spacebar: attempt to pick up the selected load when no load is attached, or deliver it at the selected target when carrying a load.

Opposing inputs cancel each other on their respective axes (Left/Right, Up/Down, and W/S). Provide touch controls for all crane actions on mobile devices.

Initial movement settings:

- Trolley speed: 5 ft/s.
- Jib swing speed: 5 degrees/second.
- Hook speed: 3 ft/s.
- Hook height range: 0 to 100 ft.
- Trolley radius range: 50 to 150 ft. Clamp movement at both limits, including while carrying a load.

Other inputs:

- Load selection (payload weight; hook and rigging weights are not included):
  - Small pallet: 2,000 lb.
  - Concrete bundle: 5,000 lb.
  - Steel beams: 8,000 lb.
  - Heavy equipment: 12,000 lb.
- Target selection: choose a fixed building delivery location in the scenario.
- Start, Pause, Resume, Reset, and Retry controls manage the simulation.
- Pickup and delivery attempts are accepted only when the hook is at or within 5 ft of the relevant location, measured as straight-line distance in 3D. Rejected attempts display a clear message explaining why.

### Coordinate system and fixed locations

The crane mast is the coordinate origin. Radius is measured horizontally from the mast in feet. Angle is measured in degrees in the horizontal plane: 0 degrees points along the positive x-axis, and positive angles rotate counterclockwise when viewed from above. Height is measured in feet above ground level.

The scenario has fixed pickup and delivery locations. Their coordinates use the radius, angle, and height fields below and are within the trolley-radius and hook-height limits.

| Location | Radius (ft) | Jib angle (degrees) | Height (ft) |
|---|---:|---:|---:|
| Pickup point | 50 | 0 | 0 |
| Building delivery target | 75 | 90 | 20 |

Default crane position:

- Trolley radius: 50 ft.
- Jib angle: 0 degrees.
- Hook height: 0 ft.
- Current load: no load attached.
- Simulation state: ready to start.

## 3. Calculations

The app uses the following illustrative and educational load chart. It is not a real crane specification:

| Radius (ft) | Capacity (lb) |
|---|---:|
| 50 | 20,000 |
| 75 | 13,000 |
| 100 | 9,000 |
| 125 | 7,000 |
| 150 | 5,500 |

### Load capacity lookup and operating limits

Keep the trolley radius between 50 and 150 ft by clamping movement at both limits. Recalculate allowed capacity immediately whenever the actual trolley radius changes, including while carrying a load.

For capacity lookup, use the exact chart value when the actual radius matches a chart row. Between chart rows, use the next larger listed radius. This conservative lookup is a step function, not interpolation. The chart radius is the radius used for the lookup and may differ from the actual radius.

For example:
- At 50 ft, capacity = 20,000 lb.
- At 60 ft, use the 75 ft capacity = 13,000 lb.
- At 80 ft, use the 100 ft capacity = 9,000 lb.

### Load utilization

When a load is attached, calculate load utilization using the actual, unrounded load weight and allowed capacity:

Load Utilization (%) = (Current Load / Allowed Capacity) × 100

Round values only for display; do not use rounded values in safety checks. When no load is attached, display utilization as N/A.

### Safety rules

- Below 90%: normal operation.
- At or above 90%: show a warning.
- At exactly 100%: show a warning; do not tip over.
- Above 100%: trigger the tip-over animation and enter the overloaded state. Stop crane movement and the timer immediately. Enable Retry only after the tip-over animation finishes.

The Capacity Utilization and Risk Indicator is based only on the load utilization calculated above. It does not calculate or represent actual crane stability.

## 4. Outputs

The app displays:

- An animated isometric view of a tower crane.
- The selected load and its weight (lb).
- Current trolley radius (ft).
- Chart radius used for the allowed-capacity lookup (ft).
- Current jib angle (degrees) and hook height (ft).
- Attached-load status and current target, including its location.
- Allowed lifting capacity (lb).
- Load utilization (%) or N/A when no load is attached.
- The illustrative and educational load chart, marked with the actual radius, chart radius, and current load.
- A warning when utilization reaches 90%.
- A tip-over animation when utilization exceeds 100%.
- A timer showing elapsed active simulation time.
- A score showing successfully completed load placements.
- Clear feedback explaining rejected pickup and delivery attempts.
- The current simulation state: ready, active, paused, completed, or overloaded.
- The Capacity Utilization and Risk Indicator.

## 5. Look and Feel

The application should have a clean, modern construction-site design.

- Use a construction-themed color palette.
- Show the tower crane on the main screen.
- Display controls, coordinates, load information, and simulation state clearly.
- Keep the load chart visible while operating.
- Use green, yellow, and red to communicate capacity-utilization levels, without implying actual crane stability.
- Make the interface usable on desktop and mobile devices.
- Provide clear instructions for keyboard and touch controls.
- Keep the educational disclaimer visible: this is a simplified educational simulator and must not be used for real crane operations or safety decisions.

## 6. Validation

The app will be validated against the supplied illustrative and educational load chart. Safety calculations must use unrounded values, with rounding applied only to displayed values.

### Hand calculation test

The app uses the exact chart value at a matching radius and the next larger chart radius between rows.

Test these radii:

1. At 74 ft, use the 75 ft chart value:
   Capacity = 13,000 lb.

2. At 75 ft, use the exact chart value:
   Capacity = 13,000 lb.

3. At 76 ft, use the 100 ft chart value:
   Capacity = 9,000 lb.

4. At 50 ft, use the exact 50 ft chart value:
   Capacity = 20,000 lb.

5. At 150 ft, use the exact 150 ft chart value:
   Capacity = 5,500 lb.

6. Attempt to move below 50 ft or above 150 ft:
   Expected result: radius remains clamped at the corresponding limit.

### Safety validation

At a radius of 76 ft:

- Allowed capacity = 9,000 lb.
- Current load = 8,100 lb.
- Utilization = (8,100 / 9,000) × 100 = 90%.
- Expected result: warning appears.

For a load of 9,000 lb:

- Utilization = (9,000 / 9,000) × 100 = 100%.
- Expected result: warning appears, but the crane does not tip over.

For a load of 9,100 lb:

- Utilization = (9,100 / 9,000) × 100 = 101.1%.
- Expected result: crane tips over, movement and timer stop immediately, and Retry becomes available after the animation finishes.

When no load is attached, expected utilization display: N/A.

The app's displayed values and safety behavior must match these hand calculations.

## 7. Out of Scope

The app will not:

- Replace real crane operator training or certification.
- Provide real-world crane engineering approval.
- Simulate detailed structural mechanics.
- Calculate wind loads or soil stability.
- Represent the load chart of an actual commercial crane.
- Guarantee real construction-site safety.
- Calculate or claim to represent actual crane stability.
- Be used to make real-world lifting or construction-site safety decisions.

## 8. Features

### Feature 1: Load History

Display a history of successfully transported loads, including their weights and placement locations. Keep history for the current attempt; clear it when Reset is selected.

### Feature 2: Capacity Utilization and Risk Indicator

Add a Capacity Utilization and Risk Indicator that changes with load utilization. Show green below 90%, yellow at or above 90% through exactly 100%, and red above 100%. This indicator reflects only the simplified chart-based utilization and does not calculate actual crane stability.

These features are educational additions to the required simulator.

### Simulation states and scoring

- Ready: the simulation has not started.
- Active: crane controls are enabled and the timer runs.
- Paused: crane movement and the timer are stopped; Resume returns to active.
- Completed: each of the four available loads has been successfully delivered once; crane movement and the timer stop.
- Overloaded: utilization has exceeded 100%; crane movement and timer are stopped. After the tip-over animation finishes, Retry starts a completely new attempt: reset the timer and score, clear load history, return the crane to its initial position, remove any attached load, and restore all four loads.
- Add one point for each successfully delivered load.
- The timer measures active simulation time only, excluding paused time.
- Reset restarts the simulation, resets the timer and score, and clears load history.

## Build stages

The application will be developed in the following stages, testing each stage before moving to the next:

### Stage 1: Visual mockup and page layout

- **Build:** An isometric crane scene and page layout for controls, load and target information, chart, timer, score, history, and simulation status.
- **Requirements:** Construction-site styling, visible illustrative-chart label and educational disclaimer, desktop and mobile layout.
- **Check:** Confirm the layout is understandable and required information has a clear place; verify it does not imply actual crane stability.
- **Gate:** The page layout and crane mockup are clear before adding behavior.

### Stage 2: Crane movement and controls

- **Build:** Keyboard and touch controls for jib swing, trolley movement, and hook height, with position displays.
- **Requirements:** Specified movement speeds, coordinate system, trolley and hook limits, clamping, and cancellation of opposing inputs.
- **Check:** Verify movement rates, position readouts, opposing-input cancellation, and clamps at 50–150 ft and 0–100 ft.
- **Gate:** Crane movement and position displays behave correctly at limits before adding loads.

### Stage 3: Load selection, pickup, and delivery

- **Build:** The four load choices, fixed pickup and delivery points, target selection, and attach/deliver interactions.
- **Requirements:** Load weights; pickup at (50 ft, 0 degrees, 0 ft); delivery at (75 ft, 90 degrees, 20 ft); 3D tolerance of 5 ft; clear rejection messages.
- **Check:** Test pickup and delivery at and beyond the tolerance, load attachment and delivery, and the message shown when an attempt is rejected.
- **Gate:** Loads can be selected and delivered correctly, and invalid interactions are rejected before adding safety calculations.

### Stage 4: Capacity calculations and safety warnings

- **Build:** Capacity lookup, utilization display, chart markers, warning colors, and overload behavior.
- **Requirements:** Exact chart-row matches, next-larger-radius lookup, immediate capacity updates, unrounded safety checks, N/A when unloaded, 90% warning, and tip-over above 100%.
- **Check:** Verify the 74, 75, and 76 ft lookup examples; 50 and 150 ft limits; 90% warning; exactly 100% warning without tip-over; and overload behavior above 100%.
- **Gate:** Chart values and thresholds match the specification, and overload stops crane movement before adding full simulation lifecycle features.

### Stage 5: Simulation states, timer, score, and custom features

- **Build:** Ready, active, paused, completed, and overloaded states; timer, score, load history, reset, and retry.
- **Requirements:** Timer excludes paused time; one point per delivery; completion after all four loads are delivered once; reset and retry behavior; Capacity Utilization and Risk Indicator.
- **Check:** Verify pause/resume timing, score and history updates, completion after four unique deliveries, and that overload stops the timer and movement. Confirm Retry waits for the animation, then resets the attempt as specified.
- **Gate:** State transitions, timer, score, history, and retry/reset behavior work together before final validation.

### Stage 6: Final validation and responsive design

- **Build:** Responsive refinements and final consistency checks across desktop and mobile.
- **Requirements:** All specification validation examples, keyboard and touch usability, readable status and chart displays, visible disclaimer, and educational-only framing.
- **Check:** Run the full hand-calculation and interaction checklist, check mobile layout and touch controls, and confirm no display rounding changes safety outcomes.
- **Gate:** All specified behavior and validation examples pass, with no safety, state, or layout regressions.
