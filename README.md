# Interactive Birthday Gift — GitHub Pages

## Folder structure

```text
birthday-gift-site/
├─ index.html
└─ assets/
   ├─ letter-card.png
   ├─ memory-01.jpg
   ├─ memory-02.jpg
   ├─ memory-03.jpg
   ├─ memory-04.jpg
   ├─ memory-05.jpg
   └─ memory-06.jpg
```

## 1. Set the password

Open `index.html` and find:

```js
PASSWORD_SHA256: "REPLACE_WITH_SHA256",
FIRST_MESSAGE_DATE: "2000-01-01",
```

Put the SHA-256 hash of your password in the first field, and the real first-message date in the second.

Example in browser DevTools:

```js
crypto.subtle.digest(
  "SHA-256",
  new TextEncoder().encode("your-password")
).then(buf =>
  console.log([...new Uint8Array(buf)].map(b=>b.toString(16).padStart(2,"0")).join(""))
)
```

## 2. Add your memories

Put your photos into `assets/` and update:

```js
MEMORIES: [
  { src:"assets/memory-01.jpg", caption:"..." },
  ...
]
```

The site automatically distributes them to both sides of the letter.

## 3. Replace the letter

The current site uses the uploaded card as:

```text
assets/letter-card.png
```

Replace that file with your final letter image, keeping the same filename.

## 4. Publish on GitHub Pages

1. Create a new GitHub repository.
2. Upload `index.html` and the whole `assets/` folder.
3. GitHub → Settings → Pages.
4. Source: **Deploy from a branch**.
5. Select `main` and `/root`.
6. Save.
7. GitHub will give you a public URL.

## Important security note

Because GitHub Pages is a static client-side website, this is a **cute access gate, not real security**. A technically experienced person can inspect the JavaScript and bypass the gate. The password is stored as SHA-256 to avoid putting the plaintext password directly in source code, but the check still happens in the browser.

For a personal birthday surprise, this is normally fine.
