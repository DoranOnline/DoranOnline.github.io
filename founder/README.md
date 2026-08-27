# Founder / team photos

**Do not put these in `public/team/`.** `/team/:path*` is the auth-gated team
portal (see the matcher in `middleware.ts`), so anything served from that folder
answers `307 → /login` and the image silently never loads. The `next/image`
optimizer then returns `400 The requested resource isn't a valid image`, which
looks like a broken file rather than a routing collision. This folder is outside
the matcher and serves normally.

| Person | Filename       |
| ------ | -------------- |
| Doran  | `doran.webp`   |
| Gal    | `gal.webp`     |
| Adi    | `adi.webp`     |
| Noa    | `noa.webp`     |

Guidance:
- Portrait orientation, roughly 4:5 (1000×1250), face centred toward the top.
- Any background works — surfaces render them grayscale and warm to full colour
  on hover, so casual phone photos still sit inside the ink/ember palette.
- WebP, quality ~82, under ~120KB. Convert with:
  `node -e "require('sharp')('in.png').resize(1000,1250,{fit:'cover',position:'top'}).webp({quality:82}).toFile('out.webp')"`

After adding a file, set the matching `photo` path in the `TEAM` array in
`app/(marketing)/our-team/page.tsx`.
