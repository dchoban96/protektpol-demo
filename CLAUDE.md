# Protektpol — demo redesign sito

Demo one-page (russo) del redesign di https://protektpol.ru/ e https://протектпол.рф/ — impresa di Krasnodar/Belorechensk (dal 2011) che posa e ripara pavimenti polimerici e industriali, leviga/lucida calcestruzzo, fa decorativi effetto marmo e impermeabilizzazioni.

## File
- `index.html` — tutto il sito in un file: CSS, JS, shader WebGL. Nessuna dipendenza oltre a Google Fonts (Unbounded + Manrope).
- Servire con `python -m http.server 8080` (non aprire via file://).

## Struttura della pagina (ordine)
header sticky → hero (marmo bianco-nero) → barra numeri → servizi (9 card) → settori → calcolatore → perché noi → processo 5 passi → decorativi (marmo bianco-marrone + 3 campioni) → objetti prima/dopo → prezzi (tabella a scaglioni) → FAQ → contatti (marmo "слюда") + form → footer → pulsanti flottanti WA/TG.

## Marmi liquidi
Shader in `<script>` (sezione "Liquid marble"): fbm + domain warping, un canvas per ogni `[data-liquid]` (`whiteblack`, `whitebrown`, `mica`), palette in `PAL`, scala in `data-scale`. Resa a metà risoluzione, si ferma fuori viewport, statico con prefers-reduced-motion.

## Calcolatore
Logica in "Calculator": scaglioni 0–50 / 51–199 / 200–499 / 500–1499 / 1500+ m² presi dal listino reale del sito (senza IVA, betone M300). Chiavi in mano polimerico: 1600 ₽/m² ≤50 m² → 899 ₽/m² ≥700 m² (interpolazione lineare). I prezzi "materiale (ориентир)" per quarzo/cemento e i decorativi sono stime da confermare col cliente.
- La tabella prezzi segue riga per riga https://protektpol.ru/cenyi/pokryitiya.php (verificata il 28/10/2026), incluse le note "без материала". Città servite secondo quella pagina: Краснодар, Сочи, Новороссийск, Армавир, Майкоп, Ростов-на-Дону, Ставрополь, Крым.
- Gli sconti nei box sotto il prezzario (`data-disc`) sono calcolati da `turnkey()`, così non contraddicono il calcolatore. Se il cliente conferma sconti diversi (es. −15 % da 200 m²), va cambiata la curva, non il box.
- WhatsApp riceve il preventivo già scritto (`?text=`); Telegram non lo supporta, quindi il testo viene copiato negli appunti; "Получить смету" lo inserisce nel form.

## Dati azienda confermati
- Tel. +7 (918) 682-91-87 (altro numero visto sul sito mobile: +7 (918) 188-96-39 — da chiarire)
- info@protektpol.ru
- Краснодар, ул. Зиповская, 37 · Белореченск, ул. Комсомольская, 199/1
- Promesse già dichiarate dal cliente: бесплатная диагностика, гарантия на отрыв от основания, работаем с НДС
- Video lavori: https://dzen.ru/id/62abf0e9078622570760d9ca?tab=longs

## Segnaposto da sostituire
- Foto reali nei "prima/dopo" (ora texture CSS) e nelle card servizi (ora canvas 2D)
- Nomi/m²/tempi dei 3 oggetti in portfolio (inventati come esempio)
- ИНН/ОГРН e ragione sociale nel footer, orari di apertura
- Link reali a Политика e Согласие (152-ФЗ): i due checkbox devono restare separati
- Invio del form (ora solo demo: preventDefault + messaggio)

## Convenzioni
- Testi utente in russo; commenti e commit in italiano
- Palette: grafite #17191D/#1F2328, accento giallo segnaletica #FFC21A; tema chiaro/scuro via token CSS in `:root`
- Mantenere il sito in un solo file finché il cliente non approva la demo
