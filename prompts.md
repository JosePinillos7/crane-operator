
# Prompt Log - Crane Operator

## Prompt 1 - Initial specification review

Read spec.md and AGENTS.md carefully.

Review my Crane Operator web app specification. Identify missing inputs, calculations, requirements, validation issues, and possible user errors. Do not modify files or write code.

## Prompt 2 - Specification improvements

Review the suggestions and update spec.md only. Incorporate crane movement limits, capacity lookup rules, safety thresholds, movement speeds, coordinates, pickup and delivery rules, simulation states, displays, and validation requirements.

Do not write application code or modify other files.

## Prompt 3 - Resolve remaining decisions

Update spec.md to define the initial hook height, pickup and delivery coordinates, scenario completion, and Retry behavior.

Preserve all existing requirements and validation examples. Do not create application code or modify other files.

## Prompt 4 - Add overview and approved build stages

Read spec.md without writing code or modifying files. Write a short overview of the complete Crane Operator application, then propose 4 to 6 sequential build stages starting with a visual mockup. For every stage, describe what will be built, which specification requirements it includes, what to test, and what must work before proceeding. Include crane visualization, controls, load selection, pickup and delivery, capacity calculations, safety warnings, timer, score, and custom features. Do not start implementation.

The six-stage plan was approved:

1. **Visual mockup and page layout:** Create an isometric crane scene and page layout for controls, load and target information, chart, timer, score, history, and status. Include construction styling, the illustrative-chart label, educational disclaimer, and desktop/mobile layout. Check clarity and ensure the interface does not imply real crane stability. Proceed when the layout and mockup are clear.
2. **Crane movement and controls:** Add keyboard and touch controls, position displays, specified movement speeds, coordinate system, limits, clamping, and opposing-input cancellation. Test movement rates, readouts, opposing inputs, and clamps. Proceed when movement and displays work correctly at limits.
3. **Load selection, pickup, and delivery:** Add the four loads, fixed locations, target selection, attach/deliver interactions, 5 ft 3D tolerance, and rejection messages. Test valid and invalid interactions and feedback. Proceed when loads can be selected and delivered correctly and invalid attempts are rejected.
4. **Capacity calculations and safety warnings:** Add chart lookup, utilization, chart markers, warning colors, and overload behavior. Include exact/next-larger radius lookup, immediate capacity updates, unrounded safety checks, N/A when unloaded, the 90% warning, and tip-over above 100%. Test the 74/75/76 ft examples, limits, 90%, exactly 100%, and overload. Proceed when chart and threshold behavior matches the specification.
5. **Simulation states, timer, score, and custom features:** Add all simulation states, timer, scoring, load history, reset, retry, and the Capacity Utilization and Risk Indicator. Test pause/resume timing, score/history, completion after four unique deliveries, and overload/retry behavior. Proceed when state transitions and attempt management work together.
6. **Final validation and responsive design:** Refine desktop/mobile layouts and validate the full specification. Test hand calculations, interactions, touch controls, disclaimer, and unrounded safety behavior. Finish when all specified behavior passes without regressions.

## Development approach

The specification was reviewed and refined through questions and feedback before implementation. Suggestions were evaluated before being accepted. The application will be built incrementally, tested, and validated against hand calculations.
