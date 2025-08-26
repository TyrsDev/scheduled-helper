# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a scheduled news search application that runs every 15 minutes via GitHub Actions, using OpenAI's GPT-5-nano model with web search capabilities to find positive Norwegian news articles.

## Key Commands

### Development
- `python news_search.py` - Run the news search script locally (requires OPENAI_API_KEY environment variable)
- `pip install -r requirements.txt` - Install Python dependencies

### Testing
- Manual testing is done through GitHub Actions workflow dispatch
- The workflow validates environment and checks results automatically

## Architecture

### Core Components
- `news_search.py` - Main script using OpenAI responses API with web_search_preview tool
- `.github/workflows/hourly-news-search.yml` - GitHub Actions workflow for scheduled execution
- `requirements.txt` - Python dependencies (openai, requests)

### OpenAI Integration
- Uses the `responses` API (not chat completions) with `gpt-5-nano` model
- Configured with `web_search_preview` tool for real-time web searches
- Location context set to Trondheim, Norway
- Low verbosity and minimal reasoning effort for efficiency
- Retry logic with exponential backoff for robustness

### Output Format
- Results saved as JSON with timestamps
- Two output files: timestamped and latest versions
- Includes URL validation and extraction from model responses
- Usage tracking for OpenAI API calls

### GitHub Actions Configuration
- Runs every 15 minutes via cron schedule
- Manual dispatch available with debug option
- Artifacts uploaded with 30-day retention
- Environment validation for API key
- Results summary in GitHub Actions UI

## Environment Requirements
- `OPENAI_API_KEY` - Required GitHub secret for API access
- Python 3.12 runtime
- Ubuntu latest for GitHub Actions execution