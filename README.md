# Polymarket BTC 5-Minute Bot

A trading bot for Polymarket's **BTC and ETH 5-minute / 15-minute Up or Down markets**.

Not a black box: the account it trades is public, every fill is on the record,
and the source ships with the bot.

**Live account & source:** https://depoly.fun

## What this is

Polymarket runs short-duration binary markets on crypto prices — a new
"Bitcoin Up or Down" window every 5 minutes, settling at 100¢ or 0¢.
The bot trades those windows under fixed rules:

- Entry below model fair value, exit on mean reversion
- Fixed per-window sizing with a hard exposure cap
- Daily loss limit that stops trading when it trips
- Paper mode that charges Polymarket's real fee formula

## Why the fee math decides everything

Taker fees are `0.07 × p × (1 − p)` per share, and taker rebates return by
30-day volume tier (Bronze $2k → Obsidian $10M, 3% → 50%). At a 1.5%
effective fee a 2¢ edge on a 50¢ contract is barely positive — the rebate
tier is what makes it a business.

Full breakdown: https://depoly.fun/polymarket-fees-and-rebates/

## Public record

| Metric | Value |
| --- | --- |
| Account | `0xc53375ff94e96100f2b30a4b5775db35218d69a9` |
| Profile | https://polymarket.com/@dangerously-skip-permissions |
| Trades | 33,000+ |
| Volume | $29M+ |

Every number is readable from Polymarket's public API. Nothing here is a screenshot.

## Quick start (paper mode)

```bash
git clone <your-download-link>
cd polymarket-bot
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp config.example.json config.json
chmod 600 config.json
python run.py --paper
