lib フォルダ：外部ライブラリの写し（index.html と同じサーバーに置いて使う）
================================================================

外部のサイト（CDN）が止まっても動くように、使っているライブラリの写しをここに置いています。
index.html は、まずここから読み込み、読めない時だけ外部の場所から読み込みます。
このフォルダごと、index.html と同じ場所にアップロードしてください。


1. three.js（3D の土台）
------------------------
  置き場所：lib/three/
  元      ：code4fukui さんが公開している three.js
            https://github.com/code4fukui/three.js （dev ブランチ）
            コミット dfbc04ba4c4b6d875e6df3c8b5d2af726df2b0d9（2026-05-14）
            これまで index.html が読んでいた https://code4fukui.github.io/three.js/ と同じもの
  版      ：REVISION '166dev'（package.json の version は 0.165.0）
  ファイル：build/three.module.js
            examples/jsm/loaders/GLTFLoader.js
            examples/jsm/exporters/GLTFExporter.js
            examples/jsm/webxr/VRButton.js
            examples/jsm/webxr/ARButton.js
            examples/jsm/utils/BufferGeometryUtils.js（GLTFLoader が使う）
            examples/jsm/utils/TextureUtils.js（GLTFExporter が使う）
            どれも元のまま（書き換えていない）
  ライセンス：MIT（lib/three/LICENSE）

  読み込み方（index.html の import map の所）：
    1) lib/three/ から読む
    2) 読めなかった時は、このタブで1回だけ自動で読み直し、外部（code4fukui.github.io）から読む
    3) それでも読めない時は「よみこめませんでした」と「もういちど よみこむ」ボタンを出す
       （60秒たっても動き出さない時も、同じ案内を出す。あとから動き出したら消える）


2. model-viewer（かんたんAR・モデル画面の 3D の見本）
-----------------------------------------------------
  置き場所：lib/model-viewer/model-viewer.min.js
  元      ：npm の @google/model-viewer 4.4.0（dist/model-viewer.min.js。書き換えていない）
  ライセンス：Apache-2.0（lib/model-viewer/LICENSE）。NOTICE ファイルはありません
            このファイルの中には lit（BSD-3-Clause）・three.js r183（MIT）などが含まれていて、
            それぞれの著作権表示（@license）はファイルの中に残っています

  読み込み方（index.html の「モデル表示（model-viewer）の部品」の所）：
    1) lib/model-viewer/ から読む
    2) 読めなかった時は、外部（https://unpkg.com/@google/model-viewer@4.4.0/）の同じ版から読む
    3) それでも読めない時は「かんたんAR」だけ押せなくして、理由をボタンの下に出す
       （「ARで あそぶ」は押せる。モデル画面の 3D の見本が出ないだけ）

  ※ model-viewer は、圧縮した 3D モデル（Draco・KTX2）を表示する時だけ、
    その部品を外部（www.gstatic.com）から読みます。このアプリが作るモデルは圧縮していません。


3. もとから同じサーバーにあるもの（変えていない）
------------------------------------------------
  js-aruco2（ぬりえ・カードの読み取り）：coloring/lib/（読めない時は jsdelivr の 2.0.0）
  qrcode-generator 2.0.4（受け取りQR）：index.html の中に埋め込み


更新する時
----------
  ・three.js を替える時は lib/three/ のファイルを入れ替え、index.html の import map の所にある
    外部の場所（code4fukui.github.io）も、同じ版が読める場所にそろえてください。
  ・model-viewer を替える時は lib/model-viewer/model-viewer.min.js を入れ替え、
    index.html の外部の URL の版（@4.4.0）も同じ版にしてください。
  ・ライセンスのファイル（LICENSE）は消さずに、一緒に置いておいてください。


止まった時の動きを試すには
--------------------------
  Chrome の開発者ツール → Network → 右クリック「Block request URL」
  （または「Network request blocking」）で、lib/three や unpkg.com などを止めて読み込み直すと、
  外部への切り替えや案内を確かめられます。
  外部に切り替わったタブを元に戻すには、タブを開き直してください。
