# Fejlesztői Útmutató - CompanyLandingPage

## 🚀 Első Lépések

### 1. Repo Clone

```bash
git clone https://github.com/PDominikHU/CompanyLandingPage.git
cd CompanyLandingPage
```

### 2. Függőségek Telepítése

```bash
npm install
```

### 3. Dev Szerver Indítása

```bash
npm run dev
```

**Nyelvek tesztelése:**

- Magyar: http://localhost:5173/hu
- Angol: http://localhost:5173/en

---

## 📋 Workflow - Hogyan Dolgozz?

### 1. Válassz egy Issue-t (GitHub Projects Board)

- **Todo** oszlopból válassz egy taskot
- **Assign yourself** (rendeld magadhoz)
- Mozgasd **In Progress** oszlopba

### 2. Friss Main Branch Lehúzása

```bash
# Mindig friss main-ről indulj!
git checkout main
git pull origin main
```

### 3. Új Feature Branch Készítése

```bash
# Névadás: feature/mit-csinalok
git checkout -b feature/hero-section
# vagy
git checkout -b feature/footer
# vagy
git checkout -b feature/contact-form
```

### 4. Kódolás

**Lokálisan tesztelj:**

```bash
npm run dev
```

### 5. Ellenőrzés Commit Előtt (fontos!)

```bash
# ESLint ellenőrzés
npm run lint

# TypeScript ellenőrzés
npm run check

# Build teszt (fordul-e?)
npm run build
```

**Ha hibát ír → javítsd!**

### 6. Commit

```bash
git add .
git commit -m "Add hero section with gradient background"
```

**Jó commit üzenetek:**

- "Add hero section"
- "Fix: responsive layout on mobile"
- "Update footer links"

**Rossz commit üzenetek:**

- "fix"
- "asdf"
- "changes"

### 7. Push a Saját Branch-edre

```bash
git push origin feature/hero-section
```

### 8. Pull Request (PR) Nyitása GitHub-on

2. **Pull requests** tab
3. **New pull request** gomb
4. **Compare:** `feature/hero-section`
5. **Create pull request**

**PR Leírás Template:**

```markdown
## Changes

- Hero section komponens létrehozása
- Gradient background
- Responsive design
  Closes #1
```

**Reviewers:** Add hozzá a társaidat!

### 9. Várd Meg a GitHub Actions Ellenőrzést

**Automatikusan fut:**

```
⏳ quality / Build test
⏳ quality / Type check
⏳ quality / Lint check
```

**Ha ❌ piros X:**

- Kattints rá → nézd meg mi a hiba
- Javítsd lokálisan
- Commit + push → újra fut automatikusan

**Ha ✅ zöld pipa:**

- Várj code review-ra (társad megnézi)

### 10. Code Review + Merge

**Társad review-olja:**

- Approve ✅ → Merge-elheted
- Request changes ❌ → Javítsd, majd push

**Merge:**

- **Squash and merge** (ajánlott)
- **Confirm merge**
- **Delete branch**

### 11. Cloudflare Automatikusan Deploy-ol!

**1-2 perc múlva élesen is látszik:**
https://companylandingpage.pages.dev

---

## 🔧 Hasznos Parancsok

```bash
# Dev szerver
npm run dev              # Alapértelmezett
npm run dev -- --open    # Auto nyit böngészőt

# Ellenőrzés
npm run lint             # ESLint
npm run check            # TypeScript
npm run build            # Production build teszt
npm run preview          # Production preview lokálisan

# Git
git status               # Mi változott?
git checkout main        # Main branch-re váltás
git pull origin main     # Friss main lehúzása
git branch               # Melyik branch-en vagy?
git branch -d feature/xyz # Branch törlése (merge után)
```

---

## 🌍 Többnyelvűség (Paraglide)

### Fordítás Hozzáadása

**1. Szerkeszd a fordítás fájlokat:**

`messages/hu.json`:

```json
{
	"hero_title": "Modern webes megoldások",
	"hero_cta": "Ajánlatot kérek"
}
```

`messages/en.json`:

```json
{
	"hero_title": "Modern web solutions",
	"hero_cta": "Get a quote"
}
```

**2. Használd a komponensben:**

```svelte
<script>
	import * as m from '$lib/paraglide/messages';
</script>

<h1>{m.hero_title()}</h1>
<button>{m.hero_cta()}</button>
```

---

## 🎨 Design Guidelines (később frissítjük)

- **Színvilág:** TBD (később döntünk)
- **Fontok:** TBD
- **Spacing:** Tailwind default (4, 8, 16, 32, 64px)

---

## ✅ Checklist Minden Feature-hez

- [ ] Issue kiválasztva és assigned
- [ ] Friss main lehúzva (`git pull origin main`)
- [ ] Feature branch létrehozva
- [ ] Kód megírva
- [ ] Lokálisan tesztelve (`npm run dev`)
- [ ] Lint + Type check OK (`npm run lint`, `npm run check`)
- [ ] Commit üzenet értelmes
- [ ] Push
- [ ] PR nyitva
- [ ] GitHub Actions ✅
- [ ] Code review kérve
- [ ] Merge után branch törölve

---
