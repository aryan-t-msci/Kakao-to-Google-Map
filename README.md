# Kakao → Google Coordinate Locator

Paste a Kakao place link (e.g. `https://place.map.kakao.com/838484446`), get the exact
WGS84 coordinate, and open the same rooftop on Google Maps as a coordinate pin — not as a
Korean text search. Built for geocoding spot-checks.

The single file (`index.html`) auto-detects how it's opened:

- **Lite mode** — open the file directly (double-click). No key, no setup. Resolves a Kakao
  place link through a public relay, shows the Google satellite, gives you the coordinate and
  all the map links. Best-effort, fine for spot-checks. The Kakao satellite panel is off here.
- **Full mode** — open it from a real web address (a hosted link or `localhost`) with a Kakao
  JavaScript key. Adds the **Kakao satellite next to Google** and reliable name/address search.

---

## Host it on GitHub Pages (recommended for sharing)

This gives you a link colleagues just open — no key for them, nothing to install — with the
side-by-side satellite working.

**1. Get a Kakao JavaScript key**
- developers.kakao.com → sign in → My Application → add an app
- Open the app → **App Keys** → copy the **JavaScript key** (not REST, not Admin)
- App → **Kakao Map → Activation → ON**

**2. Bake the key into the file**
- Open `index.html` in any text editor
- Near the top of the `<script>`, set:
  ```js
  const BAKED_KEY = "your_javascript_key_here";
  ```
- A JavaScript key is **domain-locked**, so it's safe to ship inside the page once step 4 is done —
  it can't be used from any other address.

**3. Publish on GitHub Pages**
- Create a repo, add `index.html` to it
- Repo **Settings → Pages → Build from a branch** → pick your branch, folder `/ (root)` → Save
- After a minute you get a URL like `https://YOURNAME.github.io/REPO/`

**4. Register the address with Kakao**
- In your Kakao app → **App Settings → Platform → Web → Add site domain**
- Add the **origin only** (no path):
  ```
  https://YOURNAME.github.io
  ```
- Kakao matches on the address, not the path, so this one entry covers every page in the repo.

**5. Open the link.** You should see the green **Full mode** banner and the Kakao satellite
beside Google. If you get the blue **Lite mode** banner instead, see Troubleshooting.

---

## Message to send colleagues

> Here's a quick tool to get Google Maps coordinates from a Kakao place link:
> `https://YOURNAME.github.io/REPO/`
>
> 1. Open the Kakao place page and copy its link (looks like `place.map.kakao.com/...`)
> 2. Paste it into the box and press **Find**
> 3. Check the pin is on the right building in the two satellite views
> 4. Copy the **Google Maps — pin** link, or the lat, lng

---

## Troubleshooting

**Blue "Lite mode" banner on the hosted link (Kakao panel off):**
- The address you opened isn't registered with Kakao. Open the setup panel in the tool — it shows
  the **exact** address to register. Add that under Platform → Web (step 4).
- Wrong key type — must be the **JavaScript** key.
- Kakao Map feature is **OFF** — turn it ON (step 1).
- Use the **Test & save** button in the setup panel; it tells you which of these is wrong.

**"Couldn't read the place page" in Lite mode:**
- The public relay was down or your browser blocked the call. Try again, or use Full mode and
  search by name/address. Pasting `lat, lng` directly always works.

**Pin is on a gate or next building:**
- Kakao POI pins can sit at an entrance. Pick a different match, or paste a corrected `lat, lng`.

---

## At scale

For thousands of rows, a browser tool is the wrong shape. Use a **Kakao REST key** in a script to
batch-geocode a spreadsheet of addresses to WGS84 + Google links in one pass. Ask and I'll write it.
