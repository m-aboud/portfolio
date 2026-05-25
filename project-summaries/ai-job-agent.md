# AI Job Agent — Project Summary

## Problem
Senior infrastructure / cloud / AI architect roles are scattered across job boards and demand fast, tailored responses. Manual job-hunting is repetitive, inconsistent, and doesn't scale.

## Solution
An end-to-end automation pipeline:
- **Playwright scraper** with persistent LinkedIn session and anti-detection
- **Filter engine** (keywords, location, seniority)
- **SQLite dedup** so the same role is never seen twice
- **LLM ranker** (multi-provider — OpenAI / Anthropic / Gemini) producing structured fit scores
- **CV generator** (Jinja2 + WeasyPrint) producing tailored PDF CVs per role
- **Telegram notifier** that alerts on high-fit matches with the CV attached

Runs containerised; scheduled via cron or compose loop.

## Impact
- Cuts manual screening time by an order of magnitude
- Improves response speed on senior MENA roles where windows are short
- Surfaces matches that would otherwise be missed across boards

## Stack
Python 3.11 · Playwright · Pydantic · structlog · Jinja2 · WeasyPrint · SQLite · OpenAI/Anthropic SDKs · httpx · Docker · GitHub Actions

## Links
- Code: [github.com/mohammedabood/ai-job-agent](https://github.com/mohammedabood/ai-job-agent)
