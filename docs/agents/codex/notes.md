# Codex Notes

## Landing Page

- Main behavior lives in `index.html`; there is no build step.
- Store redirect URLs are defined at the top of the inline `<script>` as `APP_STORE_URL` and `PLAY_STORE_URL`.
- Auto-redirect is intentionally limited to detectable mobile devices:
  - Android user agents go to Google Play.
  - iPhone, iPad, iPod, and iPadOS-on-Mac user agents go to the App Store.
  - Desktop or unknown devices stay on the page and can pick a store manually.

## Fast Paths

- Read the app page: `sed -n '1,260p' index.html`
- Check repo state: `git status --short`
- Verify the important strings: `rg -n "APP_STORE_URL|PLAY_STORE_URL|getTargetStore|status-message" index.html`

## Gotchas

- Keep manual store buttons even when auto-redirecting; TikTok in-app browser flows can block or delay navigation.
- Preserve the iPadOS detection fallback: `navigator.platform === 'MacIntel' && navigator.maxTouchPoints > 1`.
