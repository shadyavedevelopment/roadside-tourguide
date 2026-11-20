# Roadside Tourguide Lambda backend

This function keeps the OpenAI API key on AWS and offers two operations: concise landmark narration and speech audio. It uses Node.js built-in `fetch`; no npm packages are needed.

## Create the Lambda

1. In AWS Console, choose **Lambda → Create function → Author from scratch**.
2. Name it `roadside-tourguide-api`, choose **Node.js 26.x (or the current managed Node.js runtime)**, and create a basic execution role.
3. In **Code**, use **Upload from → .zip file** and upload `roadside-tourguide-lambda.zip` from this folder. Set **Runtime settings → Handler** to `index.handler`.
4. In **Configuration → General configuration**, set memory to 256 MB and timeout to 30 seconds. Set reserved concurrency to 2 for a small test group.
5. In **Configuration → Environment variables**, add:
   - `OPENAI_API_KEY`: the OpenAI API key for the project. Enter it only in the AWS console; never add it to this repository.
   - `APP_ACCESS_CODE`: a long random code to share privately with the testers.
   - `ALLOWED_ORIGINS`: `https://shadyavedevelopment.github.io,http://localhost:8000`
6. In **Configuration → Function URL**, create a function URL with **Auth type: NONE**. Configure CORS to allow only `https://shadyavedevelopment.github.io` (add `http://localhost:8000` while testing locally), method `POST`, and headers `content-type` and `x-tourguide-access-code`. Do not enable credentials.
7. Keep the Function URL for the app connection step.

The app must send `POST` JSON with an `action` of `narration` or `speech` and the `x-tourguide-access-code` header. Browser-origin checks and the shared tester code are suitable for a small invited pilot, but they are not a substitute for user authentication in a public launch. Set usage limits on the OpenAI project and an AWS cost budget before sharing the endpoint. AWS budget alerts can arrive after usage has occurred.

## Request examples

Narration:

```json
{
  "action": "narration",
  "title": "Example landmark",
  "distanceMeters": 420,
  "relativeDir": "just ahead",
  "selectedCategories": ["Historic buildings & districts"],
  "storyPacing": "",
  "wikiExtract": "Verified source text about the landmark."
}
```

Speech:

```json
{
  "action": "speech",
  "voice": "nova",
  "text": "A concise narration about the landmark."
}
```
