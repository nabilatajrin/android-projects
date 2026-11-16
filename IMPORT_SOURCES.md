# Import full Android project sources

This monorepo already includes:

- Root README listing all 16 practice apps
- Per-project README stubs
- Top-level `build.gradle` / `settings.gradle` for each app

**`lost-phone-finder-android` is NOT merged** — keep it as its own repo.

To copy the remaining app source (Java, layouts, manifests) from the original repos into this monorepo, run locally:

```bash
git clone https://github.com/nabilatajrin/android-projects.git
cd android-projects

for name in alert-dialog animation audio-capture audio-manager auto-complete \
  background-location-service bluetooth bmi-calculator camera code-snippets \
  coffee-ordering-app courtcounter diceout implicit-intent locationfinder note-taking-app
do
  git clone --depth 1 "https://github.com/nabilatajrin/android-$name.git" "/tmp/a-$name"
  rsync -a --exclude='.git' --exclude='.idea' --exclude='build' --exclude='.gradle' \
    --exclude='*.mp4' --exclude='*.apk' --exclude='local.properties' \
    "/tmp/a-$name/" "android-$name/"
done

git add android-*
git commit -m "Import full sources from original android-* repos"
git push
```

Then delete the old individual `android-*` repos in GitHub Settings (keep `lost-phone-finder-android`).
