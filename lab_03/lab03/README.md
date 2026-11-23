# ЛР № 3. Контекстный перевод и локализация с помощью LLM (вариант 3)

Управляемый LLM-пайплайн перевода: системная инструкция, термины сегмента из TBX, примеры few-shot из TMX,
JSON Schema + Pydantic, терминологическая QA, targeted repair, сравнение стилей и сравнение с NMT (ЛР № 2).

## Как воспроизвести
1. Открыть `LAB_03.ipynb` в Google Colab, среда — GPU T4.
2. Положить `variant_<N>.tmx`, `variant_<N>.tbx` и `lab02_results.zip` в `lab03/input/`.
3. Выполнить все ячейки. Модель: `qwen3.5:4b` (`ollama`), сборка `d8b0f5e9760c`, temperature 0.0, seed 42.
4. Для облачных моделей задать секреты по образцу `.env.example` (Colab Secrets или `.env`).

## Структура
- `prompts/` — промпты (версия v1.1, хэши в `prompt_versions.md`) и JSON Schema
- `results/` — трассировка `results_llm.jsonl`, `terminology_qa.csv`, `markup_checks.csv`, `repair_cases.csv`,
  `style_comparison.csv`, `comparison.csv`, `mode_summary.csv`
- `figures/` — рисунки анализа
- `report.md` — отчёт; `requirements.txt` — зависимости
