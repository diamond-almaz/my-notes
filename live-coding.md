1. Релизуйте функцию debounce
    ```
    const fetchUrl = (url) => {
    console.log(url)
    }

    const debounce = (callback, delay) => {
      // реализовать код который выведет 3
    }

    const fetching = debounce(fetchUrl, 300);

    fetching(1);
    fetching(2);
    fetching(3);
    ```

    <details>
      <summary>Ответ</summary>
      
  
        const fetchUrl = (url) => {
        console.log(url)
        }

        const debounce = (callback, delay) => {
        let timerId;

        return (...arg) => {
        if (timerId) {
          clearTimeout(timerId);
        }

        timerId = setTimeout(() => {
          callback(...arg)
        }, delay)
        }
        }

    const fetching = debounce(fetchUrl, 300);

    fetching(1);
    fetching(2);
    fetching(3);
</details>
   
2. Реализуйте собственный класс Promise
   <details>
     <summary>Ответ</summary>
      
   </details>
4. Реализуйте собственный Promise.all
   <details>
     <summary>Ответ</summary>
      
   </details>
5. Реализуйте собственный Promise.allSettled
   <details>
     <summary>Ответ</summary>
      
   </details>
6. Реализуйте собственный Promise.race
   <details>
     <summary>Ответ</summary>
      
   </details>
8. Реализуйте собственный Promise.any
   <details>
     <summary>Ответ</summary>
      
   </details>
9. Промисифицирйте данный код
    ```javascript
    function loadScript(src, callback) {
    let script = document.createElement('script');
    script.src = src;

      script.onload = () => callback(null, script);
      script.onerror = () => callback(new Error(`Ошибка загрузки скрипта ${src}`));

      document.head.append(script);
    }

    ```
   <details>
     <summary>Ответ</summary>

      ```javascript
      function loadScript(src) {
        return new Promise((resolve, reject) => {
        let script = document.createElement('script');
        script.src = src;

        script.onload = () => resolve(script);
        script.onerror = () => reject(new Error(`Ошибка загрузки скрипта ${src}`));

      document.head.append(script);
        })
    }
      ```
   </details>

