Testing [Astro x KeyStatic](https://maciekpalmowski.dev/blog/keystatic-x-astro/) with the [forked theme](#mizar)

Further description at `keystatic.md`

Setup:

```sh
#git clone https://github.com/JAlcocerT/mizar
#git clone https://github.com/majesticooss/mizar
npm install

npm run dev --host #as i was using the Opi
npm run build
#npm install -g serve #serve with npm
#serve -s dist #http://localhost:3000
npx serve -s dist #http://localhost:3000
```

You will see the regular `localhost:4321` to explore the theme

> But also: `http://127.0.0.1:4321/keystatic/` is available.

```sh
npm run build
npx serve -s dist #http://localhost:3000 keystatic wont be available, just the built files
```

> > Forked from [majesticooss](https://github.com/majesticooss/mizar)

---

# [Mizar](https://mizar.majestico.co)

<a href="https://astro.build/">![Astro](.github/images/astro-icon.png)</a>
<a href="https://tailwindcss.com/">![Tailwind](.github/images/tailwind-icon.png)</a>
<a href="https://alpinejs.dev/">![Alpine js](.github/images/alpine-icon.png)</a>

Mizar is a template made with [Astro](https://astro.build), [Tailwind](https://tailwindcss.com/) and [AlpineJS](https://alpinejs.dev/).

This project was strongly inspired by a template found on Webflow which I can longer find, if you are the author please let me know so I can give you the credits.

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/majesticooss/mizar)

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/majesticooss/mizar)

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/majesticooss/mizar)


### [🧪 Site preview →](https://mizar.majestico.co)

### [🧑‍🚀 Astro website →](https://astro.build/)

### [🕮 Astro docs →](https://docs.astro.build/en/getting-started/)

---

## Preview

![Astros Preview](.github/images/screenshot.png)

## 🧪 Test

On the folder run

1. `bun install`  <small>(or `yarn` or `pnpm i`)</small>
2. `bun run dev`  <small>(or `yarn dev` or `pnpm dev`)</small>

## ✅ Features

- [x] Localization
- [x] Blog
- [x] CMS for editing blog post (thanks to Keystatic)
- [x] PWA (thanks to vite-pwa)

## ✍️ Admin dashboard

You can access the admin dashboard for editing blog post at `/keystatic`

For more information follow Keystatic documentation at [https://keystatic.com/docs/introduction](https://keystatic.com/docs/introduction)


---

<p align="right"><a href="https://majestico.co" target="_blank">majestico.co</p>
