# 🔒 Documentazione Sicurezza - La Vera Pizzeria Landing Page

## Protezioni Implementate

### 1. **Content Security Policy (CSP)**
- **Scopo**: Previene attacchi XSS (Cross-Site Scripting) e injection
- **Implementazione**: 
  - Header HTTP: `Content-Security-Policy`
  - Meta tag HTML nel `<head>`
  - Configurazione Vercel: `vercel.json`
- **Dettagli**:
  - `default-src 'self'`: Carica solo risorse dal dominio stesso
  - `script-src`: Consente solo script da fonti attendibili (Tailwind, FontAwesome, Google Fonts)
  - `img-src`: Consente immagini da HTTPS, data URI, e blob
  - `frame-ancestors 'none'`: Blocca il sito da essere caricato in iframe (Clickjacking)

### 2. **Protezione da Clickjacking**
- **X-Frame-Options: DENY** - Impedisce che il sito sia caricato in un iframe
- **Frame Detection JavaScript** - Rileva se il sito è in un iframe e lo blocca

### 3. **MIME Type Sniffing Protection**
- **X-Content-Type-Options: nosniff** - Forza il browser a rispettare il Content-Type dichiarato
- Previene attacchi dove file pericolosi vengono mascherati

### 4. **XSS Protection**
- **X-XSS-Protection: 1; mode=block** - Abilita il filtro XSS del browser
- **Sanitizzazione Input JavaScript**:
  - Funzione `sanitizeInput()` che escapa caratteri pericolosi
  - Validazione su blur e keypress
  - Blocco di caratteri speciali: `< > { }`

### 5. **HTTPS Enforcement (HSTS)**
- **Strict-Transport-Security**: `max-age=31536000; includeSubDomains`
- Forza HTTPS per 1 anno
- Preload list per massima sicurezza

### 6. **Referrer Policy**
- **strict-origin-when-cross-origin**: Limita informazioni inviate a siti esterni
- Protegge la privacy dell'utente

### 7. **Permissions Policy**
- Disabilita accesso a:
  - Geolocalizzazione
  - Microfono
  - Fotocamera
  - Pagamenti
  - USB
  - Sensori (magnetometro, giroscopio, accelerometro)

### 8. **Rate Limiting Form**
- Cooldown di 3 secondi tra invii di form
- Previene spam e attacchi brute-force

### 9. **CORS Protection**
- Validazione fetch API
- Solo richieste HTTPS consentite
- Blocco di richieste insicure

### 10. **Protezione da SQL Injection (.htaccess)**
- Blocco pattern comuni di SQL injection
- Blocco di comandi pericolosi: UNION, SELECT, INSERT, DELETE, DROP, UPDATE

### 11. **Blocco File Sensibili**
- `.git`, `.env`, `.htaccess` non accessibili
- Blocco di directory listing

### 12. **Compressione GZIP**
- Riduce dimensione file trasferiti
- Migliora performance e sicurezza

### 13. **Cache Control**
- HTML: No-cache (sempre aggiornato)
- Assets statici: 1 anno di cache (performance)

### 14. **Blocco User Agent Malevoli**
- Blocco automatico di bot, crawler, scraper
- Riduce carico server da attacchi

## File di Configurazione

### `index.html`
- Meta tag CSP nel `<head>`
- JavaScript di protezione nel `<body>`
- Sanitizzazione input form
- Validazione form

### `.htaccess`
- Header di sicurezza Apache
- Rewrite rules per HTTPS
- Blocco SQL injection
- Blocco file sensibili
- Compressione GZIP

### `vercel.json`
- Header di sicurezza per Vercel
- Cache control
- Rewrite rules

## Best Practices Implementate

✅ **Validazione Input**
- Sanitizzazione di tutti gli input utente
- Blocco di caratteri pericolosi

✅ **Output Encoding**
- Uso di `textContent` invece di `innerHTML` dove possibile
- Escape di caratteri speciali

✅ **Protezione Sessione**
- Rate limiting su form submission
- Blocco di eval()

✅ **Logging & Monitoring**
- Console logging di errori
- Avvisi di attacchi bloccati

✅ **Dependency Management**
- Uso di CDN affidabili (Tailwind, FontAwesome, Google Fonts)
- Verifica di integrità dei file

## Raccomandazioni Aggiuntive

### Per Produzione:
1. **Certificato SSL/TLS**: Assicurati che il dominio abbia un certificato valido
2. **WAF (Web Application Firewall)**: Considera l'uso di Cloudflare o simile
3. **Backup Regolari**: Esegui backup del sito
4. **Monitoraggio**: Usa strumenti come Sentry per monitorare errori
5. **Aggiornamenti**: Mantieni le dipendenze aggiornate

### Per Vercel:
1. Abilita "Automatic HTTPS"
2. Configura "Environment Variables" per dati sensibili
3. Usa "Preview Deployments" per testare prima di pubblicare

### Per Apache (.htaccess):
1. Assicurati che `mod_rewrite` sia abilitato
2. Assicurati che `mod_headers` sia abilitato
3. Testa le regole in staging prima di produzione

## Testing di Sicurezza

Puoi testare la sicurezza del sito usando:

1. **OWASP ZAP**: https://www.zaproxy.org/
2. **Burp Suite Community**: https://portswigger.net/burp
3. **Mozilla Observatory**: https://observatory.mozilla.org/
4. **SSL Labs**: https://www.ssllabs.com/ssltest/

## Contatti & Supporto

Per segnalare vulnerabilità di sicurezza, contatta:
- Email: security@laveraphizzeria.it
- Telefono: +39 XXX XXX XXXX

**Non divulgare pubblicamente le vulnerabilità prima di contattarci!**

---

**Ultimo aggiornamento**: 28 Marzo 2026
**Versione**: 1.0
