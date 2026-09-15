---
title: "Going from Software Engineering Skills to Data Engineering"
description: "I spent years as a backend developer following SOLID, DRY, and clean architecture. Then I moved into Data Engineering and quietly stopped being a software engineer. Here's how that happened, and what it took to notice."
pubDate: 2026-09-15
author: "Morad Abaz"
category: "My Journey as a Data Engineer"
tags: ["Data Engineering", "Software Engineering", "Career", "PySpark"]
---

After graduating from college, I spent years developing backend systems where the goal was always SOLID, DRY, clean architecture. Shared libraries, dependency injection, structured logging, unit tests before every deploy. It was second nature.

Then I transitioned to Data Engineering. And somewhere between my first Glue job and my tenth, I stopped being a software engineer.

## How it happened without me noticing

It was gradual. The first script was a quick prototype. The second one? I copied the first and changed a few lines. By the time I had 70+ PySpark scripts in production, this is what my codebase actually looked like:

- The same Iceberg catalog configuration copy-pasted across 10+ files
- The same business constants, with subtle variations, duplicated in 4 different scripts
- `print()` statements instead of structured logging
- Zero data validation before writing to production tables

If a junior developer had submitted this as a pull request at my previous backend job, I would have rejected it immediately.

But it was "just a script." That's what I kept telling myself. And I think that's the trap.

## The mindset shift nobody warns you about

When you write a REST API, you think in systems. When you write a Spark job, you think in scripts. The language changes, the tools change, and somehow your engineering standards quietly walk out the door with them.

I once asked Claude to review my entire codebase. The feedback was clear: the pipelines worked, but they weren't engineered.

- No shared utility module
- No audit columns for traceability
- No assertions on data quality
- No structured logging with row counts and run IDs

## The tools were never the problem

The irony is that every single one of these problems has a solution I already knew, from years before I ever wrote a line of Spark:

- A shared Python module for utils is just a library.
- Adding `_ingested_at` and `_job_run_id` to every table is just traceability.
- Validating row counts before a write is just a test.
- Replacing `print()` with the `logging` module is just... basic.

I already had the tools. I just forgot to unpack them.

## Why this matters beyond me

I don't think this is just a me problem. I've seen it in other engineers making the same transition. We learn Spark, we learn Iceberg, we learn Terraform — but we leave behind the engineering principles that made us good at building software in the first place.

We trade clean architecture for "it runs." We trade tests for "I'll check the output manually." We trade observability for `print()`.

Data pipelines are software. They deserve the same discipline as any backend system: modularity, tests, validation, traceability, and logging that tells you what happened at 3 a.m. without needing to SSH into anything. Skipping that discipline doesn't make the pipeline simpler, it just moves the cost from write-time to debug-time, and someone always pays it later.

The transition from Software to Data Engineering isn't about learning new tools. It's about recognizing the moment you stopped applying what you already know, and bringing it back.
