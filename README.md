# js-concepts

---

## Event loop

<details>
  <summary>Тезисное объяснение</summary>
  <br/>

  Javascript является однопоточным языком программирования, то есть он не может выполнять две операции одновременно. Исходя из этого возникает необходимость работы с асинхронными операциями. Для этого есть Event loop - менеджер асинхронных вызовов.
  <br/>
    <br/>
  Если синхронный код попадая в стек вызовов (callstack) выполняется мгновенно, то с асинхронным все иначе. Асинхронный код после того как попадает в callstack не вызывется сразу, он    переходит в web api и когда он будет готов, он переходит в очередь задач (task queue) и после того как очиститься callstack - выполняется.

  Сама очередь задач делится на два типа:
   - микрозадачи
       - промисы
       - queueMicrotask
       - mutationObserver
   - макрозадачи
       - таймеры (setTimeout, setInterval)
       - события (клик, загрузка изображения и тд)
       - браузерные нюансы (рендер, I/O и тд)
    
  Микротаски выполняются первее макрозадач. 

  Наглядный пример работы event loop:
  ![Наглядный пример](https://www.jscamp.app/ru/assets/images/br-1e24a585f7b50873c0cae1bec221d0d7.gif "Наглядный пример")

  Важные замечание: 
   - Event loop не является частью движка, он предоставляется средой (браузер или node js)
   - Устройство event loop в браузере и node js разный
   - Задачи из очереди задач выполнятся только когда callstack будет пустой
  
  

  
</details>

#### Статьи
  1. [Event Loop в деталях](https://habr.com/ru/articles/762618)
  2. [Событийный цикл: микрозадачи и макрозадачи](https://learn.javascript.ru/event-loop)
  3. [Асинхронность Event loop](https://www.jscamp.app/ru/docs/javascript25)
  4. [Как управлять event loop в JavaScript. Часть 1](https://skillbox.ru/media/code/event_loop_chast_1/)
  5. [Как управлять event loop в JavaScript. Часть 2](https://skillbox.ru/media/code/event_loop_chast_2/)
#### Видео
  1. [Event Loop от А до Я. Архитектура браузера и Node JS. Движки и рендер. Самое подробное видео](https://www.youtube.com/watch?v=zDlg64fsQow)

#### Задачи
---
1. Что код выведет в консоли
   ```
   console.log("Step 1: In global scope")

    setTimeout(() => console.log("Step 2: In setTimeout"));

    new Promise((resolve) => {
      console.log('Step 3: In promise constructor');
    }).then(() => console.log('Step 4: In then'));

    setTimeout(() => console.log("Step 5: In another setTimeout"))
   ```
   <details>
     <summary>Ответ</summary>

      >Step 1: In global scope \
      Step 3: In promise constructor \
      Step 4: In then \
      Step 2: In setTimeout \
      Step 5: In another setTimeout
   </details>
---
2. Что код выведет в консоли
   ```
   console.log("Step 1: In global scope")

   setTimeout(() => console.log("Step 2: In setTimeout"));

   new Promise((resolve) => {
    console.log('Step 3: In promise constructor');
   }).then(() => console.log('Step 4: In then'))
     .then(() => console.log('Step 5: In another then'));

   setTimeout(() => console.log("Step 6: In another setTimeout"))
    ```
    <details>
      <summary>Ответ</summary>

      >Step 1: In global scope \
      Step 3: In promise constructor \
      Step 4: In then \
      Step 5: In another then \
      Step 2: In setTimeout \
      Step 6: In another setTimeout
    </details>
  
---

3. Что код выведет в консоли
   ```
   console.log("Step 1: In global scope")

    setTimeout(() => console.log("Step 2: In setTimeout"));

    new Promise((resolve) => {
    console.log('Step 3: In promise constructor');
    resolve();
    }).then(() => console.log('Step 4: In then'))
    .then(() => console.log('Step 5: In another then'));

    setTimeout(() => console.log("Step 6: In another setTimeout"))

    new Promise((resolve) => {
      console.log('Step 7: In promise constructor');
      resolve();
    }).then(() => console.log('Step 8: In then'))
      .then(() => console.log('Step 9: In another then'));
   ```
   <details>
      <summary>Ответ</summary>

      >Step 1: In global scope \
      Step 3: In promise constructor \
      Step 7: In promise constructor \
      Step 4: In then \
      Step 8: In then \
      Step 5: In another then \
      Step 9: In another then \
      Step 2: In setTimeout \
      Step 6: In another setTimeout
    </details>
---
4. Что код выведет в консоли
   ```
   setTimeout(() => console.log('Step 1: In setTimeout'));

   new Promise(resolve => {
    console.log('Step 2: In promise constructor');
    resolve();
    }).then(() => {
    console.log('Step 3: In then');
    setTimeout(() => console.log('Step 4: In setTimeout (inside of "then")'));
   });

    setTimeout(() => console.log('Step 5: In another setTimeout'));
   ```
   <details>
     <summary>Ответ</summary>
     
     >Step 2: In promise constructor \
      Step 3: In then \ 
      Step 1: In setTimeout \
      Step 5: In another setTimeout \
      Step 4: In setTimeout (inside of "then")
   </details>  
---
5. Что код выведет в консоли
   ```
   setTimeout(() => console.log('Step 1: In setTimeout'));
   setTimeout(() => {
    new Promise(resolve => {
    console.log('Step 2: In promise constructor (inside setTimeout)');
    resolve();
    }).then(() => console.log('Step 3: In then (inside setTimeout)'));
    });

    new Promise(resolve => {
    console.log('Step 4: In promise constructor');
    resolve();
    }).then(() => {
    console.log('Step 5: In then');
    });

    setTimeout(() => console.log('Step 6: In another setTimeout'));
   ```
   <details>
     <summary>Ответ</summary>
     
     >Step 4: In promise constructor \
     Step 5: In then \
     Step 1: In setTimeout \
     Step 2: In promise constructor (inside setTimeout) \
     Step 3: In then (inside setTimeout) \
     Step 6: In another setTimeout 
   </details> 
6. Что код выведет в консоли
   ```
   setTimeout(function timeout() {
    console.log('Таймаут');
    }, 0);

    let p = new Promise(function(resolve, reject) {
    console.log('Создание промиса');
    resolve();
    });

    p.then(function(){
    console.log('Обработка промиса');
    });

    console.log('Конец скрипта');
    ```
   <details>
     <summary>Ответ</summary>
     
     >Создание промиса \
     Конец скрипта \
     Обработка промиса \
     Таймаут
   </details> 
7. ```
   console.log(1);

    setTimeout(() => console.log(2));

    Promise.resolve().then(() => console.log(3));

    Promise.resolve().then(() => setTimeout(() => console.log(4)));

    Promise.resolve().then(() => console.log(5));

    setTimeout(() => console.log(6));

    console.log(7);
   ```
   <details>
     <summary>Ответ</summary>
     
     >1 7 3 5 2 6 4
   </details> 



---

