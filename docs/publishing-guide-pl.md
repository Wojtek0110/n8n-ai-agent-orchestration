# Jak opublikować repo i wykorzystać je w portfolio

## Proponowana nazwa repozytorium

`n8n-ai-agent-orchestration`

**GitHub description (wklej do About):**

> Guardrailed AI coding-agent orchestration with n8n: state-aware task execution, quota checks, automated validation, monitoring, and human approval.

**GitHub topics:** `n8n`, `ai-agents`, `workflow-automation`, `javascript`, `api-integration`, `ai-automation`, `observability`, `human-in-the-loop`, `codex`

## Publikacja

1. Na GitHubie wybierz **New repository** → nazwa `n8n-ai-agent-orchestration` → **Public**. Nie dodawaj automatycznie README, żeby uniknąć konfliktu przy pierwszym pushu.
2. Rozpakuj dostarczone archiwum ZIP do nowego, osobnego katalogu na dysku. **Nie** umieszczaj go jako podfolder istniejącego repo gry.
3. Otwórz terminal w folderze z `README.md` i wykonaj:

   ```bash
   git init
   git branch -M main
   git add .
   git commit -m "docs: publish AI agent orchestration portfolio case study"
   git remote add origin https://github.com/TWOJ_LOGIN/n8n-ai-agent-orchestration.git
   git push -u origin main
   ```

4. Wejdź w ustawienia repozytorium → **About**: wklej opis, dodaj topics i, opcjonalnie, link do właściwego projektu Deckdrive.
5. Dodaj własne zrzuty ekranu n8n z ukrytymi adresami/poświadczeniami do `assets/`, a następnie umieść je na początku README, np. `![Task orchestrator](assets/orchestrator.png)`.
6. Przypnij repo w **GitHub profile → Customize your pins**. Zachowaj istniejące repo gry jako osobny projekt pokazujący rezultat tej automatyzacji.

**Uwaga:** JSON-y w `workflows/` to zabezpieczone eksponaty. Nie uruchamiaj ich jako nowego TASK-a; historyczny task został zakończony.

## Gotowy tekst do CV (EN)

> Designed an n8n-based AI coding-agent orchestration workflow integrating a custom HTTP Worker and Codex, with state-driven task progression, guarded execution, quota checks, automated test gates, read-only monitoring, and SMTP incident alerts.

> Built human-in-the-loop safeguards for multi-stage AI-assisted development, including safe preview checks, explicit recovery states, bounded Git worktree modifications, and separate final human approval.

## Co powiedzieć na rozmowie

> This wasn't a chatbot wrapper or a model-training pipeline. I used n8n as a control plane for an AI coding agent. The challenging part was not calling the model, but managing state, permissions, validation, quota exhaustion, and recovery in a multi-step workflow. The Worker owns the authoritative state, and humans retain approval and Git integration decisions.

## Jakie trzy screenshoty mają największy sens

- **Orchestrator canvas:** cały przebieg i widoczny podział na preflight, task decision, quota guard, Worker, notifications.
- **LIVE Monitor canvas:** pętla GET → status normalization → IF → Wait 15 s, bez ujawniania odpowiedzi z prywatnego API.
- **Status examples:** samodzielnie przygotowane, **jawnie oznaczone dane syntetyczne** (np. `QUOTA_PAUSED`, `READY_FOR_REVIEW`) lub zanonimizowany autentyczny zrzut z logów.

Najmocniejszy przekaz dla rekrutera: **problem → zaprojektowane zabezpieczenia → architektura → dowód działania → granice projektu**. Nie dopisuj liczbowych oszczędności czasu, procentowych wskaźników jakości ani zapewnień o niezawodności bez pomiarów.
