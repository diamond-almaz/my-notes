1. ```const fetchUrl = (url) => {
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
```

<details>
    <summary>Название</summary>
    Какой-нибудь длиинный дополнительный текст, который по умолчанию должен быть скрыт. Его можно показать, нажав на спойлер.
</details>
