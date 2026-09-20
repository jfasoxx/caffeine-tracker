# Caffeine Tracker

A single-page web app that logs what you drink and shows how much caffeine is
still in your system right now, at bedtime, and when you'll drop below a
negligible dose.

**Live:** https://jfasoxx.github.io/caffeine-tracker/

## What it does

- Log drinks from presets (drip coffee, espresso, energy drink, cold brew,
  black tea, cola) or enter a custom amount in mg
- Shows your current caffeine level, your projected level at bedtime, and the
  time you'll fall below 25 mg
- Plots a decay curve with markers for "now" and bedtime
- Set your own bedtime; the chart and projection update with it
- Remove individual drinks or clear the whole log
- Light and dark themes, following your system setting
- Refreshes itself every minute, so the numbers stay current

## How the math works

Caffeine leaves the body on an exponential decay curve. This app uses a
half-life of **6 hours**, meaning every 6 hours the remaining amount halves:

```
remaining = dose * 0.5 ^ (hours_elapsed / 6)
```

Overlapping drinks are summed, so the curve reflects everything still active,
not just your most recent cup.

Six hours is a rough population average. Real half-life varies widely with
genetics, liver function, medication, pregnancy, and smoking — anywhere from
about 2 to 10 hours. Treat the numbers as a useful estimate, not a
measurement.

## Your data stays on your device

Everything is saved in the browser's `localStorage`. There is no account, no
server, and no analytics — nothing is transmitted anywhere. Two consequences
worth knowing:

- Your log is per-device and per-browser. Your phone and laptop keep separate
  histories.
- Clearing your browser data erases the log.

Entries older than 48 hours are dropped automatically, since they no longer
affect the current level.

## Running it locally

No build step, no dependencies. Clone and open the file:

```bash
git clone https://github.com/jfasoxx/caffeine-tracker.git
cd caffeine-tracker
```

Then open `index.html` in any browser.

## Built with

Plain HTML, CSS, and JavaScript in a single file. The chart is hand-drawn SVG.
The only external resource is the Bricolage Grotesque font from Google Fonts.

## License

MIT
