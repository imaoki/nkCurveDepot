# nkCurveDepot

[![GitHub release (latest by date)](https://img.shields.io/github/v/release/imaoki/nkCurveDepot)](https://github.com/imaoki/nkCurveDepot/releases/latest)

リグ用コントローラを作成するツール。

![window-main](resource/window-main.png "window-main")

## 特徴

* 任意のカーブをリグコントローラとして無制限に定義可能

* 複数のカーブを合成して単一ノードとして作成するためのコードを生成可能。

* カーブのローカル変換を専用のTRS値で編集可能。

  * 編集が完了したカーブはロックすることで編集用の計算ノードを除去できます。

  * 編集モードへはいつでも切り替えが可能。

## 開発環境

Maya 2022.5 / Windows 10

## インストール

01. `nkCurveDepot.mel`をスクリプトディレクトリにコピー

    | バージョン | ディレクトリ                             |
    | ---------- | ---------------------------------------- |
    | 英語版     | `%MAYA_APP_DIR%\<version>\scripts`       |
    | 日本語版   | `%MAYA_APP_DIR%\<version>\ja_JP\scripts` |

02. Mayaを再起動

## 起動方法

```mel
nkCurveDepot;
```

## メインウィンドウ

![window-main](resource/window-main.png "window-main")

| ボタン                                                                                                                                                                                        | 機能                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| ![Add Curve](resource/item_add.png "Add Curve")                                                                                                                                               | カーブ定義を追加                           |
| ![Rename Curve](resource/passSetRelationEditor.png "Rename Curve")                                                                                                                            | カーブ定義をリネーム                       |
| ![Create Curve](resource/createNode.png "Create Curve")                                                                                                                                       | カーブノードをシーンに作成                 |
| ![Unlock Shape Transform](resource/unlockGeneric.png "Unlock Shape Transform")                                                                                                                | 選択したカーブノードのシェイプ変換を有効化 |
| ![Lock Shape Transform](resource/lockGeneric.png "Lock Shape Transform")                                                                                                                      | 選択したカーブノードのシェイプ変換を無効化 |
| ![Replace Curve](resource/bufferSnap.png "Replace Curve")                                                                                                                                     | 既存のカーブノードのシェイプを置き換える   |
| ![Delete Curve](resource/item_delete.png "Delete Curve")                                                                                                                                      | カーブ定義を削除する                       |
| ![Move Curve Up](resource/item_up.png "Move Curve Up")![Move Curve Down](resource/item_down.png "Move Curve Down")![Sort by ascending order](resource/sortName.png "Sort by ascending order") | カーブ定義を並べ替える                     |

## カーブ定義の追加とカーブノードの作成

![add-curve](resource/add-curve.gif "add-curve")

01. 追加したいカーブを用意する。

02. ![Add Curve](resource/item_add.png "Add Curve")ボタンでカーブ定義を追加。

03. リストに追加されたカーブ定義を選択して![Create Curve](resource/createNode.png "Create Curve")ボタンでカーブノードを作成。

## カーブノードのシェイプ変換

![shape-transform](resource/shape-transform.gif "shape-transform")

01. カーブノードを選択して![Unlock Shape Transform](resource/unlockGeneric.png "Unlock Shape Transform")ボタンでアトリビュートのロックを解除。

02. チャンネルボックスまたはアトリビュートエディタで`Shape Translate/Rotate/Scale`の値を編集。

03. ![Lock Shape Transform](resource/lockGeneric.png "Lock Shape Transform")ボタンでアトリビュートをロック。

### 注意点

* 編集は本ツールで作成したカーブノードに限ります。

  トランスフォームノードに`Shape Translate/Rotate/Scale`アトリビュートを追加しても機能しません。
  シェイプノードにオリジナルのカーブデータが埋め込まれている必要があります。

* 編集後はロックすることをおすすめします。

  カーブの複雑さによっては大量の計算ノードがシーン内に常時存在することになるからです。

## 既存のカーブノードを置き換える

![replace-curve](resource/replace-curve.gif "replace-curve")

01. 置き換え元のカーブノード（本ツールで作成）を選択。

02. 置き換え対象のカーブノード（通常のカーブノード or 本ツールで作成したカーブノード）を選択。

03. ![Replace Curve](resource/bufferSnap.png "Replace Curve")ボタンで置き換え。

04. 実行後にオフセットが反映されていない場合は![Unlock Shape Transform](resource/unlockGeneric.png "Unlock Shape Transform")/![Lock Shape Transform](resource/lockGeneric.png "Lock Shape Transform")ボタンを使用して更新してください。

### 注意点

* 置き換え対象の元のシェイプは削除されますので適宜バックアップしてください。

## 補足事項

* ![Delete Curve](resource/item_delete.png "Delete Curve")ボタンで削除したカーブ定義は`nkCurveDepotCurves/trash`フォルダに上書き移動されます。

  残しておきたいカーブ定義は適宜`.curve`ファイルをバックアップしてください。
