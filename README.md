# Roadside Tourguide

A personal audio tour that reads out nearby historic landmarks as you travel.

The tour lets listeners choose the kinds of places they want to hear about. Its default search range adapts to movement speed: close range on foot, a focused neighborhood range on local roads, and a wider area at highway speeds. It selects one well-documented landmark at a time and keeps stories concise, allowing a longer narration only when a site has enough substance to merit it.

## Try it locally

Serve this folder from `localhost` (service workers do not run from `file://` URLs), then open the local address in a browser. For example, with Python installed, run `python -m http.server 8000` from this folder and visit `http://localhost:8000`.

## GitHub Pages

This is a static site. Publish the repository's root folder with GitHub Pages. The deployed site will be available at the Pages URL shown in the repository's **Settings → Pages**.

The app shell can load offline after its first successful visit. Live Wikipedia lookups, geocoding, and OpenAI features require their respective network access. The optional OpenAI key is stored in the browser and should not be committed to the repository.
