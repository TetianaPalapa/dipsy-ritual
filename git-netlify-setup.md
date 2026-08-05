# Підключення GitHub → Netlify (автодеплой)

Мета: `git push` у Cursor автоматично оновлює вже опубліковані сайти — без ручного перетягування файлів у Netlify.

Стосується двох існуючих проєктів (URL не зміняться):
- **dipsy-roadmap** — https://dipsy-roadmap.netlify.app
- **dipsy-ritual** (віджет-прототип) — https://neon-moxie-b94d61.netlify.app

---

## Крок 1 — GitHub-репозиторії

В Cursor (термінал усередині нього) для кожного проєкту окремо:

```bash
cd шлях/до/dipsy-roadmap
git init
git add .
git commit -m "init"
```

На github.com → New repository → назви `dipsy-roadmap` (без README, .gitignore тощо — репо вже має файли локально) → Create.

GitHub покаже команди для підключення — по суті це:

```bash
git remote add origin https://github.com/ТВІЙ_ЛОГІН/dipsy-roadmap.git
git branch -M main
git push -u origin main
```

Повторити те саме для `dipsy-ritual` з окремим репо (наприклад `dipsy-ritual-widget`).

---

## Крок 2 — Прив'язати репо до вже існуючого сайту в Netlify

Важливо: сайти вже створені (`dipsy-roadmap`, `neon-moxie-b94d61`) — не створюй нові, а прив'язуй репо до наявних, щоб URL лишився той самий.

1. app.netlify.com → відкрити потрібний проєкт (**dipsy-roadmap** або **neon-moxie-b94d61**)
2. **Site configuration** → **Build & deploy** → **Continuous deployment**
3. **Link repository** (або **Link site to Git**) → обрати GitHub → авторизувати доступ → обрати відповідний репозиторій → гілка `main`
4. Налаштування білду:
   - **Build command**: залишити порожнім (це static HTML, без збірки)
   - **Publish directory**: `.` (корінь репо, де лежить `index.html`)
5. Save

---

## Крок 3 — Перевірка

Зроби будь-яку дрібну правку → `git add . && git commit -m "test" && git push` → у Netlify на вкладці **Deploys** має з'явитись новий деплой автоматично, і сайт за тим самим лінком оновиться за 10–30 секунд.

---

## Далі за таким принципом

- Стратегію, контент, тексти й правки для роадмапи готую тут — віддаю тобі готовий `index.html`.
- Ти кладеш його у папку репозиторію в Cursor, комітиш і пушиш.
- Netlify підхоплює автоматично — ручний drag-and-drop більше не потрібен.

Те саме працюватиме і для технічної реалізації віджета (MediaPipe-код, продакшн-версія на React + Vite), коли дійдемо до 6 етапу.
