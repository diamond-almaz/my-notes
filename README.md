# js-concepts

---

## Event loop

<details>
  <summary>Тезисное объяснение</summary>

  
</details>

#### Статьи
  1. [Event Loop в деталях](https://habr.com/ru/articles/762618)
#### Видео
  1. [Event Loop от А до Я. Архитектура браузера и Node JS. Движки и рендер. Самое подробное видео](https://www.youtube.com/watch?v=zDlg64fsQow)

#### Задачи
---
1. ```
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
2. ```
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

3. ```
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
4. ```
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
5. ```
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




---

