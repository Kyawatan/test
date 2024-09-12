# SXGプログラミングバトル2024　めざせ最強うどん職人！！

## 概要

### 競技内容

### ゲーム内容

### 本番の進行方法

---

## 開発環境

- Unity 2022.3.39f1

---

## Unityプロジェクト内構成

### フォルダ構成

```
Assets/
├── GaneAssets/
│   ├── ParticipantList.asset
│   └── Textures/
│       ├── PlayerSampleImage_Lucca00.png
│       ├── PlayerSampleImage_Lucca01.png
│       ├── PlayerSampleImage_Lucca02.png
│       └── PlayerSampleImage_Takoneko.png
├── Participant/
│   ├── Sample/
│   │   ├── ComPlayerSample.cs
│   │   └── ComPlayerSample.prefab
│   ├── Sample01/
│   │   ├── ComPlayerSample01.cs
│   │   └── ComPlayerSample01.prefab
│   ├── Sample02/
│   │   ├── ComPlayerSample02.cs
│   │   └── ComPlayerSample02.prefab
│   └── Sample03/
│       └── ComPlayerSample03.prefab
├── Scenes/
│   ├── Game.scene
│   ├── PartisipantSelection.scene
│   └── Title.scene
└── UdonChef/
    └── Program/
        └── ComPlayerBase.cs    
```

### タイトル画面（Assets/Scenes/Title.scene）

タイトル画面です。<br>
Spaceキーを押すと、挑戦者選択画面へ遷移します。

[画像]

### 挑戦者選択画面（Assets/Scenes/ParticipantSelection.scene）

その試合でバトルさせるAIを選択する画面です。<br>
AIは必ず4人選ぶ必要があります（重複可）。4人選ぶと「決定」ボタンを押せるようになります。<br>
「決定」ボタンを押すと、ゲーム画面へ遷移します。

[画像]

### ゲーム画面（Assets/Scenes/Game.scene）

冒頭ではその試合でバトルする4人のAIが表示されます。<br>
挑戦者選択画面から遷移してきた場合は、選択した挑戦者が表示されます。<br>
ゲーム画面から起動した場合は、挑戦者リスト（Assets/GameAssets/ParticipantList.asset）の上から4つ分の要素が選択されます。

Spaceキーを押すと表示が消え、プレイ画面が見えるようになります。<br>
Spaceキーを押すと試合が開始します。<br>
試合が終了すると「GAME SET」と表示されます。<br>
Spaceキーを押すと、リザルトが表示されます。<br>
Spaceキーを押すと、タイトル画面へ遷移します（リザルト演出中も押下可能）。

[画像]

### AI作成時に継承するベースクラス（Assets/UdonChef/ComPlayerBase.cs）

AIを作成時、ComPlayerBaseクラスを継承します。<br>
AI作成時は、ベースクラスの関数を用いて機能実装します。

### 挑戦者のAIデータ（Assets/Participant/ 以下）

AIデータは、挑戦者ごとにフォルダ単位で分けます。各フォルダ内は以下で構成されます。<br>
　① ComPlayerBaseクラスを継承したスクリプトファイル<br>
　② ①をアタッチしたPrefab<br>
　③ アイコン画像（最大サイズ216*216）<br>

② ①をアタッチしたPrefab には、挑戦者ごとに任意の所属名、プレイヤー名、③ アイコン画像 を設定します。

あらかじめ、いくつかのサンプルAIが用意されています。

### 挑戦者リスト（Assets/GameAssets/ParticipantList.asset）

挑戦者選択画面で選択できるAIをリスト管理するScriptableObjectです。<br>
このリストに、① のPrefabをアタッチします。

### サンプルアイコン画像（Assets/GameAssets/Textures/ 以下）

PlayerSampleImage_***.png は、挑戦者のAIのアイコン画像として使用可能です。<br>
アイコン画像を用意できない場合はお使いください。<br>
一部のサンプルAIは、このサンプルAIアイコン画像を使用しています。

---

## AI作成手順

### 作成する前に

**connpassでエントリーし、「参加番号」を発行してください。**<br>
エントリーせずにAIを提出した場合、無効となります。

### AI登録方法

#### 1. Unity上部メニュー SXG2024 > 挑戦者作成 を選択

挑戦者登録ウィンドウが開きます。

#### 2. 各項目を入力

必須項目として、「参加番号」の欄に **connpassエントリー時に発行された参加番号** を入力してください。<br>

任意項目として、「所属名」「挑戦者名」をそれぞれ入力します。<br>
所属名は、実際に所属している会社名や学校名を記入しても、架空の所属名を記入しても構いません。<br>
挑戦者名は、本名でも亀井でも構いません。

また、アイコン画像ファイル（jpgかpng）を「参照」ボタンから選択します（未選択可）。<br>
最大サイズは256*256です。版権画像は使用しても構いませんが、公序良俗に反する画像はご遠慮ください。<br>

これらの任意項目は、後からでも変更可能です。

[画像]

#### 3. 「作成」ボタン押下

各項目を入力し終えて「作成」ボタンを押すと、挑戦者のAIデータが作成されます。<br>
フォルダ名、各ファイル名は「Player(3桁の参加番号）」で命名されます。<br>
同時に、挑戦者リスト（Assets/GameAssets/ParticipantList.asset）の0番目の要素に登録され、ゲーム内で挑戦者として選択できるようになります。

例：参加番号 41

```
Assets/
└── Participant/
    └── Player041/
        ├── Player041.cs
        └── Player041.prefab
        └── Player041.png
```

挑戦者作成ウィンドウでアイコン画像ファイルを設定しなかった場合、後から手動で追加してください。<br>
Prefabで、所属名（Your Organization）、挑戦者名（Your Name）、アイコン画像ファイル（Face Image）を変更可能です。<br>
アイコン画像を用意できない場合、サンプルアイコン画像（Assets/GameAssets/Textures/ 以下の PlayerSampleImage_***.png）を使用しても構いません。

#### 4. AIを作成する

作成されたC#スクリプトを使用して、AIを作成していきます。<br>
初期状態では、オーバーライドされた`UDON_ShouldGetTheFoodOnStage`関数と`UDON_ReportOnShipping`関数のみが記入されています。<br>

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using SXG2024;

namespace Player000
{
    public class Player000 : ComPlayerBase
    {
        public override bool UDON_ShouldGetTheFoodOnStage(FoodNowInfo foodInfo)
        {
            return true;
        }

        public override void UDON_ReportOnShipping(IList<FoodType> foodsList, int tableId, int price, string menuName)
        {

        }
    }
}
```

### 注意事項

- 必ずconnpassでエントリーし、参加番号を発行してください
- 参加番号を間違えないよう注意してください
- アイコン画像サイズは最大256*256とし、公序良俗に反する画像はご遠慮ください
- AI作成時にパッケージの追加はできません
- AI提出後、弊社で不正や目立った不具合が無いか審査いたします

### 提出方法

・Googleフォームで提出

---

## オーバーライドできる関数

- [UDON_ShouldGetTheFoodOnStage](#override01)
- [UDON_ReportOnShipping](#override02)

---

<h3 id="override01">UDON_ShouldGetTheFoodOnStage</h3>

bool UDON_ShouldGetTheFoodOnStage(FoodNowInfo foodInfo);

自身が食材に触れたときに呼び出されます。<br>
自身に触れた食材（foodInfo）を拾うかどうかの処理を記述し、拾う場合はtrue、拾わない場合はfalseを返してください。

---

<h3 id="override02">UDON_ReportOnShipping</h3>

public virtual void UDON_ReportOnShipping(IList<FoodType> foodsList, int tableId, int price, string menuName);

自身の出荷テーブルに出荷されたときに呼び出されます。プレイヤーの自他を問わず呼び出されます。

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
- [SXG_GetCollidedPlayersNumber](#func20)

---

<h3 id="func01">SXG_GetFoodsInfoOnStage</h3>

List<FoodNowInfo> SXG_GetFoodsInfoOnStage(FoodState[] targetFoodsState=null);

ステージ上の食材の情報を取得します。

---

<h3 id="func02">SXG_GetFoodInfo</h3>

FoodNowInfo SXG_GetFoodInfo(int foodId);

foodIdを指定して現在の状態を取得します。

---

<h3 id="func03">SXG_GetFoodInfo</h3>

FoodType SXG_GetTheNextFallingFood();

次に落ちてくるFoodTypeを取得します。<br>
何秒後に落ちてくるのかまでは分かりません。

---

<h3 id="func04">SXG_GetAllFutureFoodsDrops</h3>

FoodType[] SXG_GetAllFutureFoodsDrops();

次以降に落ちてくるFoodTypeをすべて取得します。<br>
次以降に落ちてくる順番が分かります。

---

<h3 id="func05">SXG_MoveToTargetPosition</h3>

void SXG_MoveToTargetPosition(Vector3 targetPosition, float speedRate);

目標座標を指定してそこへ移動します。

---

<h3 id="func06">SXG_Kick</h3>

void SXG_Kick();

正面方向にキックします。その後、しばらく硬直します。

---

<h3 id="func07">SXG_GetMyFoodsListOnHand</h3>

IList<FoodType> SXG_GetMyFoodsListOnHand();

手に持っている食材のリストを返します。

---

<h3 id="func08">SXG_HowManyMoreCanIHave</h3>

int SXG_HowManyMoreCanIHave();

食材をあと何個持てるかを返します。

---

<h3 id="func09">SXG_GetPositionAndRotation</h3>

void  SXG_GetPositionAndRotation(out Vector3 position, out Quaternion rotation);

自身の座標と角度を取得します。

---

<h3 id="func10">SXG_GetVelocity</h3>

Vector3 SXG_GetVelocity();

自身の移動速度を取得します。

---

<h3 id="func11">SXG_IsOnGround</h3>

bool SXG_IsOnGround();

自身が地面に接地しているかを返します。

---

<h3 id="func12">SXG_GetPriceOfFoods</h3>

int SXG_GetPriceOfFoods(FoodType[] foods);

食材を指定して価格を取得します。

---

<h3 id="func13">SXG_GetNowPriceOnHand</h3>

int SXG_GetNowPriceOnHand();

今、手に持っている食材の出荷価格を取得します。

---

<h3 id="func14">SXG_RaycastFromPlayer</h3>

bool SXG_RaycastFromPlayer(Vector3 origin, Vector3 direction, float maxDistance, RaycastTarget raycastTarget);

Raycastによるコリジョン判定を取得します。

---

<h3 id="func15">SXG_GetPlayersInfo</h3>

PlayerInfo[] SXG_GetPlayersInfo();

他のプレイヤーの座標やスコアの情報を取得します。

---

<h3 id="func16">SXG_IsStiffness</h3>

bool SXG_IsStiffness();

硬直動作中かどうかを取得します。<br>
キックするとしばらく別の行動をできません。

---

<h3 id="func17">SXG_GetLeftTimeOfStiffness</h3>

float SXG_GetLeftTimeOfStiffness();

硬直の残り時間を取得します。

---

<h3 id="func18">SXG_GetPlayerGroundType</h3>

GameConstants.PlayerGroundType SXG_GetPlayerGroundType();

プレイヤーの足元の領域種類を取得します。

---

<h3 id="func19">SXG_GetRemainingGameTime</h3>

float SXG_GetRemainingGameTime();

試合の残り時間を取得します。

---

<h3 id="func20">SXG_GetCollidedPlayersNumber</h3>

List<int> SXG_GetCollidedPlayersNumber();

今現在接触しているプレイヤー番号のリストを返します。<br>
接触してるプレイヤーがいない場合、要素数0のリストを返します。<br>
この番号は `SXG_GetPlayersInfo` で得られる配列の添え字と一致します。0（自分自身）は返しません。

---

## ステージ見取り図

[画像]

---

## サンプルAI解説

### Sample


### Sample01


### Sample02


### Sample03


---

## 食材一覧

プレイヤーが拾う食材は、`FoodType`というenumで管理されています。

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

### うどんメニュー価格一覧

| メニュー名       | 価格 | 必要食材                                  | Bonus食材  | Bad食材        | 
| --------------- | ---- | ---------------------------------------- | ---------- | ------------- | 
| かけうどん       | 200  | うどん玉                                  |            | バター        | 
| おろしぶっかけ   | 320  | うどん玉<br>大根おろし                     |            | バター        | 
| 海老天うどん     | 400  | うどん玉<br>海老天                        | 海老天      | バター         | 
| ちく天ぶっかけ   | 550  | うどん玉<br>ちくわ天                      | ちくわ天    | バター         | 
| きつねうどん     | 320  | うどん玉<br>きつね                        | きつね     | バター         | 
| 特上天ぷらうどん | 780  | うどん玉<br>海老天<br>ちくわ天             |            | バター         | 
| 釜玉うどん       | 300  | うどん玉<br>卵                           |            | バター         | 
| 釜バターうどん   | 520  | うどん玉<br>卵<br>バター                  |            |                | 
| 肉うどん         | 450  | うどん玉<br>肉                           | 肉         | バター         | 
| 肉ぶっかけ       | 500  | うどん玉<br>肉<br>レモン                  | 肉         | バター         | 
| 肉釜玉うどん     | 550  | うどん玉<br>肉<br>卵                      | 肉         | バター         | 
| カレーうどん     | 400  | うどん玉<br>カレー                        |            | バター<br>大根 | 
| 肉カレーうどん   | 970  | うどん玉<br>肉<br>カレー                  | 肉         | バター<br>大根 | 
| エックスうどん   |  2310 | うどん玉<br>海老天 ×2<br>肉<br>レモン     |            | バター         | 

### メニュー成立優先

複数のメニューが成立する場合、価格一覧表で最も下に位置しているメニューが成立します。

例えば、「うどん玉×1、大根おろし×1、肉×1、卵×1」で出荷した場合、おろしぶっかけ、肉うどん、肉釜玉うどんのいずれも成立しますが、
この場合、価格一覧表で最も下に位置している「肉釜玉うどん」が成立します。<br>
    `うどん玉×1、大根おろし×1、肉×1、卵×1` ⇒ `肉釜玉うどん`


### 価格変動：うどん玉追加

全てのメニューは、うどん玉を1つ必要とします。<br>
うどん玉が2つ以上あった場合、価格が **うどん玉追加分×100円増加** します。<br>
また、うどん玉の追加分に応じて、メニュー名に接尾辞が付与されます。

| うどん玉の追加数 | 接尾辞    |
| --------------- | -------- |
| 1               | 中       |
| 2               | 大       |
| 3               | 特大     |
| 4               | ジャンボ |

例えば、「うどん玉×3、大根おろし×1」で出荷した場合、おろしぶっかけ（320円）が成立し、更にうどん玉が2つ追加されているため200円増加して「おろしぶっかけ大（520円）」となります。<br>
    `うどん玉×3、大根おろし×1` ⇒ `おろしぶっかけ（320円）` + `うどん玉×2（200円）` = `おろしぶっかけ大（520円）`

### 価格変動：Bonus食材

メニューによっては「Bonus食材」があります。<br>
**うどん玉とBonus食材だけ**でメニューが成立している場合、価格が **Bonus食材追加分倍増** します。<br>
Bonus食材以外の食材が含まれていれば、Bonus食材はGood食材として扱われます。<br>
また、Bonus食材が1つ追加分に応じて、メニュー名に接頭辞が付与されます。

| Bonus食材の追加数 | 接頭辞    |
| --------------- | --------- |
| 1               | ダブル     |
| 2               | トリプル   |
| 3               | デラックス |

例えば、「うどん玉×1、海老天×4」で出荷した場合、海老天うどん（400円）が成立し、更に海老天が3つ追加されているため4倍して「デラックス海老天うどん（1600円）」となります。<br>
    `うどん玉×1、海老天×4` ⇒ `海老天うどん（400円）` × (1 `+ 3（海老天×3）`) = `デラックス海老天うどん（1600円）`
    
「うどん玉×2、肉×2、カレー×1」で出荷した場合、肉カレーうどん（970円）が成立し、更にうどん玉が1つ追加されているため100円増加、肉が1つ追加されているため2倍して「ダブル肉カレーうどん中（2140円）」となります。<br>
    `うどん玉×2、肉×2、カレー×1` ⇒ ( `肉カレーうどん（970円）` + `うどん玉×1（100円）`) × (1 `+ 1（肉×1）`) = `ダブル肉カレーうどん中（2140円）`

### 価格変動：Bad食材

メニューによっては、メニュー成立に必要な食材と相性が悪い「Bad食材」があります。<br>
メニューが成立していても、Bad食材が含まれている場合、価格が **Bad食材分半減** します。

例えば、「うどん玉×1、バター×2」で出荷した場合、かけうどん（200円）が成立し、更にバターが2つ含まれているため200円÷2÷2して「かけうどん（50円）」となります。<br>
    `うどん玉×1、バター×2` ⇒ `かけうどん（200円）` `÷ 2^2（バター×2）` = `かけうどん（50円）`

### 価格変動：Good食材

メニュー成立に必要な食材とうどん玉以外の、Bonus食材でもBad食材でもない食材は全て「Good食材」となります。<br>
Good食材は、価格が **Good食材分×50円増加** します。<br>

例えば、「うどん玉×1、大根おろし×1、肉×1、卵×1」で出荷した場合、価格一覧表で最も下に位置している肉釜玉うどん（550円）が成立し、更に大根おろしが1つ含まれているため50円増加して「肉釜玉うどん（600円）」となります。<br>
    `うどん玉×1、大根おろし×1、肉×1、卵×1` ⇒ `肉釜玉うどん（550円）` + `大根おろし×1（50円）` = `肉釜玉うどん（600円）`
