# Operator

Kita tahu banyak operator dari sekolah. Mereka adalah penambahan `+`, perkalian `*`, pengurangan `-`, dll.

Di bab ini, kita akan fokus pada aspek operator yang tak dicover artimatika sekolah.

## Istilah: "unary", "binary", "operand"

Sebelum kita lanjut, mari pahami dulu terminologi umum.

- *Operand* -- untuk apa operator diaplikasikan. Misalnya, dalam perkalian `5 * 2` ada dua operand: operand kiri `5` dan operand kanan `2`. Kadang, orang memanggil ini "argumen" ketimbang "operand".
- Operator disebut *unary* jika ia punya operand tunggal. Misalnya, negasi unary `-` membalikkan tanda dari angka:

    ```js run
    let x = 1;

    *!*
    x = -x;
    */!*
    alert( x ); // -1, negasi unary diaplikasikan
    ```
- Operator disebut *binary* jika ia punya dua operand. Minus yang sama juga berada dalam bentuk binary:

    ```js run no-beautify
    let x = 1, y = 3;
    alert( y - x ); // 2, minus binary mengurangi nilai
    ```

    Formalnya, kita akan membahas tentang dua operator berbeda di sini: negasi unary (operand tunggal: membalikkan tanda) dan pengurangan binary (dua operand: pengurangan).

## Konkatenasi string, binary +

Sekarang, mari kita lihat fitur spesial operator JavaScript di luar aritmatika sekolah.

Biasanya, operator plus `+` menambah angka.

Tapi, jika binary `+` diaplikasikan ke string, ia menggabungkan (konkatenasi) mereka:

```js
let s = "my" + "string";
alert(s); // mystring
```

Ingat bahwa jika salah satu operand berupa string, maka yang satunya dikonversi ke string juga.

Misalnya:

```js run
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```

Lihat, tak masalah operand manapun yang berupa string. Aturannya simpel: jika salah satu operand adalah string, maka yang satunya dikonversi ke string juga.

Namun, ingat bahwa operasi berjalan dari kiri ke kanan. Jika ada dua angka diikuti string, angka akan ditambah sebelum dikonversi ke string:


```js run
alert(2 + 2 + '1' ); // "41" dan bukan "221"
```

Konkatenasi string dan konversi adalah fitur spesial dari binary plus `+`. Operator aritmatika lainnya bekerja hanya dengan angka dan selalu mengkonversi operand mereka ke angka.

Misalnya, pengurangan dan pembagian:

```js run
alert( 2 - '1' ); // 1
alert( '6' / '2' ); // 3
```

## Konversi angka, unary +

Plus `+` ada dalam dua bentuk: bentuk binary yang kita gunakan di atas dan bentuk unary.

Plus unary atau, dalam kata lain, operator plus `+` diaplikasikan ke nilai tunggal, tak berefek apapun ke angka. Tapi jika operand bukan angka, plus unary dikonversi ke dalam angka.

Misalnya:

```js run
// Tak ada efek ke angka
let x = 1;
alert( +x ); // 1

let y = -2;
alert( +y ); // -2

*!*
// Mengkonversi non-angka
alert( +true ); // 1
alert( +"" );   // 0
*/!*
```

Sebenarnya ia melakukan hal yang sama seperti `Number(...)`, tapi lebih pendek.

Kebutuhan mengkonversi string ke angka sangat sering meningkat. Misalnya, jika kita memperoleh nilai dari field form HTML, mereka biasanya string.

Bagaimana jika kita ingin menjumlahkan mereka?

Binary plus akan menambah mereka sebagai string:

```js run
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", binary plus mengkonkatenasi string
```

Jika kita ingin memperlakukan mereka sebagai angka, kita harus mengkonversi, lalu menjumlahkan mereka:

```js run
let apples = "2";
let oranges = "3";

*!*
// kedua nilai dikonversi ke angka sebelum binary plus
alert( +apples + +oranges ); // 5
*/!*

// varian lebih panjang
// alert( Number(apples) + Number(oranges) ); // 5
```

Dari sisi pandang matematikawan, melimpahnya plus terlihat aneh. Tapi dari sisi pandang programmer, tak ada yang spesial: plus unary diaplikasikan dahulu, lalu mengkonversi string ke angka, dan lalu binary plus menjumlahkan mereka.

Kenapa plus unary diaplikasi ke nilai sebelum binarynya? Seperti yang kita lihat, itu karena *peresedensi lebih tinggi* mereka.

## Presedensi operator

Jika expresi punya lebih dari satu operator, urutan eksekusi ditentukan oleh *presedensi* mereka, atau dengan kata lain, urutan prioritas implisit operator.

Dari sekolah, kita semua tahu bahwa perkalian dalam expresi `1 + 2 * 2` harus dihitung sebelum penambahan. Itulah arti dari presedensi. Perkalian disebut memiliki *presedensi lebih tinggi* dari penambahan.

Tanda kurung mengesampingkan presedensi apapun, jika jika kita tak puas dengan urutan implisit, kita bisa gunakan mereka untuk mengubahnya. Misalnya: `(1 + 2) * 2`.

Ada banyak operator di JavaScript. Tiap operator punya nomor presedensi masing-masing. Nomor yang lebih besar dieksekusi terlebih dahulu. Jika presedensinya sama, urutan eksekusinya dari kiri ke kanan.

Di sini adalah extrak dari [tabel presedensi](https://developer.mozilla.org/en/JavaScript/Reference/operators/operator_precedence) (kamu tak usah mengingat ini, tapi catat bahwa operator unary lebih tinggi dari binary terkait):

| Presedensi | Nama | Tanda |
|------------|------|------|
| ... | ... | ... |
| 16 | plus unary | `+` |
| 16 | negasi unary | `-` |
| 14 | perkalian | `*` |
| 14 | pembagian | `/` |
| 13 | penambahan | `+` |
| 13 | pengurangan | `-` |
| ... | ... | ... |
| 3 | penetapan | `=` |
| ... | ... | ... |

Seperti yang kita lihat, "plus unary" punya prioritas `16` yang lebih tinggi dari `13` "penambahan" (plus binary). Itulah kenapa, dalam expresi `"+apples + +oranges"`, plus unary bekerja sebelum penambahan.

## Penetapan

Mari ingat bahwa penetapan `=` juga merupakan operator. Ia terdaftar di tabel presedensi dengan prioritas sangat rendah `3`.

Itulah kenapa, ketika kita tetapkan variabel, seperti `x = 2 * 2 + 1`, kalkulasinya dilakukan pertama dan kemudian `=` dievaluasi, menyimpan hasilnya dalam in `x`.

```js
let x = 2 * 2 + 1;

alert( x ); // 5
```

Penetapan dapat dirantai:

```js run
let a, b, c;

*!*
a = b = c = 2 + 2;
*/!*

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

Penetapan berantai berevaluasi dari kanan ke kiri. Pertama, expresi paling kanan `2 + 2` dievaluasi dan ditetapkan ke variabel di sebelah kiri: `c`, `b` dan `a`. Pada akhirnya, semua variabel berbagi nilai tunggal.

````smart header="Operator penetapan `\"=\"` mengembalikan nilai"
Operator selalu mengembalikan nilai. Sudah jelas untuk kebanyakan operator seperti penambahan `+` atau perkalian `*`. Tapi operator penetapan mengikuti aturan ini juga.

Panggilan `x = value` menulis `value` ke dalam `x` *dan mengembalikannya*.

Ini adalah demo yang menggunakan penetapan sebagai bagian dari expresi yang rumit:

```js run
let a = 1;
let b = 2;

*!*
let c = 3 - (a = b + 1);
*/!*

alert( a ); // 3
alert( c ); // 0
```

Di contoh di atas, hasil dari `(a = b + 1)` ialah nilai yang ditetapkan ke `a` (yaitu `3`). Ia kemudian digunakan untuk pengurangan dari `3`.

Kode yang lucu, ya kan? Kita sebaiknya memahami cara ia bekerja, karena kadang kita lihat ia ada dalam librari pihak ke-3, tapi tak boleh menulis apapun seperti yang kita lakukan. Trik macam itu tentu saja tak membuat kode lebih jelas atau lebih terbaca.
````

## Remainder %

The remainder operator `%`, despite its appearance, is not related to percents.

The result of `a % b` is the remainder of the integer division of `a` by `b`.

Misalnya:

```js run
alert( 5 % 2 ); // 1 is a remainder of 5 divided by 2
alert( 8 % 3 ); // 2 is a remainder of 8 divided by 3
alert( 6 % 3 ); // 0 is a remainder of 6 divided by 3
```

## Exponentiation **

The exponentiation operator `**` is a recent addition to the language.

For a natural number `b`, the result of `a ** b` is `a` multiplied by itself `b` times.

Misalnya:

```js run
alert( 2 ** 2 ); // 4  (2 * 2)
alert( 2 ** 3 ); // 8  (2 * 2 * 2)
alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2)
```

Operator juga bekerja untuk angka non-integer.

Misalnya:

```js run
alert( 4 ** (1/2) ); // 2 (power of 1/2 is the same as a square root, that's maths)
alert( 8 ** (1/3) ); // 2 (power of 1/3 is the same as a cubic root)
```

## Increment/decrement

<!-- Can't use -- in title, because built-in parse turns it into – -->

Increasing or decreasing a number by one is among the most common numerical operations.

So, there are special operators for it:

- **Increment** `++` increases a variable by 1:

    ```js run no-beautify
    let counter = 2;
    counter++;      // works the same as counter = counter + 1, but is shorter
    alert( counter ); // 3
    ```
- **Decrement** `--` decreases a variable by 1:

    ```js run no-beautify
    let counter = 2;
    counter--;      // works the same as counter = counter - 1, but is shorter
    alert( counter ); // 1
    ```

```warn
Increment/decrement can only be applied to variables. Trying to use it on a value like `5++` will give an error.
```

The operators `++` and `--` can be placed either before or after a variable.

- When the operator goes after the variable, it is in "postfix form": `counter++`.
- The "prefix form" is when the operator goes before the variable: `++counter`.

Both of these statements do the same thing: increase `counter` by `1`.

Is there any difference? Yes, but we can only see it if we use the returned value of `++/--`.

Let's clarify. As we know, all operators return a value. Increment/decrement is no exception. The prefix form returns the new value while the postfix form returns the old value (prior to increment/decrement).

To see the difference, here's an example:

```js run
let counter = 1;
let a = ++counter; // (*)

alert(a); // *!*2*/!*
```

In the line `(*)`, the *prefix* form `++counter` increments `counter` and returns the new value, `2`. So, the `alert` shows `2`.

Now, let's use the postfix form:

```js run
let counter = 1;
let a = counter++; // (*) changed ++counter to counter++

alert(a); // *!*1*/!*
```

In the line `(*)`, the *postfix* form `counter++` also increments `counter` but returns the *old* value (prior to increment). So, the `alert` shows `1`.

To summarize:

- If the result of increment/decrement is not used, there is no difference in which form to use:

    ```js run
    let counter = 0;
    counter++;
    ++counter;
    alert( counter ); // 2, the lines above did the same
    ```
- If we'd like to increase a value *and* immediately use the result of the operator, we need the prefix form:

    ```js run
    let counter = 0;
    alert( ++counter ); // 1
    ```
- If we'd like to increment a value but use its previous value, we need the postfix form:

    ```js run
    let counter = 0;
    alert( counter++ ); // 0
    ```

````smart header="Increment/decrement among other operators"
The operators `++/--` can be used inside expressions as well. Their precedence is higher than most other arithmetical operations.

For instance:

```js run
let counter = 1;
alert( 2 * ++counter ); // 4
```

Compare with:

```js run
let counter = 1;
alert( 2 * counter++ ); // 2, because counter++ returns the "old" value
```

Though technically okay, such notation usually makes code less readable. One line does multiple things -- not good.

While reading code, a fast "vertical" eye-scan can easily miss something like `counter++` and it won't be obvious that the variable increased.

We advise a style of "one line -- one action":

```js run
let counter = 1;
alert( 2 * counter );
counter++;
```
````

## Bitwise operators

Bitwise operators treat arguments as 32-bit integer numbers and work on the level of their binary representation.

These operators are not JavaScript-specific. They are supported in most programming languages.

The list of operators:

- AND ( `&` )
- OR ( `|` )
- XOR ( `^` )
- NOT ( `~` )
- LEFT SHIFT ( `<<` )
- RIGHT SHIFT ( `>>` )
- ZERO-FILL RIGHT SHIFT ( `>>>` )

These operators are used very rarely. To understand them, we need to delve into low-level number representation and it would not be optimal to do that right now, especially since we won't need them any time soon. If you're curious, you can read the [Bitwise Operators](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) article on MDN. It would be more practical to do that when a real need arises.

## Modify-in-place

We often need to apply an operator to a variable and store the new result in that same variable.

For example:

```js
let n = 2;
n = n + 5;
n = n * 2;
```

This notation can be shortened using the operators `+=` and `*=`:

```js run
let n = 2;
n += 5; // now n = 7 (same as n = n + 5)
n *= 2; // now n = 14 (same as n = n * 2)

alert( n ); // 14
```

Short "modify-and-assign" operators exist for all arithmetical and bitwise operators: `/=`, `-=`, etc.

Such operators have the same precedence as a normal assignment, so they run after most other calculations:

```js run
let n = 2;

n *= 3 + 5;

alert( n ); // 16  (right part evaluated first, same as n *= 8)
```

## Comma

The comma operator `,` is one of the rarest and most unusual operators. Sometimes, it's used to write shorter code, so we need to know it in order to understand what's going on.

The comma operator allows us to evaluate several expressions, dividing them with a comma `,`. Each of them is evaluated but only the result of the last one is returned.

For example:

```js run
*!*
let a = (1 + 2, 3 + 4);
*/!*

alert( a ); // 7 (the result of 3 + 4)
```

Here, the first expression `1 + 2` is evaluated and its result is thrown away. Then, `3 + 4` is evaluated and returned as the result.

```smart header="Comma has a very low precedence"
Please note that the comma operator has very low precedence, lower than `=`, so parentheses are important in the example above.

Without them: `a = 1 + 2, 3 + 4` evaluates `+` first, summing the numbers into `a = 3, 7`, then the assignment operator `=` assigns    `a = 3`, and finally the number after the comma, `7`, is not processed so it's ignored.
```

Why do we need an operator that throws away everything except the last part?

Sometimes, people use it in more complex constructs to put several actions in one line.

For example:

```js
// three operations in one line
for (*!*a = 1, b = 3, c = a * b*/!*; a < 10; a++) {
 ...
}
```

Such tricks are used in many JavaScript frameworks. That's why we're mentioning them. But, usually, they don't improve code readability so we should think well before using them.
