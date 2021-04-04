---
title: "JAMstackで技術ブログを作った話【Next.js ✖️ microCMS ✖️ Vercel】"
emoji: "📚"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: [nextjs, microcms, vercel, figma]
published: true
---

今回、Next.js, micoroCMS, Vercel を用いて JAMstack の技術ブログを作りましたので、そのお話をいたします。

作成したブログは[こちら](https://www.nochitoku-it.com/)
ソースコードは[こちら](https://github.com/YukiOnishi1129/nochitoku-blog)
![NOCHITOKU](https://images.microcms-assets.io/assets/07ff07e8d1244dd1984512c2a5431805/d4e0072141cf4b1fafd57356714d9e04/about.png)

# 私はこんなやつ

モダンフロントを中心に活躍しているフリーランスエンジニアです。
エンジニアについての詳細なプロフィールはこちらにまとめていますので、良ければご覧ください。
[プロフィール | NOCHITOKU](https://www.nochitoku-it.com/profile)

# なぜ作ったのか？

以下の理由で作成しています。

- **技術ノウハウの発信場所**
- **SSG のアウトプット**

私自身スキルのキャッチアップの中で、個人ブログの知見により救われたことが多くありました。
そこで、**自分でも他のエンジニアの方の役に立とうと思い**、個人ブログの開発に至りました。

ブログコンセプトなどはこちらにまとめていますので、良ければご覧ください。
[「NOCHITOKU ブログ」について](https://www.nochitoku-it.com/about)

また、React, Next.js をメインに仕事をしているので、SSG 構成のアウトプットを兼ねて開発しています。
現状は SSG 構成ですが、今後 ISR 化や E2E テストの導入など、保守体制の構築にも力を入れていこうと思います。

# ブログの機能

一般的なブログの機能に加えて、PWA の機能があります。

- **ブログ一覧、記事詳細**
- **検索**
- **カテゴリー検索**
- **アーカイブ検索**
- **プロフィール**
- **利用規約**
- **プライバシーポリシー**
- **PWA**

## PWA 機能について

### スマートフォン (iPhone, Android)

ブログサイトを「ホーム画面に追加」することで、ネイティブアプリのように操作することができます。
![](https://storage.googleapis.com/zenn-user-upload/chkqq2btt7jgt3pdzvh89hubrdwy =250x)

### PC ブラウザ (Mac)

ブログサイトにブラウザからアクセスします。
URL の右の方にあるアイコンをクリックし、「NOCHITOKU」ブログをインストールします。
![](https://storage.googleapis.com/zenn-user-upload/e1j7eyxqjcwaz7ui0a6nmuza3dxt)
すると画像のようなデスクトップアプリとして、ブログサイトを操作できるようになります。
![](https://storage.googleapis.com/zenn-user-upload/ho2c3cphgx08sekg3sz89gj8fl3x)

# システム構成

以下の構成にて、技術ブログを構築しています。

![](https://storage.googleapis.com/zenn-user-upload/citgvqslnvxfnz3li8h5ybnxpixe)

ホスティングは Vercel で実施しています。
Github との連携で、main リポジトリ push 時に自動デプロイが実行されるようになっています。
また macroCMS と連携しており、**webhook を用いて記事を公開するタイミングでも同様に自動デプロイが実行**されます。

今回 SSG を採用しており、ビルド時に microCMS から API にて記事データを取得し、静的ファイルを生成するようにしています。
そのため画面遷移時の同期通信などは発生せず、快適な操作性を実現しています。

# 開発の流れ

## 要件定義・WF 作成 (半月)

ブログコンセプトの決定とデザインの WF(ワイヤーフレーム)作成に注力しました。
デザインは妻に外注しています。
**妻は現在、未経験から UI・UX デザイナーへの転職活動をしており、今回のブログデザインは良いポートフォリオになると思いお願いしました。**
おしゃれで使いやすい UI のデザインを作成してくれて大満足です！

PC のみならずレスポンシブのデザインも作成していただきました。
■PC
![](https://storage.googleapis.com/zenn-user-upload/dtoe0ipvgs9uzybz5bffeicjf1x9)

■ レスポンシブ
![](https://storage.googleapis.com/zenn-user-upload/mj4ef76g01710wo78ybv5wwhu43g)

またデザインツールに「**Figma**」を使用しています。
Figma は以下の 2 点が魅力的で、チーム開発において最適なデザインツールだと捉えています。

- **コンポーネント単位にパーツを分割し、再利用できる**
- **複数人でデザインを共有し同時操作ができる**

今回のブログデザインもコンポーネントを作成し再利用することで効率的に開発することができました。

## 設計・開発・デプロイ(1 ヶ月)

WF 完成後、妻が本格的なデザインカンプを作成するのと並行して、私の方で技術ブログの開発に取り組みました。
スキルスタックは以下の通りです。

- **Next.js**
- **TypeScript**
- **CSS Modules**
- **jest**, **testing-library**
- **Storybook**
- **eslint**, **prittier**

またその他ライブラリとして、以下のものを導入しています。

- **dayjs**
- **axios**
- **react-anchor-link-smooth-scroll** // ページ内リンク
- **react-modal** // モーダル表示
- **react-scroll** // ページトップへ遷移するためのライブラリ
- **react-share** // SNS シェアボタン
- **cheerio** // microCMS の記事データを変換
- **highlight.js** // 記事内のコードをハイライト

設計方針や構成などは後ほど[「NOCHITOKU ブログ」](<(https://www.nochitoku-it.com/)>)で発信する予定です。
また Github にコードは公開していますので、ご興味がありましたらご覧ください。

[YukiOnishi1129/nochitoku-blog](https://github.com/YukiOnishi1129/nochitoku-blog)

# 役にたった記事紹介

開発時に助けられた記事を紹介いたします。

## [Next.js に CSS Modules を導入する](https://zenn.dev/catnose99/scraps/5e3d51d75113d3)

CSS Modules を Next.js に導入する際にとても参考になりました。
CSS 変数の扱い方、メディアクエリの共有方法、絶対パスの指定方法など助けられました。

## [Nest.js + Storybook + Bulma 環境構築メモ](https://zenn.dev/kobayashi_m42/scraps/41aae5f3091204)

Storybook に CSSmodules を導入する際の方法です。
「sass-loader」のバージョンが v10.1.1 にしないと、Storybook 側でエラーが発生するので注意です。(Storybook が v6 の場合)

## [How To Import SVGs into NextJS](https://medium.com/frontend-digest/how-to-import-svgs-into-nextjs-8ec6100e613f)

Next.js で svg を使用する設定です。
いくつか方法はありますが、私は以下の方法を取っています。

- 「babel-plugin-inline-react-svg」を install → .babelrc に設定
- index.d.ts に svg の型定義を追加

## [Next.js でサクッと PWA 対応](https://qiita.com/NozomuTsuruta/items/8991707ff549b1552e78)

Next.js に PWA 対応を導入する方法です。
「next-pwa」というライブラリが良く使われているので、こちらを採用しました。

## [Next.js の Preview Mode ＋ Vercel でプレビュー機能を実現する](https://blog.microcms.io/nextjs-preview-mode/)

microCMS 側で記事を下書きした場合のプレビュー機能の設定です。
結構難しかったですが、micoroCMS 社が記事にしてくれていたので、詰まることなく進めることができました。
プレビュー機能を導入する際も、ホスティングは Vercel にした方が構築は楽でしたね。

## [Using NextJS with Google Analytics and TypeScript](https://medium.com/frontend-digest/using-nextjs-with-google-analytics-and-typescript-620ba2359dea)

Next.js に Google Analytics を適用させる方法です。
gtag の型定義ライブラリである「@types/gtag.js」をインストールすることで簡単に設定できます。

## [Next.js(SSG)でページネーションを実装してみよう](https://blog.microcms.io/next-pagination/)

ブログ記事一覧ページのページネーションの構築方法がまとめられています。
getStaticPath で動的ページの作成、getStaticProps でデータ取得、ページネーションコンポーネントの作成など、結構複雑でしたが記事があって助かりました。

## [Next.js アプリを Vercel で公開して、独自ドメインに反映する](https://qiita.com/Niceguy1234567890/items/48923a766f101425a677)

XSERVER で取得したドメインを Vercel に割り当てる方法です。
こちらはサブドメインの割り当てですが、オリジンドメインを XSERVER 側で設定し、ネームサーバを Vercel に設定し直せばいけました。
この辺りもいつか NOCHITOKU ブログでまとめようと思います。

# 最後に

以上、JAMstack な技術ブログを開発した話でした。
SSG に関しては初めての実装だったので戸惑うことが多かったですが、数多くの技術記事のおかげで完成まで到達することができました。
私も「NOCHITIOKU」ブログで技術ノウハウを発信していき、同じように苦しんでいるエンジニアの方々の手助けをしていこうと思います。
「NOCHITOKU」ブログでは実践的な技術ノウハウを中心に発信していきますので、ぜひご覧になってみてください！

[「NOCHITOKU ブログ」について](https://www.nochitoku-it.com/about)

また私の妻が現在 UI・UX デザイナーへの転職活動をしております。
このブログのデザインを 1 から全て担当しており、もしご興味がありましたら以下のアカウント宛に DM いただければ幸いです。

[@shio_design](https://twitter.com/shio_design)
