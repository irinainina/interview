# CSS-анимации

### Основные способы анимации в CSS

* `transition`: анимация одного/нескольких свойств при изменении состояния
* `animation`: воспроизведение серии ключевых кадров по заданным параметрам

### Свойства `transition`:

* `transition-property`: список свойств, которые должны анимироваться (например, `opacity`, `transform`)
* `transition-duration`: продолжительность анимации (например, `0.5s`)
* `transition-timing-function`: кривая ускорения (`ease`, `linear`, `ease-in-out`, `cubic-bezier()` и т.д.)
* `transition-delay`: задержка перед началом анимации

### Свойства `animation`:

* `animation-name`: имя анимации, заданной через `@keyframes`
* `animation-duration`: продолжительность одного цикла
* `animation-timing-function`: кривая ускорения (аналог `transition-timing-function`)
* `animation-delay`: задержка перед запуском
* `animation-iteration-count`: число повторений (`infinite` для бесконечной)
* `animation-direction`: направление (`normal`, `reverse`, `alternate`, `alternate-reverse`)
* `animation-fill-mode`: поведение до/после анимации (`none`, `forwards`, `backwards`, `both`)

### Пример `transition`

```css
.button {
  transition: background 0.3s ease;
}
.button:hover {
  background: red;
}
```

### Пример `@keyframes`

```css
@keyframes slideIn {
  from { transform: translateX(-100%); }
  to { transform: translateX(0); }
}
.box {
  animation: slideIn 0.5s ease-out;
}
```

### Рекомендации по производительности

* Использовать `transform` и `opacity`, избегать `top/left`, `width/height`
* Использовать `will-change` только на элементах, где это оправдано
* Не применять анимации ко множеству элементов одновременно
* Тестировать с помощью DevTools > Performance

  * Record > interaction > Frames per second (FPS)
  * Layout & Paint > проверить нагрузку рендера
  * Layers > выявить перегрузку GPU

---

## Частые вопросы по CSS-анимациям на собеседовании

**Чем `animation` отличается от `transition`?**

* `transition` — одноразовое изменение при смене состояния, `animation` — воспроизведение по ключевым кадрам, может повторяться и быть автономной

**Как задать бесконечную анимацию?**

```css
animation-iteration-count: infinite;
```

**Как применить задержку между итерациями?**

* CSS не поддерживает паузу между итерациями напрямую. Решение — вставить паузу в `@keyframes` или использовать JS/GSAP

**Какие свойства анимируются лучше всего?**

* `transform`, `opacity` — GPU-ускоряются и не вызывают reflow/repain

**Как использовать `animation-fill-mode`?**

* `forwards` — сохранить конечное состояние
* `backwards` — применить начальное до старта анимации
* `both` — совместить оба

---

## Альтернативные и дополнительные виды анимаций

### Lottie (анимации из After Effects через JSON)

* Использует библиотеку `lottie-web`
* Позволяет вставлять сложные SVG-анимации в Web

**Пример инициализации:**

```js
lottie.loadAnimation({
  container: document.getElementById('anim'),
  renderer: 'svg',
  loop: true,
  autoplay: true,
  path: 'data.json'
});
```

**Когда использовать:**

* Для иконок, лоадеров, сцен из AE без потери качества

### Вопросы по Lottie

**Что такое Lottie?**

* JSON-анимации, экспортированные из After Effects с Bodymovin

**Когда лучше использовать?**

* Когда нужны сложные SVG-анимации с минимальным весом

**Как синхронизировать с действиями пользователя?**

* Через методы `play()`, `stop()`, `goToAndStop(frame)` и события `onComplete`

---

### JavaScript-анимации (GSAP, anime.js)

**GSAP:**

```js
gsap.to('.box', { x: 100, duration: 1 });
```

* Производительный, поддерживает сложные последовательности

**Anime.js:**

```js
anime({ targets: '.box', translateX: 250, duration: 800 });
```

* Простая и мощная API, поддержка SVG и DOM

**Вопросы по GSAP:**

* В чём плюсы GSAP? → Производительность, контроль, паузы, цепочки
* Что такое timeline? → Механизм синхронизации анимаций в GSAP

---

### Three.js (WebGL-анимации)

* Для 3D, физики, сложных визуализаций
* Используется цикл `requestAnimationFrame`

```js
function animate() {
  requestAnimationFrame(animate);
  mesh.rotation.x += 0.01;
  renderer.render(scene, camera);
}
animate();
```

**Вопросы по Three.js:**

* Как анимировать объект? → Изменять свойства в каждом кадре
* Что делает `requestAnimationFrame`? → Оптимизирует отрисовку под частоту кадров браузера

---

### SVG-анимации

* Через `stroke-dashoffset`, `path`-анимации, SMIL или JS
* Эффективны для иконок, логотипов, иллюстраций

---

### Canvas-анимации

* Низкоуровневые, контроль каждого пикселя
* Используются в играх, интерактивных сценах

---

## Общее

**Какие виды анимаций наиболее производительные?**

* `transform` и `opacity` в CSS или GSAP с hardware acceleration

**Когда лучше использовать JS вместо CSS?**

* Когда требуется контроль, сложные цепочки, события, паузы

**Как оценить влияние анимаций на производительность?**

* Инструменты: Chrome DevTools → Performance → FPS/Timeline/Rendering
* Lighthouse → «Avoid large layout shifts», «Reduce impact of animations»
* Снижение FPS, скачки layout — тревожный сигнал

---

## Заключение

Компании, которые стремятся к «wow-эффекту», применяют сложные интерфейсные анимации: от CSS до Lottie и WebGL. Ключевые факторы успеха: умеренность, производительность, осмысленность движения.
