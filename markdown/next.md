# Основы Next.js

**Что такое Next.js?**

* Фреймворк поверх React для серверного рендеринга, генерации страниц и маршрутизации.
* Поддерживает SSR, SSG, ISR и CSR.
* Имеет встроенную маршрутизацию, API routes, поддержку module CSS и TypeScript.

**Зачем использовать Next.js?**

* Улучшенная SEO-оптимизация благодаря SSR/SSG.
* Повышение производительности за счёт предварительной генерации и стриминга.
* Встроенные оптимизации (lazy loading, image optimization и др.).

---

## Рендеринг

**Типы рендеринга в Next.js:**

1. **CSR (Client-Side Rendering)** — обычный React
2. **SSR (Server-Side Rendering)** — `getServerSideProps`
3. **SSG (Static Site Generation)** — `getStaticProps`
4. **ISR (Incremental Static Regeneration)** — `revalidate` в `getStaticProps`


**В чём разница между getStaticProps и getServerSideProps?**

* `getStaticProps` — вызывается на этапе сборки, используется для SSG.
* `getServerSideProps` — вызывается на каждый запрос, используется для SSR.

**Что такое ISR и зачем он нужен?**

* Позволяет статическим страницам обновляться после сборки.
* Объединяет преимущества SSR и SSG.

---

## Маршрутизация

**Как работает маршрутизация в Next.js?**

* Основывается на файловой структуре в папке `/pages`.
* Каждый файл = маршрут.
* Поддерживает динамические маршруты: `[id].js`

**Что такое dynamic routing и catch-all routing?**

* `[id].js` — динамический маршрут.
* `[...slug].js` — catch-all маршрут (массив сегментов).
* `[[...slug]].js` — необязательный catch-all.

---

## App Router (Next.js 13+)

**Чем отличается App Router от Pages Router?**

* App Router (папка `/app`) использует React Server Components, async/await, layout.
* Pages Router (папка `/pages`) — классический подход.

**Что такое layouts и зачем они нужны?**

* Позволяют создавать общие обёртки для страниц (например, header/footer).
* Persist layout между навигациями.

**Что такое loading.js, error.js, not-found.js?**

* Специальные файлы в App Router:

  * `loading.js` — индикатор загрузки.
  * `error.js` — обработка ошибок.
  * `not-found.js` — для 404 страниц.

---

## API Routes

**Что такое API routes в Next.js?**

* Обработка серверных запросов внутри проекта.
* Файлы в `/pages/api` становятся эндпоинтами.

```js
// pages/api/hello.js
export default function handler(req, res) {
  res.status(200).json({ name: 'John' });
}
```

---

## Static Files и Assets

**Как работать со статикой в Next.js?**

* Папка `/public` — для изображений, файлов.
* Доступ через `/имя-файла`.

---

## Оптимизация и производительность

**Оптимизация изображений:**

* `next/image` автоматически оптимизирует изображения.
* Поддерживает lazy loading, responsive, WebP.

```jsx
import Image from 'next/image';
<Image src="/logo.png" width={100} height={100} alt="logo" />
```

**Code Splitting и Lazy Loading:**

* `dynamic()` импорт компонентов по требованию:

```jsx
import dynamic from 'next/dynamic';
const DynamicComp = dynamic(() => import('./Comp'));
```

---

## Модули и TypeScript

**Как Next.js работает с TypeScript?**

* Имеет встроенную поддержку.
* При запуске с `.ts` и `.tsx` создаст `tsconfig.json` автоматически.

**ES-модули — как работают импорты/экспорты?**

```js
// export
export const x = 5;
export default function() {}

// import
import x from './file';
import { x } from './file';
```

---

## Auth и Middleware

**Что такое middleware в Next.js 12+?**

* Запускается до обработки запроса.
* Можно делать редиректы, проверку прав и т.п.

```js
// middleware.js
export function middleware(req) {
  // auth logic
}
```

---

## Новое в Next.js 14–13

* App Router — файловый layout-based routing
* Server Actions — функции, запускаемые на сервере прямо из компонента
* `use()` — await прямо в компоненте
* Больше поддержки для Streaming / SSR

---

## Бест практики

* Выносите логику в Server Components при возможности
* Используйте ISR для страниц, которые нужно периодически обновлять
* Старайтесь не использовать `getInitialProps` — устарело
* Статику храните в `/public`
* Используйте `next/image` вместо `<img>`
* Мемоизируйте heavy-компоненты с `useMemo` и `React.memo`

---
