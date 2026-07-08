# README-FORK — отличия форка highscrren-dotcom от upstream

> Upstream: [backtest-kit/backtest-monorepo-parallel](https://github.com/backtest-kit/backtest-monorepo-parallel).
> Роль в нашем стеке: **каркас продакшн-раннера** (мульти-символ в одном процессе,
> пре-кэш свечей; см. `paperhands/agent/notes/fork-map.md`). Ветка правок —
> `integration` (master = чистый upstream).
>
> ⚠️ **В upstream НЕТ LICENSE** — репозиторий формально «all rights reserved».
> GitHub не позволяет сделать форк приватным (решение владельца 2026-07-06:
> оставляем публичным). Митигация: у владельца прямой контакт с автором — он сам
> рекомендовал повторять его экосистему; при случае попросить добавить LICENSE
> в upstream. Свой оригинальный код в этот репо не добавляем.

## Отличия от upstream

1. ~~Чужие Telegram-креды удалены~~ **ОТКАЧЕНО 2026-07-08** (решение владельца:
   Telegram-сторону ведёт автор — работаем на его app-кредах). `params.ts` обоих
   пакетов и `getTelegram()` возвращены к апстриму: дефолтные креды автора
   (api_id 31861455) — fallback, env-переменные — опциональный override.
2. **Redis-пароль из окружения** (`docker/redis/docker-compose.yaml`).

## Что помнить (из разбора fork-map)

- README апстрима устарел (пишет backtest-kit 9.8.2; реально package.json пинит 15.0.0).
- «6300×» — маркетинговый агрегат (9 символов × ~703× на 34-минутном срезе).
- paper.ts == live.ts на уровне шаблона — paper-семантику даёт движок.
- Что переносим в свой стек: пре-кэш `cacheCandles` до прогонов, паттерн
  setup.config «backtest=Memory / live=Persist», golden-тесты парсера
  (test/spec/screen_crypto_yoda.test.mjs), Backtest.background по CC_SYMBOL_LIST.
