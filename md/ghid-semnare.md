# Cum se semnează avizul

## 1. Ce este semnat

Se semnează textul din fișierul `aviz.txt`, care cuprinde numele lucrării, numele celui care avizează, numărul avizului, data și licența. Semnătura arată că textul a fost semnat de cine deține cheia privată și nu arată nimic altceva.

## 2. Ce trebuie instalat

OpenSSL 3, dintr-un terminal.

## 3. Cheia

```
openssl genpkey -algorithm ed25519 -out privata.pem
openssl pkey -in privata.pem -pubout -out publica.pem
```

Cheia privată rămâne la autor. Cheia publică intră în depozit.

## 4. Semnătura

```
openssl pkeyutl -sign -inkey privata.pem -rawin -in aviz.txt -out aviz.sig
```

Verificarea, pe care o poate face oricine:

```
openssl pkeyutl -verify -pubin -inkey publica.pem -rawin -in aviz.txt -sigfile aviz.sig
```

Răspunsul așteptat este `Signature Verified Successfully`. Orice modificare a textului semnat, fie și o literă, face verificarea să eșueze.

## 5. Ce se pune în pagină

Pe fișa manualului se trec numărul avizului, data, licența și amprenta cheii publice, obținută cu:

```
openssl pkey -pubin -in publica.pem -outform DER | openssl dgst -sha256
```

## 6. Arhiva

În folderul `cheie` rămân textul semnat, cheia publică, semnătura și pagina de verificare. Cheia privată se șterge după semnare, iar pentru un aviz nou se face o cheie nouă.

## 7. Ce înseamnă avizul

Avizul este o semnătură a autorului pe propria lucrare. El nu vine de la o autoritate publică și nu ține locul unei aprobări oficiale.
