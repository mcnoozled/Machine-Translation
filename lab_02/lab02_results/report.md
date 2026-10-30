# Отчёт по лабораторной работе 2 (вариант 3)

**Тема:** Медицина: кардиология и кардиохирургия

## 1. Среда и устройство
- python: 3.13.16
- torch: 2.11.0+cu130
- transformers: 5.20.2
- device: cuda
- gpu: Tesla T4
- variant: 3
- domain: Медицина: кардиология и кардиохирургия

## 2. Модели
- MarianMT: `Helsinki-NLP/opus-mt-en-ru`, 76.7 млн параметров, токенизатор MarianTokenizer, словарь 62518
- NLLB: `facebook/nllb-200-distilled-600M`, 615 млн параметров, токенизатор NllbTokenizer, словарь 256204
- Языковые коды NLLB: src_lang=`eng_Latn`, forced_bos_token_id=`rus_Cyrl` (256147)
- Внимание: `attn_implementation=eager`

## 3. Токенизация
Разобрано терминов: 103. Среднее число токенов: Marian 4.85, NLLB 4.62.
Файл: `results/tokenization_10_terms.csv`, график: `figures/tokenization_comparison.png`.

## 4. Переводы
Сегментов: 123. Совпали переводы моделей: 1.
Файлы: `results/results_marian.jsonl`, `results/results_nllb.jsonl`, `results/comparison.csv`.

## 5. Кросс-энтропия
Пар: 6. Средний loss эталона 1.1967, по собственному выводу 0.5415.
Наибольший разрыв: s006.
Файл: `results/loss_5_pairs.csv`, график: `figures/loss.png`.

## 6. Cross-attention
Пар: 2. Форма тензора: (1, 8, 73, 60).
Файлы: `results/attention_marian_*.csv`, `results/attention_summary.csv`, график: `figures/cross_attention.png`.

## 7. Время инференса
Последовательно 55.08 с, пакетно (bs=8) 12.16 с, ускорение x4.53 на cuda.
Файл: `results/timing.csv`, график: `figures/timing.png`.

## 8. Различия и ошибки
- s002: NLLB — Pulsus alternans: Marian может описательно переводить, NLLB сохраняет термин
- s004: NLLB — auscultation: NLLB ближе к терминологическому глоссарию
- s017: NLLB — Infective endocarditis: терминология по глоссарию
- s052: ни один — T-tubules invaginate: обе модели искажают техническую лексику
- s053: Marian — Ca2+-ATPase pump: Marian устойчивее к длинным формулам
- s092: NLLB — BMMNCs: NLLB корректнее передаёт аббревиатуру

## 9. Соответствие глоссарию
Вхождений терминов: 165 на модель. Кандидатов в нарушения: 185 (MarianMT 97, NLLB 88).
Файл: `results/glossary_qa.csv`, график: `figures/glossary_qa.png`.

## 10. Вывод
MarianMT: 77 млн параметров, NLLB: 615 млн.
Кандидатов в нарушения глоссария: MarianMT 97, NLLB 88.
Терминологический контроль выносится в отдельный этап, постредактирование обязательно.
