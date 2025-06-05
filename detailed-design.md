## ログイン・サインイン


```mermaid
flowchart TD
    A[アプリ起動] --> B{初回起動?}
    B -->|Yes| C[チュートリアル表示]
    B -->|No| D[スプラッシュ画面]
    
    C --> E[ログイン/サインアップ選択画面]
    D --> F{ログイン状態確認}
    
    F -->|ログイン済み| G[メイン画面へ]
    F -->|未ログイン| E
    
    E --> H{ユーザー選択}
    H -->|ログイン| I[ログイン画面]
    H -->|サインアップ| J[サインアップ画面]
    
    I --> K[メールアドレス入力]
    K --> L[パスワード入力]
    L --> M[ログインボタンタップ]
    M --> N{認証処理}
    
    N -->|成功| O[ログイン成功]
    N -->|失敗| P[エラーメッセージ表示]
    P --> I
    
    J --> Q[ユーザー名入力]
    Q --> R[メールアドレス入力]
    R --> S[パスワード入力]
    S --> T[パスワード確認入力]
    T --> U[利用規約同意]
    U --> V[サインアップボタンタップ]
    V --> W{バリデーション}
    
    W -->|OK| X[アカウント作成処理]
    W -->|NG| Y[エラーメッセージ表示]
    Y --> J
    
    X --> Z{作成結果}
    Z -->|成功| AA[確認メール送信]
    Z -->|失敗| BB[エラーメッセージ表示]
    BB --> J
    
    AA --> CC[メール確認待ち画面]
    CC --> DD[メール内リンククリック]
    DD --> EE[アカウント有効化]
    EE --> O
    
    O --> G[メイン画面へ]
    
    %% ソーシャルログイン
    E --> FF[ソーシャルログイン選択]
    FF --> GG{プロバイダー選択}
    GG -->|Google| HH[Google認証]
    GG -->|Apple| II[Apple認証]
    GG -->|Twitter| JJ[Twitter認証]
    
    HH --> KK{Google認証結果}
    II --> LL{Apple認証結果}
    JJ --> MM{Twitter認証結果}
    
    KK -->|成功| O
    LL -->|成功| O
    MM -->|成功| O
    
    KK -->|失敗| NN[ソーシャルログインエラー]
    LL -->|失敗| NN
    MM -->|失敗| NN
    
    NN --> E
```

## オジモンシステム

```mermaid
flowchart TD
    A[ログイン成功] --> B[ホーム画面]
    
    %% ホーム画面のメニュー
    B --> C{メニュー選択}
    C -->|メール| D[メール画面]
    C -->|マップ| E[観光地画面]
    C -->|お気に入りキャラ| F[お気に入りキャラ表示]
    C -->|ガチャ| G[ガチャ画面]
    C -->|バトル| H[バトル画面]
    C -->|図鑑| I[図鑑画面]
    
    %% 図鑑画面
    I --> J[オジモン一覧表示]
    J --> K{オジモン状態}
    K -->|ゲット済み| L[通常表示]
    K -->|未ゲット| M[灰色表示]
    
    J --> N[フィルター機能]
    N --> O{フィルター条件}
    O -->|レア度| P[レア度別表示]
    O -->|タイプ| Q[タイプ別表示]
    O -->|ゲット状況| R[ゲット状況別表示]
    
    P --> J
    Q --> J
    R --> J
    
    J --> S[お気に入り選択]
    S --> T[お気に入り登録/解除]
    T --> J
    
    L --> U[オジモンタップ]
    U --> V[図鑑詳細画面]
    
    %% 図鑑詳細画面
    V --> W[オジモン詳細表示]
    W --> X[オジモン画像]
    W --> Y[名前表示]
    W --> Z[趣味表示]
    W --> AA[特技表示]
    W --> BB[好きな店表示]
    
    %% 観光地画面
    E --> CC[観光地マップ表示]
    CC --> DD[ピン表示]
    DD --> EE[ピンクリック]
    EE --> FF[店舗情報モーダル]
    FF --> GG[店舗詳細表示]
    FF --> HH[利用可能クーポン表示]
    
    %% バトル画面
    H --> II[オンラインカード対戦]
    II --> JJ{対戦相手検索}
    JJ -->|マッチング成功| KK[対戦開始]
    JJ -->|マッチング失敗| LL[再検索]
    LL --> JJ
    
    KK --> MM[カード対戦実行]
    MM --> NN{対戦結果}
    NN -->|勝利| OO[勝利報酬獲得]
    NN -->|敗北| PP[経験値獲得]
    
    %% ガチャ画面
    G --> QQ[ガチャ種類選択]
    QQ --> RR{ガチャタイプ}
    RR -->|ノーマルガチャ| SS[ノーマルガチャ実行]
    RR -->|プレミアムガチャ| TT[プレミアムガチャ実行]
    RR -->|イベントガチャ| UU[イベントガチャ実行]
    
    SS --> VV[ガチャ結果表示]
    TT --> VV
    UU --> VV
    
    VV --> WW[新規オジモン獲得確認]
    WW -->|新規| XX[図鑑登録]
    WW -->|重複| YY[強化素材変換]
    
    %% 移動先一覧（共通）
    I --> ZZ[移動先一覧]
    E --> ZZ
    H --> ZZ
    G --> ZZ
    V --> ZZ
    
    ZZ --> AAA{移動先選択}
    AAA -->|ホーム| B
    AAA -->|図鑑| I
    AAA -->|観光地| E
    AAA -->|バトル| H
    AAA -->|ガチャ| G
    
    %% 図鑑詳細へのアクセス（どこからでも）
    F --> V
    GG --> V
    OO --> V
    PP --> V
    XX --> V
    
    %% メール機能
    D --> BBB[受信メール一覧]
    BBB --> CCC[メール詳細]
    CCC --> DDD{メール種類}
    DDD -->|システム通知| EEE[通知内容表示]
    DDD -->|イベント情報| FFF[イベント詳細表示]
    DDD -->|報酬メール| GGG[報酬受取]
    
    GGG --> HHH[アイテム獲得]
    HHH --> B
```

## オジモンシステムV2

```mermaid
flowchart TD
 A[ログイン成功] --> B[ホーム画面]

 %% ホーム画面のメニュー
 B --> C{メニュー選択}
 C -->|メール| D[メール画面]
 C -->|マップ| E[観光地画面]
 C -->|お気に入りキャラ| F[お気に入りキャラ表示]
 C -->|ガチャ| G[ガチャ画面]
 C -->|バトル| H[バトル画面]
 C -->|図鑑| I[図鑑画面]

 %% 図鑑画面
 I --> J[オジモン一覧表示]
 J --> K{オジモン状態}
 K -->|ゲット済み| L[通常表示]
 K -->|未ゲット| M[灰色表示]

 J --> N[フィルター機能]
 N --> O{フィルター条件}
 O -->|レア度| P[レア度別表示]
 O -->|タイプ| Q[タイプ別表示]
 O -->|ゲット状況| R[ゲット状況別表示]

 P --> J
 Q --> J
 R --> J

 J --> S[お気に入り選択]
 S --> T[お気に入り登録/解除]
 T --> J

 L --> U[オジモンタップ]
 U --> V[図鑑詳細画面]

 %% 図鑑詳細画面
 V --> W[オジモン詳細表示]
 W --> X[オジモン画像]
 W --> Y[名前表示]
 W --> Z[趣味表示]
 W --> AA[特技表示]
 W --> BB[好きな店表示]
 %% 既定遷移：図鑑詳細→図鑑一覧へ戻る
 V --> I

 %% 観光地画面
 E --> CC[観光地マップ表示]
 CC --> DD[ピン表示]
 DD --> EE[ピンクリック]
 EE --> FF[店舗情報モーダル]
 FF --> GG[店舗詳細表示]
 FF --> HH[利用可能クーポン表示]

 %% バトル画面
 H --> II[オンラインカード対戦]
 II --> JJ{対戦相手検索}
 JJ -->|マッチング成功| KK[対戦開始]
 JJ -->|マッチング失敗| LL[再検索]
 LL --> JJ

 KK --> MM[カード対戦実行]
 MM --> NN{対戦結果}
 NN -->|勝利| OO[勝利報酬獲得]
 NN -->|敗北| PP[経験値獲得]
 %% 既定遷移：バトル終了→ホームのバトル画面へ戻る
 OO --> H
 PP --> H

 %% ガチャ画面
 G --> QQ[ガチャ種類選択]
 QQ --> RR{ガチャタイプ}
 RR -->|ノーマルガチャ| SS[ノーマルガチャ実行]
 RR -->|プレミアムガチャ| TT[プレミアムガチャ実行]
 RR -->|イベントガチャ| UU[イベントガチャ実行]

 SS --> VV[ガチャ結果表示]
 TT --> VV
 UU --> VV

 VV --> WW[新規オジモン獲得確認]
 WW -->|新規| XX[図鑑登録]
 WW -->|重複| YY[強化素材変換]

 %% 移動先一覧（共通）
 I --> ZZ[移動先一覧]
 E --> ZZ
 H --> ZZ
 G --> ZZ
 V --> ZZ

 ZZ --> AAA{移動先選択}
 AAA -->|ホーム| B
 AAA -->|図鑑| I
 AAA -->|観光地| E
 AAA -->|バトル| H
 AAA -->|ガチャ| G

 %% 図鑑詳細へのアクセス（どこからでも）
 F --> V
 GG --> V
 OO --> V
 PP --> V
 XX --> V

 %% メール機能
 D --> BBB[受信メール一覧]
 BBB --> CCC[メール詳細]
 CCC --> DDD{メール種類}
 DDD -->|システム通知| EEE[通知内容表示]
 DDD -->|イベント情報| FFF[イベント詳細表示]
 DDD -->|報酬メール| GGG[報酬受取]

 GGG --> HHH[アイテム獲得]
 HHH --> B
```

## オジモンシステムV3

```mermaid
flowchart TD
    A[ログイン成功] --> B[ホーム画面]
    
    %% ホーム画面のメニュー
    B --> C{メニュー選択}
    C -->|メール| D[メール画面]
    C -->|マップ| E[観光地画面]
    C -->|お気に入りキャラ画像| F[お気に入りキャラ表示]
    C -->|ガチャ| G[ガチャ画面]
    C -->|バトル| H[バトル画面]
    C -->|図鑑| I[図鑑画面]
    
    %% 図鑑画面
    I --> J[オジモン一覧表示]
    J --> K{オジモン状態}
    K -->|ゲット済み| L[通常表示]
    K -->|未ゲット| M[灰色表示]
    
    J --> N[フィルター機能]
    N --> O{フィルター条件}
    O -->|レア度| P[レア度別表示]
    O -->|タイプ| Q[タイプ別表示]
    O -->|ゲット状況| R[ゲット状況別表示]
    
    P --> J
    Q --> J
    R --> J
    
    J --> S[お気に入り選択]
    S --> T[お気に入り登録/解除]
    T --> J
    
    L --> U[オジモンタップ]
    U --> V[図鑑詳細画面]
    
    %% 図鑑詳細画面
    V --> W[オジモン詳細表示]
    W --> X[オジモン画像]
    W --> Y[名前表示]
    W --> Z[趣味表示]
    W --> AA[特技表示]
    W --> BB[好きな店表示]
    
    %% 観光地画面
    E --> CC[観光地マップ表示]
    CC --> DD[ピン表示]
    DD --> EE[ピンクリック]
    EE --> FF[店舗情報モーダル]
    FF --> GG[店舗詳細表示]
    FF --> HH[利用可能クーポン表示]
    
    %% バトル画面
    H --> II[オンラインカード対戦]
    II --> JJ{対戦相手検索}
    JJ -->|マッチング成功| KK[対戦開始]
    JJ -->|マッチング失敗| LL[再検索]
    LL --> JJ
    
    KK --> MM[カード対戦実行]
    MM --> NN{対戦結果}
    NN -->|勝利| OO[勝利報酬獲得]
    NN -->|敗北| PP[経験値獲得]
    
    %% バトル終了後の処理（仕様に合わせて修正）
    OO --> H
    PP --> H
    
    %% ガチャ画面
    G --> QQ[ガチャ種類選択]
    QQ --> RR{ガチャタイプ}
    RR -->|ノーマルガチャ| SS[ノーマルガチャ実行]
    RR -->|プレミアムガチャ| TT[プレミアムガチャ実行]
    RR -->|イベントガチャ| UU[イベントガチャ実行]
    
    SS --> VV[ガチャ結果表示]
    TT --> VV
    UU --> VV
    
    VV --> WW[新規オジモン獲得確認]
    WW -->|新規| XX[図鑑登録]
    WW -->|重複| YY[強化素材変換]
    
    %% ガチャ結果後はガチャ画面に戻る
    XX --> G
    YY --> G
    
    %% 移動先一覧（各画面から共通）
    I --> ZZ[移動先一覧]
    E --> ZZ
    H --> ZZ
    G --> ZZ
    V --> ZZ
    D --> ZZ
    
    ZZ --> AAA{移動先選択}
    AAA -->|ホーム| B
    AAA -->|図鑑| I
    AAA -->|観光地| E
    AAA -->|バトル| H
    AAA -->|ガチャ| G
    AAA -->|メール| D
    
    %% メール機能（移動先一覧を追加）
    D --> BBB[受信メール一覧]
    BBB --> CCC[メール詳細]
    CCC --> DDD{メール種類}
    DDD -->|システム通知| EEE[通知内容表示]
    DDD -->|イベント情報| FFF[イベント詳細表示]
    DDD -->|報酬メール| GGG[報酬受取]
    
    GGG --> HHH[アイテム獲得]
    HHH --> D
    
    %% モーダル閉じる処理
    FF --> |モーダル閉じる| E
```

## オジモンシステム　クラス図

[![](https://mermaid.ink/img/pako:eNqtWetu2zYUfhVDwAAXS4pc3FyMroBjK6mG2A5kt1kHAwEjMTZbidJ0yWVFgnXAhg39s18bsBfYQ-zH3qVFf-wtdkhKFilRdlIvRRvxnMND8vA7hx_Zt4YTuNhoG46H4rhH0DRC_oQ24IdLGi9iHDXeCgn7WU9BYLntxiiJCJ2WFBT5WKPCPiKeRu4FU0JHCUrSuN04CAIPIyqpL9BlEJEEd2coQk6CI7A6JnFyN3xN_IDeFaZfck_NRxovTBWkCdNdBsSVFMh1D7MRmgH32G4Iz1XbCPvBJb63-RQnuW3MRq7O-hZ-yXF-Hvh45EQY00q023wTJO8uiUMP3fQxTTXLouiSTFGCx0Efor7EIFyoV9ZQa3WEnBlaaHGAksTDC01OgjfYxdeqTTlIIoJKgMROaAFZA0bio6lOPgvOz2808jjEDkHe6A3xdBjOQTqaBaFGHSFQglub_x7fhFhSJtDMQVRSkXh4niBCsavDNOCrh0Ht8Z0RDjKBZBUXKGySOP-c-1sY6mw_NJAUEWeIrsvG9QviQbZ22WgRQe3GodKuInk4d6lL0zD0boSHplPjstorCaZT7_4JWwBRhHFph3gWXA1EJxLQairWxFN410Q1xh6GEucOlXHrQiVtvmZeFkN4s27Ofp3qOUuAGt1ISoIak0MpEZqrB2wcpBGJfU2ofBT2UAIY6IsPSRUSmp8Rx4HDRzohykGR105UN0ew18WVO-p6xHnThEFgjMK93k8_cJHXhK_QohcBVIbsa_XISEMrcYF5aeugB9ZJ6kLi94L03MPKAUyndbrq1JVwiFhoj77cnmnVvuWl5Fo1FZjwAQXdxTHUhZCFRKOFUz7CcazTXEIOIVh0N0jDYA4c0bqrrbZlP0ydeZgf9YqP8qKFUlmyw0XaRcPeeQ9fNcAcfNLERolub_F1SKKbnlDCv8rBA2xDe-iQ-CXyiKtnWUBUFqNWcABNOp8LxU2cYL-dm_GWnCMJipIh9eBArCUTMUaRMxuGEElMk_-hBMlzUTMNKgiONsvELJNvVeTZEhMe74OiISMgjSKY9TiNaIXv-ShxZifcd6yPPg9PbWDwNXZSONvAdxN4NEeMMO7wlqYHdQtv4svGceolCiVOwGFO7hh_vU80hRslmleE0irLhdqk4b7rEb5CkZvnqs1bdyqygRBg6kCkLZrgqRJJSNVTPhqbainKoBPuijSuuGdG5nwEZqeMUV4yZ8YayE-ZnBG-fB1HuUBzVM11cf3WCgou6OTc_lH2Xdm5h-bB3KOyCDbaQ8q0EzDGWNkTYMgATVaG5ViwunVXXWezdk28CAv-uHxLNCAMMrZdx7-gLg7wle6WugSRbGbCWUHVlaIKbgt9NbXDKHDg_BJTXrxPfT21ZJdvia4zKy0jElY67hNiyu-S4hrPPlcvrsxLZZpaPMVQjVglqCrS89dAmrVYAwxQnYaNMuZ50s--ZEaQJAAP7NpLigyB7UC6MxJOax9DMfbD8rkKRTx60-H9NBGGkBB_YfUph08NtRxI6S5TLcr3uXWXbDIivuoFf_krQfW5orxo9dKnoOdz79l53uevUEOlXXMNrbsC3-ulR2yrOnku0tM_PnXRpzT171JEE77oalElnExZKoniKKuL8BdfNEya-rEy1Xkw2XSfPgWk-TjiqHv2rHDcHfb7w0HRtju2WbRGL05M-0yVHZtH5qDXsV8teudZOu6hJfs87YxNu2ge2Z3RqGiax2Z3bFvdQjIY2v3OcX1xWjr86NVobPbPBsOxdWh1O2NLjoH50hyMz6zB4VCKi3nasXtn_Y51vJBwMmq4cOTTjjW2BkeFwBqcndjDI9uUl3xoDazRc7O3CIZLFzn82lL21oIlSzv_wrbNQfeVtO5vYLctkJk1W6vk1-KhD8Yda5DPX2zZ-Kwq7RwX4WR_AMlffc4P72ljj08knpEwbjQ-_PD3h59_-_TPTx_f_fnplz8aG42P795__PHXf39__-mv96uMxR_WswfNdiN_RYzZAqS34PX1ZxlPVR_kmDznElVN-b1N9_gke1DfWphGemOYUPnBgSmLO_38_s7E4l47ocpNjynUO51yqyrWVxGr1w7l9sDUAr8TKnNsJp-T1UzFET5X5O5kGihHoizPR-mrgWNNIVSsOB7WP-eH9yzO9FUcldCjEgUdWmosKmgp21VRU7aoIKFsUN68sr6_eAYrxptDI8IXOGK3uXgVb1kiczBIDEQSy-yjxGPKvTTqJb3LrGWOzILk1uRX9g6RkZICzKyTsWZMI-Ia7QvkxXjNgCIN9BnaBicvEyOZYR9PjDZ8ukBvJ8aE3kKnENFvg8A32kmUQrcoSKezuZM0dGHE7H8a5yac4nfZi5XR3t_c4D6M9lvj2mivb23tP95-0nqyv9vagb-7m2vGjdFubTxu7e092dzZ3t_Z2dtt7bdu14zv-bCbj_e2dja3W9tbrY3d7d39ze3b_wDf7OZi?type=png)](https://mermaid.live/edit#pako:eNqtWetu2zYUfhVDwAAXS4pc3FyMroBjK6mG2A5kt1kHAwEjMTZbidJ0yWVFgnXAhg39s18bsBfYQ-zH3qVFf-wtdkhKFilRdlIvRRvxnMND8vA7hx_Zt4YTuNhoG46H4rhH0DRC_oQ24IdLGi9iHDXeCgn7WU9BYLntxiiJCJ2WFBT5WKPCPiKeRu4FU0JHCUrSuN04CAIPIyqpL9BlEJEEd2coQk6CI7A6JnFyN3xN_IDeFaZfck_NRxovTBWkCdNdBsSVFMh1D7MRmgH32G4Iz1XbCPvBJb63-RQnuW3MRq7O-hZ-yXF-Hvh45EQY00q023wTJO8uiUMP3fQxTTXLouiSTFGCx0Efor7EIFyoV9ZQa3WEnBlaaHGAksTDC01OgjfYxdeqTTlIIoJKgMROaAFZA0bio6lOPgvOz2808jjEDkHe6A3xdBjOQTqaBaFGHSFQglub_x7fhFhSJtDMQVRSkXh4niBCsavDNOCrh0Ht8Z0RDjKBZBUXKGySOP-c-1sY6mw_NJAUEWeIrsvG9QviQbZ22WgRQe3GodKuInk4d6lL0zD0boSHplPjstorCaZT7_4JWwBRhHFph3gWXA1EJxLQairWxFN410Q1xh6GEucOlXHrQiVtvmZeFkN4s27Ofp3qOUuAGt1ISoIak0MpEZqrB2wcpBGJfU2ofBT2UAIY6IsPSRUSmp8Rx4HDRzohykGR105UN0ew18WVO-p6xHnThEFgjMK93k8_cJHXhK_QohcBVIbsa_XISEMrcYF5aeugB9ZJ6kLi94L03MPKAUyndbrq1JVwiFhoj77cnmnVvuWl5Fo1FZjwAQXdxTHUhZCFRKOFUz7CcazTXEIOIVh0N0jDYA4c0bqrrbZlP0ydeZgf9YqP8qKFUlmyw0XaRcPeeQ9fNcAcfNLERolub_F1SKKbnlDCv8rBA2xDe-iQ-CXyiKtnWUBUFqNWcABNOp8LxU2cYL-dm_GWnCMJipIh9eBArCUTMUaRMxuGEElMk_-hBMlzUTMNKgiONsvELJNvVeTZEhMe74OiISMgjSKY9TiNaIXv-ShxZifcd6yPPg9PbWDwNXZSONvAdxN4NEeMMO7wlqYHdQtv4svGceolCiVOwGFO7hh_vU80hRslmleE0irLhdqk4b7rEb5CkZvnqs1bdyqygRBg6kCkLZrgqRJJSNVTPhqbainKoBPuijSuuGdG5nwEZqeMUV4yZ8YayE-ZnBG-fB1HuUBzVM11cf3WCgou6OTc_lH2Xdm5h-bB3KOyCDbaQ8q0EzDGWNkTYMgATVaG5ViwunVXXWezdk28CAv-uHxLNCAMMrZdx7-gLg7wle6WugSRbGbCWUHVlaIKbgt9NbXDKHDg_BJTXrxPfT21ZJdvia4zKy0jElY67hNiyu-S4hrPPlcvrsxLZZpaPMVQjVglqCrS89dAmrVYAwxQnYaNMuZ50s--ZEaQJAAP7NpLigyB7UC6MxJOax9DMfbD8rkKRTx60-H9NBGGkBB_YfUph08NtRxI6S5TLcr3uXWXbDIivuoFf_krQfW5orxo9dKnoOdz79l53uevUEOlXXMNrbsC3-ulR2yrOnku0tM_PnXRpzT171JEE77oalElnExZKoniKKuL8BdfNEya-rEy1Xkw2XSfPgWk-TjiqHv2rHDcHfb7w0HRtju2WbRGL05M-0yVHZtH5qDXsV8teudZOu6hJfs87YxNu2ge2Z3RqGiax2Z3bFvdQjIY2v3OcX1xWjr86NVobPbPBsOxdWh1O2NLjoH50hyMz6zB4VCKi3nasXtn_Y51vJBwMmq4cOTTjjW2BkeFwBqcndjDI9uUl3xoDazRc7O3CIZLFzn82lL21oIlSzv_wrbNQfeVtO5vYLctkJk1W6vk1-KhD8Yda5DPX2zZ-Kwq7RwX4WR_AMlffc4P72ljj08knpEwbjQ-_PD3h59_-_TPTx_f_fnplz8aG42P795__PHXf39__-mv96uMxR_WswfNdiN_RYzZAqS34PX1ZxlPVR_kmDznElVN-b1N9_gke1DfWphGemOYUPnBgSmLO_38_s7E4l47ocpNjynUO51yqyrWVxGr1w7l9sDUAr8TKnNsJp-T1UzFET5X5O5kGihHoizPR-mrgWNNIVSsOB7WP-eH9yzO9FUcldCjEgUdWmosKmgp21VRU7aoIKFsUN68sr6_eAYrxptDI8IXOGK3uXgVb1kiczBIDEQSy-yjxGPKvTTqJb3LrGWOzILk1uRX9g6RkZICzKyTsWZMI-Ia7QvkxXjNgCIN9BnaBicvEyOZYR9PjDZ8ukBvJ8aE3kKnENFvg8A32kmUQrcoSKezuZM0dGHE7H8a5yac4nfZi5XR3t_c4D6M9lvj2mivb23tP95-0nqyv9vagb-7m2vGjdFubTxu7e092dzZ3t_Z2dtt7bdu14zv-bCbj_e2dja3W9tbrY3d7d39ze3b_wDf7OZi)
