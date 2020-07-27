
Kamu bisa perhatikan berikut:

```js no-beautify
function pow(x,n)  // <- tak ada spasi between arguments
{  // <- menemukan bracket di baris terpisah
  let result=1;   // <- tak ada spasi sebelum atau setelah =
  for(let i=0;i<n;i++) {result*=x;}   // <- tak ada spasi
  // konten { ... } sebaiknya di baris baru
  return result;
}

<<<<<<< HEAD
let x=prompt("x?",''), n=prompt("n?",'') // <-- secara teknis memungkinkan,
// tapi lebih baik buat 2 baris, juga tak ada spasi dan kehilangan ;
if (n<0)  // <- tak ada spasi di dalam (n < 0), dan harus ada baris extra line di atasnya
{   // <- menemukan bracket di baris baru
  // di bawah - baris panjang bisa dipisah menjadi baris ganda untuk keterbacaan lebih baik
=======
let x=prompt("x?",''), n=prompt("n?",'') // <-- technically possible,
// but better make it 2 lines, also there's no spaces and missing ;
if (n<=0)  // <- no spaces inside (n <= 0), and should be extra line above it
{   // <- figure bracket on a separate line
  // below - long lines can be split into multiple lines for improved readability
>>>>>>> b0464bb32c8efc2a98952e05f363f61eca1a99a2
  alert(`Power ${n} is not supported, please enter an integer number greater than zero`);
}
else // <- bisa menulisnya di baris tunggal seperti "} else {"
{
  alert(pow(x,n))  // tak ada spasi dan kehilangan ;
}
```

Varian yang dibetulkan:

```js
function pow(x, n) {
  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}

let x = prompt("x?", "");
let n = prompt("n?", "");

if (n <= 0) {
  alert(`Power ${n} is not supported,
    please enter an integer number greater than zero`);
} else {
  alert( pow(x, n) );
}
```
