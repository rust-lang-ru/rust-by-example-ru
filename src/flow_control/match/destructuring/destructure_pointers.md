# pointers/ref

Для указателей необходимо различать деструктуризацию и разыменование, 
поскольку это разные концепции, которые используются иначе, чем в языке `С`.

 * Разыменование использует `*`
 * Деструктуризация использует `&`, `ref` и `ref mut`

```rust,editable
fn main() {
    // Присваиваем ссылку на тип `i32`. 
    // Символ `&` означает, что присваивается ссылка.
    let reference = &4;

    match reference {
        // Если `reference` - это шаблон, который сопоставляется с `&val`,
        // то это приведёт к сравнению:
        // `&i32`
        // `&val`
        // ^ Мы видим, что если отбросить сопоставляемые `&`, 
        // то переменной `val` должно быть присвоено `i32`.
        &val => println!("Получаем значение через деструктуризацию: {:?}", val),
    }

    // Чтобы избежать символа `&`, нужно разыменовывать ссылку до сопоставления.
    match *reference {
        val => println!("Получаем значение через разыменование: {:?}", val),
    }

    // Что если у нас нет ссылки? `reference` была с `&`,
    // потому что правая часть была ссылкой. Но это не ссылка, 
    // потому что правая часть ею не является.
    let _not_a_reference = 3;

    // Rust предоставляет ключевое слово `ref` именно для этой цели. 
    // Оно изменяет присваивание так, что создаётся ссылка для элемента. 
    // Теперь ссылка присвоена.
    let ref _is_a_reference = 3;

    // Соответственно, для определения двух значений без ссылок, 
    // ссылки можно назначить с помощью `ref` и `ref mut`.
    let value = 5;
    let mut mut_value = 6;

    // Используйте ключевое слово `ref` для создания ссылки.
    match value {
        ref r => println!("Получили ссылку на значение: {:?}", r),
    }

    // Используйте `ref mut` аналогичным образом.
    match mut_value {
        ref mut m => {
            // Получаем ссылку. Её нужно разыменовать, 
            // прежде чем мы сможем что-то добавить.
            *m += 10;
            println!("Мы добавили 10. `mut_value`: {:?}", m);
        },
    }
}
```