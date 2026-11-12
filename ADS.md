# Ads and No Ads in Flapocalypse

Ads are **off** until you fill in `ADS_CONFIG` near the top of the ads section in `index.html`.
With it empty, the game makes no ad network calls and shows no ad buttons or banner.

## What players see

| Placement | Type | When |
|---|---|---|
| Bottom banner | Banner | Always, in a strip under the game. The game moves up, so the banner never covers play. |
| Revive here | Rewarded (opt-in) | Death screen, once per run |
| x2 coins | Rewarded (opt-in) | Death and victory screens |
| +75 coins | Rewarded (opt-in) | Shop, 3 per day |
| Between-runs break | Interstitial | At most every 4 runs and 4 minutes, never in a player's first 6 runs |

No ads ever interrupt a run, and the Daily run has none. Game audio pauses while an ad plays.
Tune the limits in `ADS_CONFIG` (`breakEveryRuns`, `breakMinGapSec`, `newPlayerRuns`).

**No Ads pack** (one-time purchase, product id `no_ads`): removes the banner and the between-runs breaks.
Rewarded ads stay available as an optional choice. The purchase survives NEW GAME, and RESTORE PURCHASE brings it back on a new phone.
Players open it from the **NO ADS** button at the top left of the title screen.

## The Android app (AdMob + No Ads purchase)

The repo already contains the Capacitor Android project (`android/`) with the AdMob and purchase plugins installed.

1. Install Node.js and Android Studio.
2. In the repo: `npm install`, then `npm run android`. This copies the game into `www/`, syncs it and opens Android Studio.
3. In the **AdMob console**, create the app and three ad units: **Banner**, **Rewarded** and **Interstitial**.
4. Replace Google's test app id in `android/app/src/main/AndroidManifest.xml` (`com.google.android.gms.ads.APPLICATION_ID`) with yours.
5. Fill in `admobBanner`, `admobRewarded` and `admobInterstitial` in `ADS_CONFIG` in `index.html`. Keep `test: true` until AdMob approves the app.
6. In **Google Play Console**, create a one-time in-app product with id **`no_ads`** and set its price. The game shows the store price on the buy button.
7. Run `npm run sync` after every change to `index.html`.
8. Before release you need a privacy policy link, the EU consent form (the AdMob plugin's UMP consent calls) and the Play Store "Contains ads" declaration.

For iPhone: `npx cap add ios`, then the same steps with App Store Connect (this needs a Mac).

## On the web (optional)

AdMob does not work in web pages. On the web the game can use **AdSense H5 Games Ads** for the rewarded ads and breaks:
put your publisher id (`ca-pub-...`) in `h5Client`. The banner and the No Ads purchase are app-only.
Ads will not run inside the claude.ai Artifact preview; use your own hosting such as GitHub Pages.

## Testing without an account

In the browser console on the game page run `localStorage.setItem('fl.adsMock', '1')` and reload.
Every ad becomes a 2-second "TEST AD" screen and a fake banner appears, so you can try revive, x2 coins,
the shop bonus and the No Ads purchase (granted instantly in test mode).
Undo it with `localStorage.removeItem('fl.adsMock')` and `localStorage.removeItem('fl.noAds')`.
