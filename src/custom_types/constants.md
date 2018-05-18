# Константы

В Rust есть два типа констант, которые могут быть объявлены
в любой области видимости, включая глобальную. Оба требуют явной аннотации типа:

* `const`: Неизменяемая переменная (в общем случае).
* `static`: Возможно, изменяемая переменная с временем жизни [`'static`][static].

Частным случаем является литерал `"string"`. Он может быть напрямую
назначен переменной с временем жизни `'static`, т.к сигнатура его типа:
`&'static str` требует время жизни `'static`. Для всех остальных ссылочных типов
должно быть указано время жизни `'static`. Это может показаться
незначительным, но в требовании явной аннотации типов и скрываются различия.

```rust,editable,ignore,mdbook-runnable
// Константы объявлены в глобальной области видимости.
static LANGUAGE: &'static str = "Rust";
const  THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    // Получаем доступ к константе внутри функции
    n > THRESHOLD
}

fn main() {
    let n = 16;

    // Получаем доступ к константе внутри функции main
    println!("Это язык {}", LANGUAGE);
    println!("Установим предел, равный {}", THRESHOLD);
    println!("Число {} {} предела", n, if is_big(n) { "больше" } else { "меньше" });

    // Ошибка! `константы` нельзя изменить.
    THRESHOLD = 5;
    // ИСПРАВЬТЕ ^ Закомментируйте эту строчку
}
```

### Смотрите также:

[RFC для `const`/`static`](
https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md),
[`время жизни 'static`][static]

[static]: scope/lifetime/static_lifetime.html