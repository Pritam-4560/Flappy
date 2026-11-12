# Ads in Flapocalypse

Ads are **off** until you fill in `ADS_CONFIG` near the top of the ads section in `index.html`.
With it empty, the game makes no ad network calls and shows no ad buttons.

## How the ads work (quiet but high-earning)

| Placement | Type | When | Why |
|---|---|---|---|
| Revive here | Rewarded (opt-in) | Death screen, once per run | The highest-value offer: players love it |
| x2 coins | Rewarded (opt-in) | Death and victory screens | Pays well, never forced |
| +75 coins | Rewarded (opt-in) | Shop, 3 per day | Gentle extra income |
| Between-runs break | Interstitial | At most every 4 runs and 4 minutes, never in a player's first 6 runs | The only unrequested ad |

There are never ads during a run, no banners, and none in the Daily run.
Game audio pauses while an ad plays.

Tune the limits in `ADS_CONFIG` (`breakEveryRuns`, `breakMinGapSec`, `newPlayerRuns`).

## Option A: Android / iOS app with AdMob

AdMob only works inside native apps, so the game must be wrapped with Capacitor:

1. `npm init -y && npm i @capacitor/core @capacitor/cli @capacitor-community/admob`
2. `npx cap init Flapocalypse com.yourname.flapocalypse --web-dir .`
3. `npx cap add android` (and/or `ios`)
4. In the AdMob console, create an app and two ad units: **Rewarded** and **Interstitial**.
5. Put the AdMob **app id** in `android/app/src/main/AndroidManifest.xml` (the plugin's README shows where).
6. Fill in `admobRewarded` and `admobInterstitial` in `ADS_CONFIG`. Keep `test: true` until AdMob approves the app.
7. Before release you need a privacy policy link and the consent form for EU players (the AdMob plugin's UMP consent calls).

The game detects the AdMob plugin automatically when it runs inside the app.

## Option B: on the web with AdSense H5 Games Ads

This is Google's web equivalent of AdMob for HTML5 games (rewarded and interstitial formats).

1. Get an AdSense account and apply for **H5 Games Ads** for your site (e.g. your GitHub Pages URL).
2. Put your publisher id (`ca-pub-...`) in `h5Client` in `ADS_CONFIG`.
3. Keep `test: true` until approved, then set it to `false`.

Note: ads will not run inside the claude.ai Artifact preview. Use your own hosting (GitHub Pages).

## Testing the flow without an account

Open the browser console on the game page and run `localStorage.setItem('fl.adsMock', '1')`, then reload.
Every ad becomes a 2-second "TEST AD" screen, so you can try revive, x2 coins and the shop bonus.
Remove it with `localStorage.removeItem('fl.adsMock')`.
