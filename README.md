# SKONGA AI — skonga-prod

**Clean production baseline.**  
Repo **`skonga-ai-v1` is frozen** — leave it as-is. Work only here.

Student AI app (Tanzania): Capacitor Android · soft free limits · M-Pesa / Tigo / Airtel / Halo.

## Clone

```bash
cd ~
git clone https://github.com/shabanihamidu19-cell/skonga-prod.git
cd skonga-prod
```

## First setup — import full app UI once

```bash
mkdir -p www scripts legal

# Full working index from last good v1 commit (not the broken tiny file)
curl -sL -o www/index.html \
  "https://raw.githubusercontent.com/shabanihamidu19-cell/skonga-ai-v1/14e341f/www/index.html"

# Pay page + assets from v1 main (optional)
curl -sL -o www/pay.html \
  "https://raw.githubusercontent.com/shabanihamidu19-cell/skonga-ai-v1/main/www/pay.html"
curl -sL -o www/manifest.json \
  "https://raw.githubusercontent.com/shabanihamidu19-cell/skonga-ai-v1/main/www/manifest.json"
curl -sL -o www/sw.js \
  "https://raw.githubusercontent.com/shabanihamidu19-cell/skonga-ai-v1/main/www/sw.js"

# Fixes: Profile + panel X / Android back
curl -sL -o scripts/fix_profile.py \
  "https://raw.githubusercontent.com/shabanihamidu19-cell/skonga-ai-v1/main/scripts/fix_profile.py"
curl -sL -o scripts/fix_panels_close.py \
  "https://raw.githubusercontent.com/shabanihamidu19-cell/skonga-ai-v1/main/scripts/fix_panels_close.py"
python3 scripts/fix_profile.py
python3 scripts/fix_panels_close.py

# Check size (~240KB+)
wc -c www/index.html

git add www scripts
git commit -m "Import app UI + profile/panel fixes"
git push origin main
```

## Legal (your zip)

```bash
mkdir -p legal
unzip -o /path/to/skonga-legal.zip -d /tmp/sklegal
cp -r /tmp/sklegal/skonga-legal/* legal/   # adjust if zip layout differs
git add legal
git commit -m "Add legal pages"
git push origin main
```

Deploy `legal/` to HTTPS. Point app `EXTERNAL_LEGAL` to that domain.

## Plans (TZS)

| Plan | Price | Duration |
|------|------:|----------|
| 1 Day | 620 | 24h |
| 1 Week | 3,500 | 7d |
| 1 Month | 5,000 | 30d |
| 1 Year | 45,000 | 365d |

## Your tasks

- [ ] Import UI (commands above)
- [ ] Add `legal/` from zip + deploy
- [ ] Real `google-services.json`
- [ ] Backend: chat API + STK + Pro entitlement
- [ ] Signed APK / Play listing

## Build

```bash
npm install
npx cap add android
npx cap sync android
```

## License

MIT — KCL Platform TZ
