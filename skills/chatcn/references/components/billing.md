# Billing

Monetizing AI apps: credit balance and top up, usage forecast, paywalls, plan picker, model upsell, trial countdown, onboarding tours. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## chatcn Pro

- `first-run-tour` (Pro): **First run tour.** Spotlight coachmarks that point at the real interface, with a cut out that glides from target to target and a tour that resumes where it was left.
- `usage-forecast` (Pro): **Usage forecast.** Not how much was used, but when it runs out: the recent pace carried forward, said as a date with its likely range, on a chart you can read day by day.
- `low-credit-banner` (Pro): **Low credit banner.** A warning before credits run out, in days at the real pace, with the way out right beside it, or one quiet line above the composer.
- `api-key-setup` (Pro): **API key setup.** Bring your own key, proven before it is saved: a real test call with its reply and timing, then the models the key can reach.
- `byok-keys` (Pro): **Bring your own keys.** One row per provider: the masked key, whether it works, when it was last used, and a test that runs in place.
- `trial-countdown` (Pro): **Trial countdown.** Days left in a trial and exactly what happens at the end, in plain words: a downgrade or a charge, when, and how much. As a card, a header chip, or the whole trial as a row of days.
- `persona-onboarding` (Pro): **Persona onboarding.** Role and goal questions that tailor the first chat, with that chat drawn beside them and redrawn on every answer.
- `capability-card` (Pro): **Capability card.** What the assistant can and cannot do, shown before the first message, with example lines that start the prompt.
- `connect-first-source` (Pro): **Connect first source.** The onboarding step that connects one source and answers from it before reading has finished.
- `training-consent` (Pro): **Training consent.** Data use choices at onboarding in plain language, off by default, with a summary of exactly what is shared.
- `mobile-paywall` (Pro): **Mobile paywall.** A full screen phone paywall that answers the money questions: what is charged, when, and how to stop it.
- `checkout-success` (Pro): **Checkout success.** Back from checkout, in the same app: wait for the payment honestly, then unlock what was paid for in place.
- `cancel-flow` (Pro): **Cancel flow.** Cancelling without the maze: one optional reason, at most one fitting offer, and a confirmation that says what is kept and what goes.
- `whats-new` (Pro): **What's new.** A feature announcement shown once per release, one feature at a time, that never comes back after Got it.
- `cost-odometer` (Pro): **Cost odometer.** A run cost that rolls its digits as it spends, with a cap marker, a warning near and past the cap, and a breakdown of where the money went.
- `credit-balance` (Pro): **Credit balance.** A credit pill whose digits roll when the balance changes, amber and red low and empty states with labels, and a popover with spend by action, the latest spend and a top up button.
- `credit-top-up` (Pro): **Credit top up.** Credit packs with price per credit and the best value marked, a custom amount, auto top up with a threshold, processing and failed states, and a receipt where the new balance rolls in.
- `limit-paywall` (Pro): **Limit paywall.** The upgrade at the moment of the limit: the locked result dithered or blurred behind one recommended plan, one action, Maybe later and a ticking countdown to the reset. Upgrading dissolves the treatment in place.
- `model-upsell` (Pro): **Model upsell.** Locked premium models inside the model list with a lock badge, what each unlocks and one upgrade action. A drop-in for the free model picker that also renders inline.
- `in-app-plan-picker` (Pro): **In-app plan picker.** Plans compared by model access, limits and speed with the recommended plan preselected, a monthly or yearly switch where prices roll, the current plan marked and a downgrade warning that lists what goes away.
- `action-cost-hint` (Pro): **Action cost hint.** The credit cost on generate, upscale and run buttons, rolling as parameters change it, with a tooltip breakdown and the balance after, and a blocked state that says how many more credits are needed.
