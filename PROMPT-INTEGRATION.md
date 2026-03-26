# Prompt: Anti AI Slop Editor Seite in pfisterer.digital integrieren

Kopiere diesen Prompt in eine neue Claude Code Session im Projekt `E:\Projekt\pfisterer.digital\pfisterer-agency`:

---

## Prompt Start

Ich möchte eine neue Unterseite unter `pfisterer.digital/anti-ai-slop-editor` erstellen. Die Seite bewirbt ein kostenloses Open-Source-Tool (Claude Code Skill + Agent), das KI-generierten Text erkennt und umschreibt.

### Quell-Datei

Die fertige Landing Page liegt hier:
`E:\Projekt\pfisterer.digital\skill anti ai\index.html`

### Aufgabe

1. **Lies zuerst die index.html** und verstehe den Inhalt (Hero, Features, Before/After Beispiele, How it Works, Install-Anleitung, Use Cases, FAQ, CTA).

2. **Lies das Pfisterer CI Brandbook** unter `E:\Projekt\pfisterer.digital\Pfisterer-CI\docs\brandbook.md` und die Farb-Tokens unter `E:\Projekt\pfisterer.digital\Pfisterer-CI\tokens\colors.json`.

3. **Lies das bestehende Hugo-Layout** (`layouts/_default/baseof.html`, `layouts/partials/header.html`, `layouts/partials/footer.html`) um die bestehende Seitenstruktur zu verstehen.

4. **Erstelle die neue Seite als Hugo-Content-Page:**
   - Erstelle `content/anti-ai-slop-editor.md` mit dem passenden Hugo Frontmatter
   - Erstelle ein eigenes Layout `layouts/_default/anti-ai-slop-editor.html` (oder nutze ein passendes bestehendes Layout)
   - Die Seite soll eigenständig sein (Landing Page Charakter), aber Header/Footer/Navigation von pfisterer.digital übernehmen

5. **Design auf Pfisterer CI umstellen:**
   - Hauptfarbe: `#DC2626` (Rot) ersetzen durch `#00c3cd` (Pfisterer Teal)
   - Hover: `#991B1B` ersetzen durch `#009aa3` (Teal Dark)
   - Light-Accent: `#EF4444` / `#F87171` ersetzen durch `#00d9e4` (Teal Light)
   - Hintergrund: `#0A0A0A` durch `#070a0f` (Page)
   - Card-Background: `#141414` durch `#131920` (Surface)
   - Card-Hover: `#1A1A1A` durch `#1a2230` (Surface Hover)
   - Text: `#E5E5E5` durch `#e6edf3` (Text Primary)
   - Text-Dim: `#A3A3A3` durch `#8b949e` (Text Secondary)
   - Border: `#262626` durch `rgba(255,255,255,0.06)`
   - Grün (After-Beispiele): `#22C55E` durch `#3fb950` (Success)
   - Font bleibt Inter + JetBrains Mono (passt bereits zur CI)
   - Before-Beispiele: Rot-Töne beibehalten (semantisch = Error = `#f85149`)

6. **Inhalt bleibt 1:1** -- nur das Design/Farben ändern, kein Text umschreiben.

7. **Verlinke auf das GitHub-Repo** `https://github.com/Kendo1988/anti-ai-slop-editor` (alle Links in der Quell-HTML zeigen bereits dorthin).

8. **Teste** dass die Seite mit `hugo server` korrekt rendert und unter `/anti-ai-slop-editor` erreichbar ist.

### Wichtig
- Die Seite soll responsive sein (ist sie bereits im Quell-HTML)
- Nutze die bestehenden CSS Custom Properties der Pfisterer CI wo möglich
- Behalte die FAQ-Accordion und Tab-Funktionalität (JavaScript am Ende der Quell-HTML)
- Wenn das Hugo-Theme bereits eine eigene CSS-Datei hat, integriere die Seiten-Styles dort oder als scoped CSS

## Prompt Ende
