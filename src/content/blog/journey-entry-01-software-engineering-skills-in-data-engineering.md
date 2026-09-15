---
title: "How Important Is It to Use Your Software Engineering Skills in Data Engineering"
description: "After years as a backend developer following SOLID, DRY, and clean architecture, I moved into Data Engineering and quietly stopped being a software engineer. Here's how that happened, and what it took to notice."
pubDate: 2026-09-15
author: "Morad Abaz"
category: "My Journey as a Data Engineer"
tags: ["Data Engineering", "Software Engineering", "Career", "PySpark"]
---

After graduating from College, I was working for years developing backend systems and our goal was always to follow SOLID, DRY, clean architecture. Shared libraries, dependency injection, structured logging, unit tests before every deploy. It was second nature.

Then I transitioned to Data Engineering. And somewhere between my first Glue job and my tenth, I stopped being a software developer.

I didn't notice it happening. It was gradual. The first script was a quick prototype. The second one? I copied the first and changed a few lines. By the time I had 70+ pyspark scripts in production, I had the same Iceberg catalog configuration copy-pasted across 10+ files, the same business constants with subtle variations in 4 different scripts, print() statements instead of structured logging, and zero data validation before writing to production tables.

If a junior developer had submitted this as a pull request in my previous backend job, I would have rejected it immediately.

But it was "just a script." That's what I kept telling myself. And I think that's the trap.

When you write a REST API, you think in systems. When you write a Spark job, you think in scripts. The language changes, the tools change, and somehow your engineering standards quietly walk out the door with them.

I once asked a claude to review my entire codebase. The feedback was clear: your pipelines work, but they're not engineered. No shared utility module. No audit columns for traceability. No assertions on data quality. No structured logging with row counts and run IDs.

The irony is that every single one of these problems has a solution I already knew. A shared python script for utils is just a library. Adding _ingested_at and _job_run_id to every table is just traceability. Validating row counts before a write is just a test. Replacing print() with the logging module is just... basic.

I already had the tools. I just forgot to unpack them.

I don't think this is just a me problem. I've seen it in other engineers making the same transition. We learn Spark, we learn Iceberg, we learn Terraform — but we leave behind the engineering principles that made us good at building software in the first place. We trade clean architecture for "it runs." We trade tests for "I'll check the output manually." We trade observability for print().

The transition from Software to Data Engineering isn't just about learning new tools. It's about recognizing the moment you stopped applying what you already know — and bringing it back.
