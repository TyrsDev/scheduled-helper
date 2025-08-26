# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a scheduled news search automation tool that runs every 15 minutes via GitHub Actions. It uses OpenAI's GPT-5-nano model with web search capabilities to find positive news articles from Norway, specifically targeting Trondheim context.

## Architecture

- **Main script**: `news_search.py` - Core functionality using OpenAI responses API with web_search_preview tool
- **Automation**: GitHub Actions workflow (`.github/workflows/hourly-news-search.yml`) runs the script every 15 minutes
- **Output**: Results saved as timestamped JSON files and artifacts

## Key Components

### News Search (`news_search.py`)
- Uses OpenAI responses API with `gpt-5-nano` model
- Configured with web_search_preview tool for Norwegian location context (Trondheim)
- Implements retry logic with exponential backoff
- Extracts and validates URLs from response text using regex
- Saves results to both timestamped and "latest" JSON files

### GitHub Actions Workflow
- Runs on schedule (every 15 minutes) and manual trigger
- Sets up Python 3.12 environment with pip caching
- Validates OpenAI API key from GitHub secrets
- Uploads results as artifacts with 30-day retention
- Provides workflow summary with JSON results

## Environment Setup

Required environment variable:
- `OPENAI_API_KEY` - Must be set in GitHub repository secrets

## Development Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Run news search locally
python news_search.py

# Manual workflow trigger (GitHub Actions tab)
# Enable debug logging via workflow_dispatch input
```

## Configuration

The search is configured for:
- Location: Trondheim, Norway (country: "NO", city: "Trondheim")
- Search context: "low" (for efficiency)
- Text verbosity: "low"
- Reasoning effort: "low"
- Target: 1 positive news article URL per search

## Output Files

- `news_results_YYYYMMDD_HHMMSS.json` - Timestamped results
- `news_results_latest.json` - Most recent results (overwritten each run)
- Workflow artifacts available for download from Actions tab