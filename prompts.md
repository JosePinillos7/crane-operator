
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

## Prompt 5 - Build Stage 1 visual mockup

Read spec.md and AGENTS.md carefully. Build only Stage 1, the visual mockup and page layout, as a single-file web application in index.html. Include an attractive isometric tower-crane scene and construction-site background, crane controls panel, load selection and target information, illustrative load chart, timer, score, load history, educational disclaimer, and responsive desktop/mobile layout. This stage is visual only: do not implement crane movement, calculations, pickup or delivery behavior, scoring logic, or safety calculations. Keep CSS and any JavaScript inside index.html. Update prompts.md with this request. Do not modify spec.md or AGENTS.md, do not create or modify any other app files, and do not start implementation beyond Stage 1. When complete, summarize what was created and how to test the visual mockup.

## Prompt 6 - Build Stage 2 crane movement and controls

Read spec.md and AGENTS.md carefully. Implement only Stage 2 in index.html: keyboard and on-screen touch controls for jib rotation, trolley movement, and hook height; exact movement speeds; coordinate and position displays; 50–150 ft trolley and 0–100 ft hook limits; clamping; opposing-input cancellation; and a crane visualization that updates as it moves. Do not implement pickup/delivery, capacity calculations, overload behavior, scoring, or timer logic. Preserve the existing visual design and keep CSS and JavaScript inside index.html. Update prompts.md with this request. Do not modify spec.md or AGENTS.md. Test keyboard and touch movement, speeds, opposing controls, and all boundaries, then summarize implementation and test results.

## Prompt 7 - Build Stage 3 load selection, pickup, and delivery

Read spec.md and AGENTS.md carefully. Implement only Stage 3 in index.html: the four exact load choices, selection, the specified fixed pickup and delivery points, pickup and delivery interactions using the specified 3D distance tolerance, visual load attachment to the moving hook, selected-target and load-status updates, success and rejection messages, and prevention of invalid actions. Preserve Stage 1 and Stage 2 behavior and design. Do not implement capacity calculations, overload behavior, timer, scoring, or load-history logic. Update prompts.md with this request. Do not modify spec.md or AGENTS.md. Test all four loads, successful pickup and delivery, attempts outside the tolerance, and visual attachment, then summarize implementation and results.

## Prompt 8 - Build Stage 4 capacity calculations and safety warnings

Read spec.md and AGENTS.md carefully. Implement only Stage 4 in index.html: exact and next-larger-radius capacity lookup from the illustrative load chart; immediate recalculation as trolley radius changes; actual-payload utilization; N/A when unloaded; a warning at or above 90%; tip-over behavior only above 100%; unrounded safety decisions; actual-radius, chart-radius, and attached-load chart markers; and immediate movement stop after overload. Preserve Stage 1, 2, and 3 functionality. Do not implement timer, scoring, load history, or the final simulation lifecycle. Update prompts.md with this request. Do not modify spec.md or AGENTS.md. Test 74, 75, and 76 ft lookup; 90%, exactly 100%, just below and above 100%; unloaded state; capacity updates while carrying; and movement stopping after overload. Summarize implementation and test results.

## Prompt 9 - Build Stage 5 simulation states, timer, score, and features

Read spec.md and AGENTS.md carefully. Implement only Stage 5 in index.html: Ready, Active, Paused, Completed, and Overloaded states; an elapsed-time timer that excludes paused time; one point per successful delivery; delivered-load history with weights and placement locations; completion after all four unique loads are delivered once; Pause and Resume controls; and the specified Reset and Retry behavior, with Retry available only after the tip-over animation finishes. Preserve Stages 1–4 and both custom features in spec.md. Do not change capacity calculations or safety thresholds, and do not begin Stage 6. Update prompts.md with this request. Do not modify spec.md or AGENTS.md. Test pause/resume timing, scoring, history, completion, overload, animation-gated Retry, and Reset behavior. Summarize changes and test results.
