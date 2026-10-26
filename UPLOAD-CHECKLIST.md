# GitHub release checklist

## 0. Before you start
- [ ] `gh auth login` (GitHub.com → HTTPS → browser)
- [ ] Confirm the public repo will contain ONLY release material, never `src/`

## 1. Create the public release repo
```powershell
cd D:\workspace\order-of-the-general\release-publish\github
git init
git add .
git commit -m "Order of the General 1.1.0 release page"
gh repo create order-of-the-general --public --source=. --remote=origin --push
```
If the repo name is taken, use another name and update the links in `README.md` and `index.html`.

## 2. Replace placeholders
Replace every `YOUR_GITHUB` in `README.md` and `index.html` with the GitHub account name.
```powershell
(Get-ChildItem README.md,index.html | ForEach-Object {
  (Get-Content $_.FullName -Raw).Replace('YOUR_GITHUB', 'YOUR_ACCOUNT') | Set-Content $_.FullName -Encoding UTF8
})
```

## 3. Create the GitHub Release
```powershell
gh release create v1.1.0 `
  "D:\workspace\order-of-the-general\game\release\desktop\Order of the General Setup 1.1.0.exe" `
  "D:\workspace\order-of-the-general\game\release\desktop\Order of the General 1.1.0.exe" `
  --repo YOUR_ACCOUNT/order-of-the-general `
  --title "Order of the General 1.1.0 — first formal release" `
  --notes-file RELEASE_NOTES-1.1.0.md
```

## 4. Turn on GitHub Pages
Repo → Settings → Pages → Build and deployment → Deploy from a branch → `main` / `/ (root)`.
The landing page is `index.html`.

## 5. Verify
- [ ] Release page shows both exe files
- [ ] `SHA256SUMS.txt` matches the files
- [ ] README and landing page download buttons work
- [ ] No `src/`, `.ts`, `package.json` or build files in the public repo
- [ ] Credits and licence are visible

## 6. Then post, in this order
1. GitHub / itch.io page
2. Bilibili 3-minute overview
3. Zhihu design post
4. NGA / Tieba / Xiaheihe battle report
5. IndieDB / ModDB entry
6. Reddit / BGG / Discord (after the first three are live)

Never upload the source tree, `.git` of the private repo, or the build pipeline to the public repo.
