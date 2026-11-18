# nro-45m-spectrometer

国立天文台 野辺山宇宙電波観測所の 45m 鏡の分光計の**運用リポジトリ**です。観測所でこの装置群をどう使い、どう保守しているかを集めます。文脈基盤のハブ [nro-context](https://github.com/nobeyama-radio-observatory/nro-context) から参照されます。

扱う装置とソフトウェア：

- SAM45（2009年度に導入した分光計。一部のアレイが故障し、4分の3で運用中）
- YATSUGATAKE（SAM45 の後継。2026年11月に試験的な科学運用を開始）
- SAM45 互換のソフトウェア（SAM45 の故障したアレイを YATSUGATAKE で肩代わりする。暫定）

## 位置づけ

文脈基盤では、装置の情報を次の四つの層に分けて置きます（ハブの判断記録 [0006](https://github.com/nobeyama-radio-observatory/nro-context/blob/main/decisions/0006-資産の情報を装置群ごとの運用リポジトリに置く.md)）。参照は上の層から下の層へだけ行います。

```
ハブ（nro-context）→ 運用（このリポジトリ）→ 製品 → 開発
```

- **このリポジトリが正本のもの：** 台帳（構成、依存関係、提供の状態、保守の状況、更新の見込み、担い手の数）、運用と保守の文書、聞き取りの記録。
- **製品と開発のリポジトリが正本のもの：** 装置そのものの設計、仕様、配布物、性能評価。ここには書き写さず、リンクで参照します。

| リポジトリ | 層 | 中身 |
|---|---|---|
| [YATSUGATAKE](https://github.com/nobeyama-radio-observatory/YATSUGATAKE) | 製品 | RFSoC 4x2 の上に作る電波分光計。配布する .bit と、その設計・仕様・性能評価 |
| [YATSUGATAKE-NRO45-sam45compat](https://github.com/nobeyama-radio-observatory/YATSUGATAKE-NRO45-sam45compat) | 製品（45m 鏡専用、暫定） | SAM45 の故障したアレイを YATSUGATAKE で肩代わりするソフトウェア。SAM45 を廃止した時点で archive する |
| [study-rfsoc](https://github.com/ars096/study-rfsoc) | 開発 | YATSUGATAKE の試作（projNNN）。仕上がったものを YATSUGATAKE に移す。観測所の組織ではなく個人のアカウントにある |

## 中身

| 場所 | 中身 |
|---|---|
| [assets.yaml](assets.yaml) | 台帳。項目の定義はハブの [assets/README.md](https://github.com/nobeyama-radio-observatory/nro-context/blob/main/assets/README.md) |
| [interviews/](interviews/README.md) | 聞き取りの記録。公開資料にない値（保守の手間、担い手の数、更新の見込みなど）の出典 |

台帳の `depends_on` と `part_of` にある id の置き場所は、ハブの[資産の索引](https://github.com/nobeyama-radio-observatory/nro-context/blob/main/assets/README.md)で引けます。`nro45m`（アンテナ）は [nro-45m-antenna](https://github.com/nobeyama-radio-observatory/nro-45m-antenna) にあります。`sw-cosmos`（観測制御）は [nro-45m-control](https://github.com/nobeyama-radio-observatory/nro-45m-control) にあります。`if-system`（IF 系）は [nro-45m-if](https://github.com/nobeyama-radio-observatory/nro-45m-if) にあります。

## 進め方

進め方の決まりの正本は、ハブの [CONTRIBUTING.md](https://github.com/nobeyama-radio-observatory/nro-context/blob/main/CONTRIBUTING.md) です。とくに次を守ってください。

- 機微情報を入れない。制御の手順、接続先、ネットワーク構成は、既存の非公開の場所に置いたままにする。
- 主ブランチに直接書き込まず、プルリクエストを出す。AI が作ったものにはラベル `AI作成` を付ける。
- 事実には出典を添える。出典を示せない事実は仮説として扱う（ハブの判断記録 [0004](https://github.com/nobeyama-radio-observatory/nro-context/blob/main/decisions/0004-事実の根拠は出典で示す.md)）。

担当：計算機グループ（[聞き取り 2026-11-18](interviews/2026-11-18.md) 問0、問9）

## 利用許諾

- コード：BSD 3-Clause License（[LICENSE](LICENSE)）
- 文書：クリエイティブ・コモンズ 表示 4.0 国際（CC BY 4.0、[LICENSE-docs](LICENSE-docs)）
