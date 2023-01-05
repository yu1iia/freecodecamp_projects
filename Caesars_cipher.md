###  Caesars Cipher

One of the simplest and most widely known ciphers is a Caesar cipher, also known as a shift cipher. In a shift cipher the meanings of the letters are shifted by some set amount.

A common modern use is the ROT13 cipher, where the values of the letters are shifted by 13 places. Thus A ↔ N, B ↔ O and so on.

Write a function which takes a ROT13 encoded string as input and returns a decoded string.

All letters will be uppercase. Do not transform any non-alphabetic character (i.e. spaces, punctuation), but do pass them on.

## Code

```javascript
function rot13(str) {
 
  const Acode = 'A'.charCodeAt();
  const Ncode = 'N'.charCodeAt();
  const Zcode = 'Z'.charCodeAt();
  return [...str]
    .map(function (e) {
      const code = e.charCodeAt();
      if (Acode <= code && code <= Zcode) {
        if (code < Ncode) {
          return String.fromCharCode(code + 13);
        } else {
          return String.fromCharCode(code - 13);
        }
      } else {
        return e;
      }
    })
    .join('');
}

rot13('SERR PBQR PNZC');
```
