1.  Релизуйте функцию debounce\
    _Примечание_: debounce запускает функцию один раз после периода «бездействия». Подходит для обработки конечного результата.

    ```javascript
    const fetchUrl = (url) => {
      console.log(url);
    };

    const debounce = (callback, delay) => {
      // реализовать код который выведет 3
    };

    const fetching = debounce(fetchUrl, 300);

    fetching(1);
    fetching(2);
    fetching(3);
    ```

    <details>
      <summary>Ответ</summary>

    ```javascript
    const fetchUrl = (url) => {
      console.log(url);
    };

    const debounce = (callback, delay) => {
      let timerId;

      return (...arg) => {
        if (timerId) {
          clearTimeout(timerId);
        }

        timerId = setTimeout(() => {
          callback(...arg);
        }, delay);
      };
    };

    const fetching = debounce(fetchUrl, 300);

    fetching(1);
    fetching(2);
    fetching(3);
    ```

    </details>
    <br/>

2.  <span style="color: red">Реализуйте собственный класс Promise</span>
    <details>
      <summary>Ответ</summary>
       
    </details>
    <br/>
3.  Реализуйте собственный Promise.all
    <details>
      <summary>Ответ</summary>

    ```javascript
    function promiseAll(arrayOfPromises) {
      return new Promise((resolve, reject) => {
        const result = [];
        let count = 0;

        for (let i = 0; i < arrayOfPromises.length; i++) {
          const promise = arrayOfPromises[i];
          promise
            .then((data) => {
              result[i] = data;
              count++;
              if (count === arrayOfPromises.length) {
                resolve(result);
              }
            })
            .catch((err) => reject(err));
        }
      });
    }
    ```

    </details>
    <br/>

4.  Реализуйте собственный Promise.allSettled
    <details>
      <summary>Ответ</summary>

    ```javascript
    function promiseAllSettled(arrayOfPromises) {
      return new Promise((resolve, reject) => {
        const result = [];
        let count = 0;
        for (let i = 0; i < arrayOfPromises.length; i++) {
          const promise = arrayOfPromises[i];
          promise
            .then((data) => {
              result[i] = { status: "fulfilled", value: data };
            })
            .catch((err) => (result[i] = { status: "rejected", reason: err }))
            .finally(() => {
              count++;
              if (count === arrayOfPromises.length) {
                resolve(result);
              }
            });
        }
      });
    }
    ```

      </details>
      <br/>

5.  Реализуйте собственный Promise.race
    <details>
      <summary>Ответ</summary>

    ```javascript
    function promiseRace(arrayOfPromises) {
      return new Promise((resolve, reject) => {
        for (let i = 0; i < arrayOfPromises.length; i++) {
          const promise = arrayOfPromises[i];
          promise
            .then((data) => {
              resolve(data);
            })
            .catch((err) => reject(err));
        }
      });
    }
    ```

    </details>
      <br/>

6.  <span style="color: red">Реализуйте собственный Promise.any</span>
    <details>
      <summary>Ответ</summary>
       
    </details>
    <br/>
7.  Промисифицируйте данный код

    ```javascript
    function loadScript(src, callback) {
      let script = document.createElement("script");
      script.src = src;

      script.onload = () => callback(null, script);
      script.onerror = () =>
        callback(new Error(`Ошибка загрузки скрипта ${src}`));

      document.head.append(script);
    }
    ```

    <details>
      <summary>Ответ</summary>

    ```javascript
    function loadScript(src) {
      return new Promise((resolve, reject) => {
        let script = document.createElement("script");
        script.src = src;

        script.onload = () => resolve(script);
        script.onerror = () =>
          reject(new Error(`Ошибка загрузки скрипта ${src}`));

        document.head.append(script);
      });
    }
    ```

    </details>
    <br/>

8.  Реализуйте функцию, которая реализует глубокое копирование объекта
    <details>
    <summary>Ответ</summary>

    ```javascript
    function cloneDeep(data) {
      if (!data || typeof data !== "object") return data;
      const result = Array.isArray(data) ? [] : {};
      for (const prop in data) {
        result[prop] = cloneDeep(data[prop]);
      }
      return result;
    }
    ```

    </details>
    <br/>

9.  Реализуйте функцию throttle
    _Примечание_: throttle запускает функцию не чаще, чем указанное время ms. Подходит для регулярных обновлений, которые не должны быть слишком частыми.

    ```javascript
    function f(a) {
      console.log(a);
    }

    // f1000 передаёт вызовы f максимум раз в 1000 мс
    let f1000 = throttle(f, 1000);

    f1000(1); // показывает 1
    f1000(2); // (ограничение, 1000 мс ещё нет)
    f1000(3); // (ограничение, 1000 мс ещё нет)

    // когда 1000 мс истекли ...
    // ...выводим 3, промежуточное значение 2 было проигнорировано
    ```
