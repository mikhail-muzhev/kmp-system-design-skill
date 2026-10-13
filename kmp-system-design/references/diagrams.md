# Как показывать диаграммы

Блок ```mermaid в чате Claude Desktop / claude.ai не рендерится. Порядок выбора:

## 1. Виджет в чате (`show_widget`, Claude Desktop / claude.ai) — проверено, работает

Один раз за сессию вызови `read_me` визуализации (module `diagram`), затем `show_widget` с HTML ниже. Подставь mermaid-исходник в `src`. Подходит и для `gantt`, и для `flowchart`. Init-блок не меняй (по нему mermaid меряет текст, иначе обрезает подписи).

```html
<h2 class="sr-only">Одно предложение: что на диаграмме.</h2>
<div id="d"></div>
<script type="module">
import mermaid from 'https://esm.sh/mermaid@11/dist/mermaid.esm.min.mjs';
const themeMode = document.documentElement.dataset.mode;
const dark = themeMode ? themeMode === 'dark' : matchMedia('(prefers-color-scheme: dark)').matches;
await document.fonts.ready;
mermaid.initialize({startOnLoad:false, theme:'base', fontFamily:'"anthropic-sans", sans-serif',
  themeVariables:{darkMode:dark, fontSize:'13px', fontFamily:'"anthropic-sans", sans-serif',
  lineColor: dark?'#9c9a92':'#73726c', textColor: dark?'#c2c0b6':'#3d3d3a'}});
const src = `gantt
  dateFormat YYYY-MM-DD
  ...`;
const { svg } = await mermaid.render('d-svg', src);
document.getElementById('d').innerHTML = svg;
</script>
```

Правила:
- В mermaid-исходнике внутри шаблонной строки не используй обратные кавычки и `${`.
- Подписи задач в Ганте — до ~30 символов, иначе налезают.
- Архитектурная схема: ≤ 10–12 узлов. Больше — разбей на обзор + деталь.
- Текст пояснений — в ответе, не внутри виджета.

## 2. Artifact
Если виджета нет (например, Claude Code в терминале) — один Artifact «System Design: <фича>» с mermaid.js; обновляй тот же артефакт, давай ссылку.

## 3. Текст
Только если нет ни того, ни другого: mermaid-текстом + «откроется в GitHub / Android Studio / Obsidian».

## Даты в Ганте
Старт — ближайший понедельник от сегодняшней даты (или дата, названная продактом). Скажи об этом одной строкой. `excludes weekends` — всегда.
