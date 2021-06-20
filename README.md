# kawakudari
 
https://user-images.githubusercontent.com/1715217/122657777-7e124b00-d1a1-11eb-908b-3490b8a49735.mp4

https://codeforkosen.github.io/kawakudari/
https://codeforkosen.github.io/kawakudari/#crt
https://codeforkosen.github.io/kawakudari/#pixel

a famous [IchigoJam](https://ichigojam.net/) game "[kawakudari](https://ichigojam.github.io/print/ja/KAWAKUDARI.html)" in JavaScript!

## program

just single HTML
```html
<!DOCTYPE html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width">
<title>kawakudari</title>
<script type="module">
import { onLoad, ticks, input, end, vec, rnd, addScore, remove, text, play } from "https://taisukef.github.io/crisp-game-lib/es/main.js";

window.title = "kawakudari";
window.description = `
[Hold]
move to right
`;
window.characters = [];
window.options = {
  isPlayingBgm: true,
  isReplayEnabled: true,
  seed: 0, // sound seed
  theme: document.location.hash.substring(1), // crt, pixel, dark
};

let y = 20;
let x = 50;
const enemy = [];
const dhit = 3;

window.update = () => { // canvas size 100x100
  if (!ticks) { // init
    enemy.length = 0;
  }
  if (input.isJustPressed) {
    play("select");
  }
  if (input.isPressed) {
    x++;
  } else {
    x--;
  }
  x = (x + 100) % 100;
  text("O", x, y);
  enemy.forEach(e => {
    text("*", e.x, e.y);
    e.y--;
    if (Math.abs(e.y - y) < dhit && Math.abs(e.x - x) < dhit) {
      end();
      play("explosion")
    };
  });
  if (ticks % 10 == 0) {
    enemy.push(vec(rnd(100), 100))
    addScore(1);
  }
  remove(enemy, (e) => e.y < -10);
};

window.addEventListener("load", onLoad);
</script>
</head>
</html>
 ```

## lib

- [crisp-game-lib by abagames](https://github.com/abagames/crisp-game-lib)

