# Comisia de Drumuri și Poduri — date publice

Arhiva și datele structurate din care se construiește monitorul activității legislative a
Comisiei pentru transporturi și infrastructură a Camerei Deputaților și a inițiativelor
deputaților USR. Totul provine din **surse publice**; nimic de aici nu e un document oficial —
pentru uz oficial, consultați pagina de pe cdep.ro din care provine fiecare înregistrare.

## Ce conține

| Director / fișier | Ce e |
|---|---|
| `raw/` | Paginile HTML și PDF-urile **exact cum au fost descărcate**, numite după hash-ul SHA-256 al conținutului. O pagină schimbată pe sursă apare ca fișier nou, lângă cel vechi. |
| `raw_pages.jsonl` | Pentru fiecare fișier din `raw/`: URL-ul sursă, data descărcării, hash-ul. |
| `markdown/` | Documentele PDF convertite în text. Cele obținute prin **OCR** au un antet care o spune: textul OCR e failibil și nu se citează ca text nativ. |
| `db/monitor-public.db` | Baza SQLite cu datele extrase (proiecte, inițiatori, parcurs, comisii, ședințe, parlamentari). Fiecare rând derivat are `source_url` și/sau `raw_page_id`, deci duce la fișierul din `raw/`. |
| `memorie/` | Fișe Markdown pe proiect/parlamentar/document/act/ședință, tăiate pe secțiuni — forma gata de indexat de [MemSearch](https://github.com/zilliztech/memsearch). Căutare semantică locală: `pip install "memsearch[onnx]"`, apoi indexează acest director cu propriul tău index; nu găzduim noi o căutare pe site. |

Cifre la ultimul export: `bill` 1262, `person` 1394, `committee_meeting` 590, `bill_document` 14275, `raw_page` 3382.

## Ce NU conține

Analizele generate de model (interpretarea AI a proiectelor), notele și pozițiile echipei,
conversațiile, identitățile și costurile apelurilor către model. Acelea sunt muncă privată și nu
ies din stația de lucru — inclusiv din `memorie/`, care duce doar tipurile derivate direct din
cdep.ro. Temele atribuite de model (`method = 'llm'`) sunt scoase din `bill_topic`.

## Surse

- **cdep.ro** — fișele proiectelor, componența comisiilor, ședințele și ordinea de zi, programul
  de lucru al Camerei, fișele deputaților și fotografiile lor.
- **legislatie.just.ro** — forma consolidată a unor acte normative. E o consolidare
  **neoficială**, conform termenilor portalului.

Câmpurile pe care sursa nu le afirmă sunt goale (`NULL`), cu motivul în `parse_issue` — nu sunt
completate prin deducție.
