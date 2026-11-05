# rubik_adat

Tanítóadat a `rubik_kocka` projekt lapdetektorához (YOLO11n-seg, egy osztály: `face`).
A Colab innen húzza az adatot (GitHub: `borsz05/rubik_adat`).

```
synth/v1/        szintetikus (Blender), YOLO-seg formátum
  data.yaml
  images/{train,val}/*.jpg
  labels/{train,val}/*.txt     soronként: 0 x1 y1 x2 y2 …  (normalizált poligon)
  meta/{train,val}/*.json      pontos sarkok (0,2,8,6 matrica felől), 54 matrica, kamera, torzítás
real/            valódi webkamerás felvételek (6. fázis)
assets/hdri/     Poly Haven HDRI-k (CC0) — nincs a gitben, tools/fetch_hdri.py tölti le
raw/             Blender nyers kimenet — nincs a gitben, a synth_post.py ebből dolgozik
```

Előállítás (a `rubik_kocka` mappából):

```bat
tools\render_synth.bat 2000 1
tools\render_synth.bat 300 9
.venv\Scripts\python tools\synth_post.py --raw ..\rubik_adat\raw\s1 ..\rubik_adat\raw\s9 --out ..\rubik_adat\synth\v1 --val-seeds 9
.venv\Scripts\python tools\synth_preview.py ..\rubik_adat\synth\v1 --out ..\rubik_adat\synth\v1_preview.jpg
```

A val egy teljes seed (más jelenetek, más kockák), nem véletlen képek a trainből.
