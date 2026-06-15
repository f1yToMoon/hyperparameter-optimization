# Как запустить

Лабораторная работа: **Плохоформализуемые задачи на примере подбора гиперпараметров
деревьев решений**. Результат — ноутбук
`Лабораторная_подбор_гиперпараметров.ipynb`.

---

## Вариант 1. Conda-окружение `nlp` (как выполнялась работа)

```bash
# активировать окружение
conda activate nlp

# доустановить зависимости (если ещё не стоят)
pip install -r requirements.txt
```

Запуск ноутбука в браузере:

```bash
jupyter notebook Лабораторная_подбор_гиперпараметров.ipynb
```

В открывшемся ноутбуке: **Kernel → Restart & Run All** (выполнить все ячейки сверху вниз).

---

## Вариант 2. Чистое виртуальное окружение (venv)

```bash
python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt

jupyter notebook Лабораторная_подбор_гиперпараметров.ipynb
```

---

## Запуск без графического интерфейса (из терминала)

Перевыполнить весь ноутбук «на месте» (перезапишет выводы и графики):

```bash
python - <<'PY'
import nbformat
from nbclient import NotebookClient
nb = nbformat.read("Лабораторная_подбор_гиперпараметров.ipynb", as_version=4)
NotebookClient(nb, timeout=600, kernel_name="python3").execute()
nbformat.write(nb, "Лабораторная_подбор_гиперпараметров.ipynb")
print("Готово")
PY
```

Либо через nbconvert (если установлен пакет `nbconvert`):

```bash
jupyter nbconvert --to notebook --execute --inplace \
  --ExecutePreprocessor.timeout=600 \
  Лабораторная_подбор_гиперпараметров.ipynb
```

---

## Что должно получиться

- Ноутбук выполняется полностью без ошибок (~10 секунд счёта).
- Печатаются результаты трёх методов (best score, число оценок функции, время).
- Строятся графики: разрывность `F(max_depth)`, «качество vs число оценок»,
  «время vs качество».
- Итоговая таблица сравнения Grid Search / Генетический алгоритм / Bayesian
  Optimization.

---

## Возможные проблемы

- **`ModuleNotFoundError: optuna` (или nbformat/nbclient)** — выполнить
  `pip install -r requirements.txt` в активном окружении.
- **`jupyter: command not found`** — установить `pip install jupyter`.
- **Предупреждение `IProgress not found` от tqdm** — безвредно, на результат
  не влияет (это лишь индикатор прогресса Optuna).
