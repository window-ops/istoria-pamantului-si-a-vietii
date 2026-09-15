# Verificarea avizului

Avizul de pe pagina „Fișa manualului” este semnat cu o cheie ed25519. Cheia este a autorului; el a făcut-o și el o ține. Semnătura arată că textul din `aviz.txt` a fost semnat de cine are cheia privată, adică de autor, și nu arată nimic altceva.

Fișierele din acest folder:

- `aviz.txt`: textul semnat;
- `publica.pem`: cheia publică, ed25519;
- `aviz.sig`: semnătura, în format binar.

Verificarea, cu OpenSSL 3, dintr-un terminal deschis în acest folder:

```
openssl pkeyutl -verify -pubin -inkey publica.pem -rawin -in aviz.txt -sigfile aviz.sig
```

Răspunsul așteptat este `Signature Verified Successfully`. Orice modificare a textului din `aviz.txt`, fie și o literă, face verificarea să eșueze.

Amprenta cheii publice (SHA-256 peste forma DER):

```
fcd80bb168becb9f76a5bc7a8bf38e8f66ef889857e56f09937c16a7f1ad4fd1
```

Cheia privată nu este în depozit: a fost ștearsă după semnare, la 15 septembrie 2026. Semnătura rămâne valabilă. Pentru un aviz nou se face o cheie nouă, după pagina „Cum se semnează avizul” din ghid.

Avizul numărul 6 înlocuiește avizul numărul 4, dat ediției din 2025. Avizul este semnătura autorului pe propria lucrare și nu provine de la o autoritate publică.
