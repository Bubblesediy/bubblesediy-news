# BubblesEdiy News

Next.js 14 (App Router) + TypeScript + Tailwind, exported as a fully static site (`output: "export"`), so it hosts free on Cloudflare Pages.

## Run locally
```
npm install
cp .env.example .env.local
npm run dev
```

## Add articles
Edit `data/articles.ts`. Replace the 10 DEMO entries with real ones and set `demo: false`. Only `demo:false` articles appear in `/news-sitemap.xml` and get `NewsArticle` JSON-LD (demo pages are `noindex`). Images go in `public/images/`. Rebuild/redeploy after changes.

## Editorial rules (read before publishing)
Do not copy other publishers. Do not fabricate events. Verify important claims. Label opinion. Use accurate dates. Credit sources. Correct errors publicly. No misleading headlines. Never publish AI-generated factual claims without human verification. Use properly licensed images. Keep author and publisher details accurate.

## Deploy free on Cloudflare Pages
1. Create a GitHub repo and push this folder (`git init && git add . && git commit -m init && git remote add origin <url> && git push -u origin main`). Do not commit `.env.local`.
2. Create a free account at cloudflare.com.
3. Workers & Pages → Create → Pages → Connect to Git → choose the repo.
4. Build settings: Framework preset **Next.js (Static HTML Export)**; Build command `npm run build`; Output directory `out`.
5. Environment variable: `NEXT_PUBLIC_SITE_URL=https://bubblesediy.pages.dev` (use your actual project URL; the name `bubblesediy` must be available).
6. Save and Deploy. Your free URL is `https://<project-name>.pages.dev`.
7. Check `/sitemap.xml`, `/news-sitemap.xml`, `/rss.xml`, `/robots.txt`.

## Custom domain later
`.com` domains are not free; buy one from any registrar (or Cloudflare Registrar). In Pages → your project → Custom domains → add it and follow the DNS steps. Then change the env variable to `NEXT_PUBLIC_SITE_URL=https://www.bubblesediy.com` and redeploy: canonicals, sitemaps, RSS, Open Graph and JSON-LD all update. Configure `contact@bubblesediy.com` email before launch.

## Google Search Console
Add a property (URL-prefix or Domain), verify (DNS TXT record or HTML tag), submit `/sitemap.xml`, use URL Inspection on key pages and Request Indexing. Indexing is not guaranteed.

## Google News
Google decides eligibility and visibility algorithmically. This site is technically ready (NewsArticle markup, news sitemap, author pages, policies, bylines, dates), but that guarantees neither inclusion nor traffic. Publish original, regular, accurate reporting with real author and publisher information.

## Switching to a CMS
All pages read through `lib/content.ts` and the `Article` type in `types/`. Replace the `ARTICLES` import with a fetch from Sanity, WordPress, Supabase, Firebase etc. (at build time), mapping fields to `Article`. UI components don't change. Use a Cloudflare deploy hook to rebuild on publish.

## Placeholders to replace
Contact email, social links, author bio, privacy/terms templates, ad slots (`Ad` in `components/Ui.tsx`), cookie banner (`SITE.cookiesEnabled` in `data/site.ts`, off because the site sets no cookies), newsletter and contact form (no backend connected).
