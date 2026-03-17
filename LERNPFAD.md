# Git Kollaboration – Lernpfad

## Das Szenario

Du bist neu in einem Team, das eine gemeinsame Rezept-Sammlung auf GitHub pflegt.
Deine Kollegin **Anna** und dein Kollege **Ben** arbeiten parallel an denselben Dateien.

Dieses Dokument führt dich durch 4 reale Situationen, die in jedem Team vorkommen.

---

## Lektion 1: Remote-Änderungen holen (fetch vs. pull)

**Situation:** Anna hat heute Morgen Änderungen gepusht. Du willst wissen, was sie gemacht hat, bevor du anfängst.

```bash
# Schritt 1: Remote-Änderungen herunterladen (noch NICHT mergen)
git fetch origin

# Schritt 2: Vergleiche deinen Stand mit dem Remote
git log HEAD..origin/master --oneline
# Zeigt alle Commits, die auf dem Remote sind, aber noch nicht bei dir

# Schritt 3: Unterschiede anschauen
git diff HEAD origin/master

# Schritt 4: Erst jetzt mergen (wenn du zufrieden bist)
git merge origin/master
```

> TIPP: `git pull` macht fetch + merge in einem Schritt.
> Aber fetch zuerst gibt dir die Kontrolle!

---

## Lektion 2: Feature-Branch erstellen und pushen

**Situation:** Du sollst ein neues Rezept hinzufügen, ohne den main-Branch zu stören.

```bash
# Schritt 1: Neuen Branch erstellen UND direkt wechseln
git checkout -b feat/mein-rezept

# Schritt 2: Datei erstellen/bearbeiten
echo "# Mein Rezept" > rezepte/mein-rezept.md

# Schritt 3: Stagen und committen
git add rezepte/mein-rezept.md
git commit -m "feat: neues Rezept hinzugefügt"

# Schritt 4: Branch zum Remote pushen (-u setzt das Tracking)
git push -u origin feat/mein-rezept

# Ab jetzt reicht einfach: git push
```

> WARUM Branches? Deine Arbeit ist isoliert. Niemand wird durch
> deine halbfertigen Änderungen gestört. Du kannst in Ruhe arbeiten.

---

## Lektion 3: Merge-Konflikt lösen

**Situation:** Du und Ben haben beide die Zutatenliste in `rezepte/pasta.md`
gleichzeitig bearbeitet. Beim Mergen gibt es einen Konflikt.

```bash
# Git zeigt dir den Konflikt so:
# <<<<<<< HEAD          ← deine Version
# 200g Pasta
# =======              ← Trennlinie
# 250g Pasta           ← Bens Version
# >>>>>>> origin/master

# Lösung:
# 1. Datei öffnen und manuell entscheiden
# 2. Die <<<, ===, >>> Zeilen entfernen
# 3. Den richtigen Inhalt behalten
# 4. git add <datei>
# 5. git commit
```

> Konflikte sind NORMAL! Sie bedeuten nur: "Zwei Personen haben
> dieselbe Stelle bearbeitet – wer hat Recht?" Das Team entscheidet.

---

## Lektion 4: Den Stand eines Kollegen reviewen

**Situation:** Ben bittet dich, seinen Branch anzuschauen, bevor er einen
Pull Request erstellt.

```bash
# Bens Branch lokal verfügbar machen
git fetch origin
git checkout feat/bens-branch

# Jetzt kannst du seinen Code lokal ausprobieren!
# Um zu deinem Branch zurückzukehren:
git checkout feat/mein-rezept
```

---

## Übersicht: Die wichtigsten Befehle

| Befehl                          | Was passiert                              |
|---------------------------------|-------------------------------------------|
| `git clone <url>`               | Remote-Repo komplett herunterladen        |
| `git fetch origin`              | Remote-Änderungen holen (nicht mergen)    |
| `git pull origin main`          | Fetch + Merge in einem Schritt            |
| `git checkout -b feat/name`     | Neuen Branch erstellen und wechseln       |
| `git push -u origin feat/name`  | Branch zum Remote pushen + Tracking setzen|
| `git merge feat/name`           | Branch in aktuellen Branch mergen         |
| `git log --oneline --graph`     | Commit-History als Graph anzeigen         |
| `git diff HEAD origin/main`     | Unterschiede zum Remote anzeigen          |
