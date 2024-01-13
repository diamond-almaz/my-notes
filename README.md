# js-concepts

---

## Event loop

#### Статьи
  1. [Event Loop в деталях](https://habr.com/ru/articles/762618)

#### Задачи
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
Step 5: In another setTimeout \
   </details>
3. dsad
4. 

---

