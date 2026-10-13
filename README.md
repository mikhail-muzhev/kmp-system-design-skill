# kmp-system-design — Claude Code skill

Скилл для Claude Code: live-помощник на собеседовании по System Design мобильной фичи (Kotlin Multiplatform + Compose Multiplatform).

По короткой постановке ("сверстать ленту новостей") и скриншотам дизайна за 30–40 минут выдаёт:
- архитектуру фичи (слои, модули, интерфейсы, офлайн, платформо-зависимое);
- тестовую стратегию, план запуска (feature flags, A/B, аналитика), риски;
- оценку по этапам и диаграмму Ганта (Mermaid);
- состав команды min / opt / max с учётом ускорения от ИИ и варианты скоупа.

## Установка

```bash
git clone https://github.com/mikhail-muzhev/kmp-system-design-skill.git
ln -s "$(pwd)/kmp-system-design-skill/kmp-system-design" ~/.claude/skills/kmp-system-design
```

## Использование

В Claude Code: `/kmp-system-design` или «спроектируй фичу …».
Команды во время сессии: `дальше`, `критика`, `кратко`, `за N недель`, `что спросить`, `допущения`, `итог`.

## Структура

```
kmp-system-design/
  SKILL.md                         — поток интервью, правила, команды
  references/architecture.md       — шаблон архитектуры KMP-фичи
  references/quality-and-risks.md  — тесты, запуск, риски
  references/estimation.md         — эвристики оценки, команда, Гант
  references/output-template.md    — шаблон итогового документа
```
