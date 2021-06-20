# kawakudari

https://user-images.githubusercontent.com/1715217/122673126-03c9e100-d20a-11eb-90db-949f6b52527a.mp4

## demo

- https://codeforkosen.github.io/kawakudari/

a famous [IchigoJam](https://ichigojam.net/) game "[kawakudari](https://ichigojam.github.io/print/ja/KAWAKUDARI.html)" in JavaScript!

## theme

- https://codeforkosen.github.io/kawakudari/#crt
- https://codeforkosen.github.io/kawakudari/#pixel
- https://codeforkosen.github.io/kawakudari/#dark

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

- [crisp-game-lib ES module version](https://github.com/taisukef/crisp-game-lib) forked from [crisp-game-lib by abagames](https://github.com/abagames/crisp-game-lib)

## 解説ブログ

- シンプルでかわいいミニゲームをブラウザのみでサクッと作ろう、crisp-game-libでかわくだり！](https://fukuno.jig.jp/3251)

