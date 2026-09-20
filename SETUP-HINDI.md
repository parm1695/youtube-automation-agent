# AgentTube — Hinglish Quick Start (apne PC pe)

Yeh guide sirf woh batati hai jo **aapko** karna hai. Baaki sab (dependencies,
folders, database, `.env`) walkthrough khud sambhal leta hai.

> Zaroori: Google login (OAuth) browser ko `localhost` pe wapas bhejta hai, isliye
> yeh setup **aapke apne computer** pe karna hota hai (Windows / Mac / Linux).

---

## 1. Ek baar install (5 min)

Pehle [Node.js 20+ LTS](https://nodejs.org) aur [Git](https://git-scm.com) install karo. Phir terminal (Windows: PowerShell) mein:

```bash
git clone https://github.com/parm1695/youtube-automation-agent.git
cd youtube-automation-agent
npm install
npx playwright install chromium
```

- `npm install` FFmpeg bhi apne aap download kar leta hai (`ffmpeg-static`).
- `npx playwright install chromium` **zaroori hai** — free "slideshow" video isi se render hota hai.
  (Yeh README mein nahi likha; iske bina pehla video fail hota hai.)

## 2. Keys taiyaar rakho (10 min)

### (a) Gemini API key — FREE
1. https://aistudio.google.com/apikey kholo, Google account se login karo
2. **Create API key** → key copy karo (`AIza...` se shuru hoti hai)

### (b) YouTube OAuth Client ID + Secret — FREE
https://console.cloud.google.com pe:
1. Upar **New project** → koi bhi naam → Create
2. **APIs & Services → Library** → search karke **Enable** karo:
   - **YouTube Data API v3** (upload ke liye)
   - **YouTube Analytics API** (views/retention analytics ke liye)
3. **APIs & Services → OAuth consent screen** → **External** → App name, support email,
   developer email bharo → Save → **Test users** mein **apna hi Gmail** add karo
4. **APIs & Services → Credentials → Create credentials → OAuth client ID**
   → Application type: **Desktop app** → Create
5. **Client ID** aur **Client Secret** copy kar lo

## 3. Walkthrough chalao (10 min) — yahin keys paste hongi

```bash
npm run walkthrough
```

| Step | Kya karna hai |
| --- | --- |
| 1. System check | Kuch nahi — sab ✓ hona chahiye (Node, FFmpeg, Chromium) |
| 2. AI provider | **Google Gemini** chuno → Gemini key paste karo → default model rehne do |
| 3. Video provider | **Local slideshow** chuno (free). Paid AI video baad mein add kar sakte ho |
| 4. YouTube | **"I already have a Client ID and Client Secret"** → dono paste karo → browser khulega → apne Gmail se login → **"Google hasn't verified this app" aaye to Continue** → Allow |
| 5. Channel basics | Channel ka naam, posting frequency, audience ek line mein |
| 6. Summary | Sab ✓ dikhna chahiye |

Har step skip ho sakta hai; progress save rehta hai. Dobara: `npm run walkthrough`.

Keys yahan save hoti hain (git mein kabhi nahi jaati): `config/credentials.json`, `config/tokens.json`, `.env`

## 4. Start karo

```bash
npm start
```

Browser mein http://localhost:3456 kholo.

## 5. Pehla video (dashboard mein)

1. **Production readiness → Run verified check** — keys, YouTube access, FFmpeg sab live test hota hai
   (koi video upload nahi hota). Paid image/video probe wale checkbox **off** rehne do.
2. Upar **＋ Create video** dabao → topic do → script → narration → slideshow video banta hai
   (`data/videos/` mein save hota hai)
3. **Review Studio** mein video dekho → factual review + media-rights confirm → **Approve**
4. Approved video **private** upload hota hai (`.env` mein `DEFAULT_PRIVACY_STATUS=private`).
   Jab bharosa ho jaye tab `public` karo.
5. Auto mode ke liye **Autonomous operator** mein objective, audience, pillars, cadence set karo → **Activate & run now**

Kuch bhi bina aapki approval ke publish **nahi** hota.

## 6. Common problems

| Problem | Fix |
| --- | --- |
| "Google hasn't verified this app" | Normal hai (app aapka apna project hai) → **Advanced → Continue** |
| "Access blocked: app not in testing / user not allowed" | Consent screen ke **Test users** mein apna Gmail add karo |
| Video generate karte waqt `Executable doesn't exist` / chromium error | `npx playwright install chromium` |
| `FFmpeg not found` | `npm install` dobara, ya Windows: `winget install Gyan.FFmpeg` (terminal restart) |
| Port 3456 busy | `.env` mein `PORT=3457` |
| Analytics tab mein "API not enabled" | Google Cloud mein **YouTube Analytics API** enable karo |
| Free Gemini limit hit | Thodi der ruko, ya `.env` mein OpenAI/OpenRouter key add karo |

## Kharcha

Gemini free tier + local slideshow = **₹0**. Paisa sirf tab lagega jab aap OpenAI, ElevenLabs,
ya AI-video providers (Seedance/MiniMax/Kling/Wan) enable karoge.
