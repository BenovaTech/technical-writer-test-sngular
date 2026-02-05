# Autonomy scenarios — Answers

This document explains how I approach common situations when working autonomously as a Technical writer, based on my real working habits and experience.

---

## Scenario 1: Undocumented API behavior

When documentation is missing or incomplete, I don’t block on it. I start by exploring the API myself. I test the endpoint with invalid inputs such as missing fields and wrong data types, using tools like curl or Postman, and I also look directly at the service and controller code to understand how errors are handled.

I document only what I can validate. If I’m confident about the behavior, I include concrete examples for error responses, status codes, and typical mistakes. If something is unclear, I clearly state the assumption instead of guessing, so developers know what is confirmed and what may change.

For future reference, I document my findings and assumptions in a clear way, so the content can be easily updated once the API team is available. My goal is to keep the documentation useful without spreading incorrect information.

---

## Scenario 2: Conflicting information

When I find conflicting information, my first step is to understand which source reflects the current reality. I check the actual codebase, recent commits, framework versions, and how similar problems are already solved in the project.

To decide which approach to document, I prioritize what is already used in the codebase, what aligns with current best practices and also what is easier to understand and maintain for developers.

If I can’t get a definitive answer before the deadline, I make a reasoned choice and document it clearly. I also mention that alternative approaches exist and explain why the chosen one is used in the codelab. This way, developers understand the context instead of blindly following instructions.

---

## Scenario 3: Last-Minute breaking changes

If a breaking change appears just before publication, my first step is to assess the real impact on the codelab. I identify which steps are affected and whether the change requires small adjustments or a deeper rewrite.

To work efficiently, I review the release notes, update the code locally, and walk through the codelab steps myself to make sure everything still works. I focus on fixing only what is necessary to keep the tutorial correct and usable.

At the same time, I communicate clearly with stakeholders and SMEs. I explain what changed, what needs to be updated, and whether it affects the delivery timeline.
