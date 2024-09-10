# SXGプログラミングバトル2024　めざせ最強うどん職人！！

## 概要

競技とゲームの内容の説明

---

## 開発環境

- Unity 2022.3.39f1

---

## Unityプロジェクト内構成

### フォルダ構成

```
Assets/
├── GaneAssets/
│   └── ParticipantList.asset
├── Participant/
│   └── Sample01/
│       ├── ComPlayerSample01.cs
│       └── ComPlayerSample01.prefab
├── Scenes/
│   ├── Game.scene
│   ├── PartisipantSelection.scene
│   └── Title.scene
└── UdonChef/
    └── Program/
        └── ComPlayerBase.cs    
```

### 各シーン

---

## AI作成手順

### AI登録方法

・フォルダ内にcsファイル、prefab、画像を入れる<br>
・Participant.assetに登録<br>
（自動化したい）

### 注意事項

・フォルダ名とnamespaceのつけ方

### 提出方法

・Googleフォームで提出

---

## 使用できる関数

- [SXG_GetFoodsInfoOnStage](#func01)
- [SXG_GetFoodInfo](#func02)
- [SXG_GetTheNextFallingFood](#func03)
- [SXG_GetAllFutureFoodsDrops](#func04)
- [SXG_MoveToTargetPosition](#func05)
- [SXG_Kick](#func06)
- [SXG_GetMyFoodsListOnHand](#func07)
- [SXG_HowManyMoreCanIHave](#func08)
- [SXG_GetPositionAndRotation](#func09)
- [SXG_GetVelocity](#func10)
- [SXG_IsOnGround](#func11)
- [SXG_GetPriceOfFoods](#func12)
- [SXG_GetNowPriceOnHand](#func13)
- [SXG_RaycastFromPlayer](#func14)
- [SXG_GetPlayersInfo](#func15)
- [SXG_IsStiffness](#func16)
- [SXG_GetLeftTimeOfStiffness](#func17)
- [SXG_GetPlayerGroundType](#func18)
- [SXG_GetRemainingGameTime](#func19)

<h3 id="func01">SXG_GetFoodsInfoOnStage</h3>

protected List<FoodNowInfo> SXG_GetFoodsInfoOnStage(FoodState[] targetFoodsState=null);

ステージ上の食材の情報を取得します。

---

<h3 id="func02">SXG_GetFoodInfo</h3>

protected FoodNowInfo SXG_GetFoodInfo(int foodId);

foodIdを指定して現在の状態を取得します。

---

<h3 id="func03">SXG_GetFoodInfo</h3>

protected FoodType SXG_GetTheNextFallingFood();

次に落ちてくるFoodTypeを取得します。<br>
何秒後に落ちてくるのかまでは分かりません。

---

<h3 id="func04">SXG_GetAllFutureFoodsDrops</h3>

protected FoodType[] SXG_GetAllFutureFoodsDrops();

次以降に落ちてくるFoodTypeをすべて取得します。<br>
次以降に落ちてくる順番が分かります。

---

<h3 id="func05">SXG_MoveToTargetPosition</h3>

protected void SXG_MoveToTargetPosition(Vector3 targetPosition, float speedRate);

目標座標を指定してそこへ移動します。

---

<h3 id="func06">SXG_Kick</h3>

protected void SXG_Kick();

正面方向にキックします。その後、しばらく硬直します。

---

<h3 id="func07">SXG_Kick</h3>

protected IList<FoodType> SXG_GetMyFoodsListOnHand();

手に持っている食材のリストを返します。
---

<h3 id="func08">SXG_HowManyMoreCanIHave</h3>

protected int SXG_HowManyMoreCanIHave();

食材をあと何個持てるかを返します。

---

<h3 id="func09">SXG_GetPositionAndRotation</h3>

protected void  SXG_GetPositionAndRotation(out Vector3 position, out Quaternion rotation);

自身の座標と角度を取得します。

---

<h3 id="func10">SXG_GetVelocity</h3>

protected Vector3 SXG_GetVelocity();

自身の移動速度を取得します。

---

<h3 id="func11">SXG_IsOnGround</h3>

protected bool SXG_IsOnGround();

自身が地面に接地しているかを返します。

---

<h3 id="func12">SXG_GetPriceOfFoods</h3>

protected int SXG_GetPriceOfFoods(FoodType[] foods);

食材を指定して価格を取得します。

---

<h3 id="func13">SXG_GetNowPriceOnHand</h3>

protected int SXG_GetNowPriceOnHand();

今、手に持っている食材の出荷価格を取得します。

---

<h3 id="func14">SXG_RaycastFromPlayer</h3>

protected bool SXG_RaycastFromPlayer(Vector3 origin, Vector3 direction, float maxDistance, RaycastTarget raycastTarget);

Raycastによるコリジョン判定を取得します。

---

<h3 id="func15">SXG_GetPlayersInfo</h3>

protected PlayerInfo[] SXG_GetPlayersInfo();

他のプレイヤーの座標やスコアの情報を取得します。

---

<h3 id="func16">SXG_IsStiffness</h3>

protected bool SXG_IsStiffness();

硬直動作中かどうかを取得します。<br>
キックするとしばらく別の行動をできません。

---

<h3 id="func17">SXG_GetLeftTimeOfStiffness</h3>

protected float SXG_GetLeftTimeOfStiffness();

硬直の残り時間を取得します。

---

<h3 id="func18">SXG_GetPlayerGroundType</h3>

protected GameConstants.PlayerGroundType SXG_GetPlayerGroundType();

プレイヤーの足元の領域種類を取得します。

---

<h3 id="func19">SXG_GetRemainingGameTime</h3>

protected float SXG_GetRemainingGameTime();

試合の残り時間を取得します。

---

## 食材一覧

| 食材       | FoodType    | 
| ---------- | ------------- | 
| うどん玉   | Noodle         | 
| 海老天     | ShrimpTempura  | 
| ちくわ天   | ChikuwaTempura | 
| きつね     | Kitsune        | 
| 大根おろし | GratedDaikon   | 
| 卵         | Egg            | 
| 肉         | Meat           | 
| バター     | Butter         | 
| レモン     | Lemon          | 
| カレー     | Curry          | 

---

## うどんメニュー一覧

### 価格計算方法

- 基本価格<br>
価格（円）= Raw価格（必要食材の原価）× Special倍率<br>
　※1の位は切り捨て


- うどん玉追加

- Good食材だけが含まれるメニュー<br>
うどん玉とGood食材だけで成立したメニューの説明

- Bad食材を含むメニュー<br>
Bad食材を含むメニューの説明

- GoodでもBadでもない食材を含むメニュー

### うどんメニュー価格一覧

| メニュー名       | 価格 | 必要食材                                  | Good食材 | Bad食材        | 
| --------------- | ---- | ---------------------------------------- | -------- | ------------- | 
| かけうどん       | 200  | うどん玉                                  |          | バター        | 
| おろしぶっかけ   | 320  | うどん玉<br>大根おろし                     |          | バター        | 
| 海老天うどん     | 400  | うどん玉<br>海老天                        | 海老天   | バター         | 
| ちく天ぶっかけ   | 550  | うどん玉<br>ちくわ天                      | ちくわ天 | バター         | 
| きつねうどん     | 320  | うどん玉<br>きつね                        | きつね   | バター         | 
| 特上天ぷらうどん | 780  | うどん玉<br>海老天<br>ちくわ天             |          | バター         | 
| 窯玉うどん       | 300  | うどん玉<br>卵                           |          | バター         | 
| 窯バターうどん   | 520  | うどん玉<br>卵<br>バター                  |          |                | 
| 肉うどん         | 450  | うどん玉<br>肉                           | 肉       | バター         | 
| 肉ぶっかけ       | 500  | うどん玉<br>肉<br>レモン                  | 肉       | バター         | 
| 肉窯玉うどん     | 550  | うどん玉<br>肉<br>卵                      | 肉       | バター         | 
| カレーうどん     | 400  | うどん玉<br>カレー                        |          | バター<br>大根 | 
| 肉カレーうどん   | 970  | うどん玉<br>肉<br>カレー                  | 肉       | バター<br>大根 | 
| エックスうどん   |  2310 | うどん玉<br>海老天 ×2<br>きつね<br>レモン |          | バター         | 
