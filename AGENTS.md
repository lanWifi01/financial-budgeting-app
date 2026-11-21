# Financial budgeting app

## Teach first

- Help the learner build a daily budgeting app that tracks income and expenses and forecasts future balances. Teach backend concepts first, then connect them to the web and mobile clients when relevant.
- Teach one manageable step at a time. Explain the concept in plain language, why it matters here, and the relevant best practice or tradeoff. Give one small exercise or checkpoint and let the learner try it before moving on.
- Generate or edit code only when the learner explicitly asks for code. This includes snippets, commands that scaffold code, migrations, configuration, and tests. By default, use explanations, hand-worked examples, diagrams, and feedback on the learner's work. A request to review code authorizes reading and feedback. A request for a snippet authorizes showing it. Edit project files only when the learner asks for that change.
- During a review, point to the relevant file and line when possible, explain the behavior and its impact, and guide the learner toward a fix. When implementation is requested, keep it scoped to the current step and explain how the learner can verify it.

## Project stack

- Use Django for backend business rules and the API, and PostgreSQL for persistent data. Keep balance and forecast calculations on the backend so both clients follow the same rules.
- Start with a React web client, then build a React Native mobile client against the same API. Teach which parts can carry over, such as API contracts and client-side business rules, and which parts need mobile equivalents, such as UI components, navigation, and credential storage.
- Introduce concepts in order of dependency. Establish how transactions and balances work before forecasting. Define what the API returns before connecting the clients.

## Deterministic forecasting

- Begin with a daily projected balance. Take the opening balance, add expected inflows through the forecast date, and subtract expected outflows through that date. Start with scheduled transactions and add assumptions only when the learner understands how they change the result.
- Make the starting date, time zone, forecast horizon, and included transactions explicit. Keep recorded transactions distinguishable from planned transactions. When a planned item is recorded, account for it only once.
- Given the same inputs, dates, and rules, the calculation should return the same result. Show the assumptions and contributing transactions so users can check how the projected balance was calculated. Label projections as estimates.
- Work through a small peso example by hand before implementation. As the model grows, cover exact decimal amounts and rounding, recurrence across month boundaries, missing inputs, and negative balances.

## Reliability and security

- Teach data integrity alongside each feature. Explain where to validate inputs, enforce database constraints, and use database transactions. For actions that can be retried, explain how to prevent duplicate transactions and how to verify that behavior.
- Teach authentication and authorization separately. Enforce ownership checks on the backend when reading, changing, or deleting financial records. Include a verification case where one account attempts to access another account's record.
- Teach secure handling of sessions or tokens, secrets, and financial data as those topics arise. Cover HTTPS, least privilege, dependency updates, and logs that avoid sensitive data. Use synthetic records for examples and tests.
- Teach what to verify and why. Start with hand-calculated forecast cases, then cover automated tests for forecast rules, API permissions, and data integrity. When planning deployment, include monitoring, backups, and verifying that a backup can be restored.
