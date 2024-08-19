# D2 Send Eagle

ComfyUIで生成した画像を画像管理ソフト [Eagle](https://en.eagle.cool/) に送るカスタムノードです。

[ComfyUI-send-eagle-slim](https://github.com/shingo1228/ComfyUI-send-eagle-slim) という既存のカスタムノードを自分の好みに拡張したものです。素晴らしいカスタムノードを制作してくださった Shingo.T 様に感謝です。

<img src="img/image.png">


## サンプルワークフロー

<img src="img/sample_workflow.png">


## 主な機能

- `image` で受け取った画像を Eagle に送信する
- `positive`、`negative` で受け取ったテキストを Eagle のメモとして記録する
- 画像の上の入力欄に記入したテキストも Eagle のメモとして記録する
- `format`: 保存形式を Webp / PNG から選択
- `lossless_webp`: Webp は可逆（lossless）か不可逆（lossy）から選択
- `compression`: lossyの時の圧縮率を指定
- `save_tags`: Eagle のタグとして保存するか選択
  - `None`: 保存しない
  - `Prompt + Checkpoint`: プロンプトとモデル名を保存
  - `Prompt`: プロンプトを保存
  - `Checkpoint`: モデル名を保存
- `filename_template`: 保存ファイル名のテンプレート。`{}` 内に該当パラメータが入る
  - 初期設定：`{model}-{width}-{height}-{seed}`
  - `{model}`: checkpoint名
  - `{width}` `{height}`: 画像の幅、高さ
  - `{steps}`: 生成ステップ数
  - `{seed}`: 生成シード
- `eagle_folder`: Eagleのフォルダ名、またはフォルダIDを指定。フォルダが存在しなければ新規作成する


## その他の機能

Eagleに送信する他に、ローカル環境の下記フォルダにも画像を保存します。
このフォルダ名は変更できません。

`./ComfyUI/output/YYYY-MM-DD/YYYYMMDD_HHMMss_SSSSSS-{FinalImage_width}-{FinalImage_height}.webp`


## インストール

### ComfyUI Manager を使う場合

1. ComfyUI Manager を開く
2. `Custom Nodes Manager` をクリック
3. `D2 Send Eagle` を検索
4. `Install` をクリック
5. ComfyUI を再起動

### コマンドプロンプトを使う場合

1. コマンドプロンプトを開く
1. `{ComfyUIインストールフォルダ}/custom_nodes` に移動
2. `git clone https://github.com/da2el-ai/ComfyUI-d2-send-eagle`


## 制限事項
PNGInfo の保存は下記のノードに対応しています。それ以外のノードでは情報を取得できません。

- Sampler：`KSampler`,`KSamplerAdvanced`
- Latentイメージ：`Empty Latent Image`
- CLIP：`ClIP TextEncoder(Prompt)`,`CLIPTextEncodeSDXL`
- Latentイメージ: [ComfyUI-SDXL-EmptyLatentImage](https://github.com/shingo1228/ComfyUI-SDXL-EmptyLatentImage)
- Sampler: `KSampler With Refiner (Fooocus)`
- Sampler: [BNK_TiledKSampler](https://github.com/BlenderNeko/ComfyUI_TiledKSampler)
- Prompt: `SDXL Prompt Styler`


## 変更履歴
- 2024/08/19
  - Unet Loaderを使った時にモデル名を取得できないのを修正
- 2024/08/04
  - とりあえず公開
