# SKIMS‑Style Flutter Store Starter

A minimalist, production‑ready Flutter starter that clones the clean look-and-feel of SKIMS: product grid, detail pages, cart state, i18n (EN/ES), analytics stubs, a feature flag banner powered by a GraphQL demo, and an image pipeline that supports **AVIF → JPG → PNG** fallbacks.

> **Note**: This project is for portfolio/educational use. “SKIMS” is referenced for design inspiration only; replace any branded assets with your own before publishing.

---

## ✨ Features

* **Material 3 theme** tuned to a SKIMS‑like palette
* **Product grid → detail → add to bag** (Riverpod state)
* **EN/ES language toggle**
* **Holiday Capsule banner** controlled via a local Remote Config default + **GraphQL demo** (graphqlzero) fetch for title
* **Analytics hooks** (Firebase Analytics stubs wired, safe if no Firebase config)
* **Image loader** with **AVIF** support and automatic **JPG/PNG** fallback
* **Web-first**: runs great in Edge/Chrome; Android optional
* **Accessibility**: Semantics on tappable cards & images

---

## 📦 Download

* **Google Drive (source ZIP)**: **[Download the starter](https://drive.google.com/file/d/168haX2fO24BEK5ETX946sCmop3YCqlTc/view?usp=sharing)**

---

## 🚀 Quick Start

```bash
# 1) Get Flutter (stable) + add to PATH
# 2) Clone or unzip this repo
cd skims_flutter_starter_plus
flutter pub get

# 3) Run on web (Edge or Chrome)
flutter run -d edge
# or: flutter run -d chrome
```

**Windows tip**: If you see "Building with plugins requires symlink support", enable **Developer Mode**: press `Win+R`, run `ms-settings:developers`, toggle **Developer Mode** ON.

> If you don’t see Chrome as a device, Edge works fine. If `flutter run` is already running, press **q** to stop, then re‑run.

---

## 🖼️ Product Images (AVIF + fallback)

Place your images here (case‑sensitive on web):

```
assets/images/Skims1.avif
assets/images/Skims2.avif
assets/images/Skims3.avif
assets/images/Skims4.avif
```

Optionally add JPG fallbacks with the same names (e.g. `Skims1.jpg`). The loader will try **.avif → .jpg → .png** automatically.

If you change only the filename **case** on Windows, do a temp rename first so it sticks:

```powershell
Rename-Item assets\images\skims1.avif skims1_temp
Rename-Item assets\images\skims1_temp Skims1.avif
```

---

## 🧩 What’s inside

```
lib/
  core/graphql_client.dart        # GraphQL client (graphqlzero demo)
  remote/remote_config_service.dart  # Local defaults; no Firebase setup required
  state/cart_provider.dart        # Riverpod cart state
  theme/brand_theme.dart          # Material 3 + SKIMS‑like tokens
  widgets/
    product_tile.dart             # Grid card (assets/network + AVIF fallback)
    image_loader.dart (optional)  # Shared loader helper (AVIF→JPG→PNG)
  screens/
    product_list_screen.dart      # Home grid + banner + i18n
    product_detail_screen.dart    # Detail page + Add to Bag
```

---

## 🔧 Configuration

* **Holiday banner on by default**: in `remote_config_service.dart` set

  ```dart
  await _rc!.setDefaults({
    RemoteFlags.holidayCapsuleEnabled: true,
  });
  ```

  Then press **r** (hot reload) in the running terminal.
* **GraphQL text**: `core/graphql_client.dart` uses `https://graphqlzero.almansi.me/api` and a tiny query to fetch a demo title.
* **Analytics**: `services/analytics.dart` stubs `viewItem` and `addToCart`. Safe with no Firebase config; wire up your own if desired.

---

## 🧪 Screenshots

Add images to a `/screenshots` folder and reference them here:

| Home Grid                     | Product Detail                    | Bag                         |
| ----------------------------- | --------------------------------- | --------------------------- |
| ![Home](screenshots/home.png) | ![Detail](screenshots/detail.png) | ![Bag](screenshots/bag.png) |

Take screenshots on Windows with **Win+Shift+S**.

---

## 📦 Build & Ship

**Web (release):**

```bash
flutter build web --release
# outputs to build/web/
```

Host on GitHub Pages, Netlify, or Vercel. For **Google Drive demo**, zip `build/web` and upload; readers can unzip and serve locally (e.g., `npx serve` or `python -m http.server`).

**Android (optional):**

```bash
# after installing Android Studio + SDK, and accepting licenses
flutter run -d emulator-5554  # or a real device
flutter build apk --release
# APK: build/app/outputs/flutter-apk/app-release.apk
```

---

## 🛠️ Troubleshooting

* **Symlink support** (Windows): enable Developer Mode → `ms-settings:developers`.
* **Assets not loading**: check exact filename **case** (web is case‑sensitive). Try `flutter clean && flutter pub get`.
* **Web devices missing**: `flutter config --enable-web`, then restart your terminal/VS Code.
* **CardTheme type error**: ensure `brand_theme.dart` uses `CardThemeData` (not `CardTheme`).
* **ValueNotifier not found**: ensure `graphql_client.dart` imports `package:flutter/foundation.dart`.

---

## 📄 License

MIT — do what you like, but please replace branded imagery and names before production distribution.

---

## 🙌 Credits

* Color & layout inspired by SKIMS (for educational design purposes only)
* GraphQL demo by graphqlzero

---

## 💡 Contributing

PRs welcome for: better theming tokens, accessibility tweaks, and additional product templates.
