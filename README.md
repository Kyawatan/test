# SXGプログラミングバトル2024　めざせ最強うどん職人！！

## 概要

『Sanuki X Game 2024』イベントの一般参加企画です。<br>
ゲーム内に登場するAIプレイヤーを募集し、イベント当日、集まったAIプレイヤーたちでトーナメントを開催します！<br>
最強のAIプレイヤーを作って応募してみませんか？

### ゲーム内容

ステージ上の食材を拾って、うどんメニューを作って出荷しよう！<br>
制限時間内にたくさん自分の出荷テーブルに出荷できたAIプレイヤーの勝利！<br>

拾う食材の組み合わせによって、スペシャルな高価格うどんメニューも作れるぞ！<br>
ステージはつるつる滑るので、間違って他のプレイヤーの出荷テーブルに出荷しないように気をつけて！<br>
他プレイヤーをキックで吹っ飛ばして妨害も可能！？<br>

[ゲーム紹介動画リンク誘導]

- 一試合4人のAIプレイヤーで対戦
- 一試合の制限時間は1分30秒
- 食材は一度に最大5つ持てる
- プレイヤーは「走る」「食材を拾う」「キック」が可能

### 参加要項

基礎的なC#プログラミングができれば、年齢・職業問わず、誰でも参加可能です！

### 本番の進行方法

・配信<br>
・トーナメント<br>
・予選やるかも

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
│   ├── ParticipantSelection.scene
│   └── Title.scene
└── UdonChef/
    └── Program/
        └── ComPlayerBase.cs    
```

### タイトル画面（Assets/Scenes/Title.scene）

タイトル画面です。<br>
Spaceキーを押すと、挑戦者選択画面へ遷移します。

<img src="https://github.com/user-attachments/assets/14b41e5b-19b7-4f37-87c2-e47676f22c34" width="50%">

### 挑戦者選択画面（Assets/Scenes/ParticipantSelection.scene）

その試合でバトルさせるAIを選択する画面です。<br>
AIは必ず4人選ぶ必要があります（重複可）。4人選ぶと「決定」ボタンを押せるようになります。<br>
「決定」ボタンを押すと、ゲーム画面へ遷移します。

<img src="https://github.com/user-attachments/assets/07bb452b-407b-4946-85eb-e246c7b266e1" width="50%">

### ゲーム画面（Assets/Scenes/Game.scene）

冒頭ではその試合でバトルする4人のAIが表示されます。<br>
挑戦者選択画面から遷移してきた場合は、選択した挑戦者が表示されます。<br>
ゲーム画面から起動した場合は、挑戦者リスト（Assets/GameAssets/ParticipantList.asset）の上から4つ分の要素が選択されます。

<img src="https://github.com/user-attachments/assets/00340903-ce1b-4bff-8b6e-d040a5d28f27" width="50%"><br>

Spaceキーを押すと、挑戦者の表示が消え、プレイ画面が表示されます。

<img src="https://github.com/user-attachments/assets/3ba2ce0e-2998-477e-ba6c-0a08b1db7b89" width="50%"><br>

Spaceキーを押すと、試合開始します。<br>
試合時間は1分30秒です。試合終了まで待ちます。

試合終了すると「GAME SET」が表示されます。<br>

<img src="https://github.com/user-attachments/assets/de45d66a-6266-4b19-be09-129f0af3f14c" width="50%"><br>

Spaceキーを押すと、リザルト演出に移ります。<br>
再度Spaceキーを押すと、タイトル画面へ遷移します（リザルト演出中でも遷移可能）。

<img src="https://github.com/user-attachments/assets/6adf6dd7-91a7-4053-a478-71359ca0259b" width="50%">

### AI作成時に継承するベースクラス（Assets/UdonChef/ComPlayerBase.cs）

AIを作成時、ComPlayerBaseクラスを継承します。<br>
AI作成時は、ベースクラスの関数を用いて機能実装します。

### 挑戦者のAIデータ（Assets/Participant/ 以下）

AIデータは、挑戦者ごとにフォルダ単位で分けます。各フォルダ内は以下で構成されます。<br>
　① ComPlayerBaseクラスを継承したスクリプトファイル<br>
　② ①をアタッチしたPrefab<br>
　③ アイコン画像（最大サイズ256*256）<br>

② のPrefabには、あなたの所属、プレイヤー名、アイコン画像(③)を設定します。

あらかじめ、いくつかのサンプルAIが用意されています。

### 挑戦者リスト（Assets/GameAssets/ParticipantList.asset）

挑戦者選択画面で選択できるAIをリスト管理するScriptableObjectです。<br>
このリストに、② のPrefabをアタッチします。

### サンプルアイコン画像（Assets/GameAssets/Textures/ 以下）

PlayerSampleImage_***.png は、挑戦者のAIのアイコン画像として使用可能です。<br>
アイコン画像を用意できない場合はお使いください。<br>
一部のサンプルAIは、このサンプル画像を使用しています。

---

## AI作成手順

<h3 id="entrypoint">作成する前に</h3>

**connpassでエントリーし、「受付番号」を発行してください。**<br>
エントリーせずにAIを提出した場合、無効となります。<br>

<img src="https://github.com/user-attachments/assets/6401effb-1418-4d37-a39f-0694ded64158" width="50%">

### AI登録方法

#### 1. Unity上部メニュー SXG2024 > 挑戦者作成 を選択

<img src="https://github.com/user-attachments/assets/c4045cde-2aa0-40a8-8668-690b34f19d3b"><br>

挑戦者登録ウィンドウが開きます。

<img src="https://github.com/user-attachments/assets/93d3bbfe-c8db-4b2b-b408-10b9d1eda08f" width="50%"><br>

#### 2. 各項目を入力

■必須項目
- 受付番号： **connpassエントリー時に発行された受付番号** を入力<br>
[作成する前に](#entrypoint) を確認

■任意項目
- 所属名：実際に所属している会社名や学校名 or 架空の所属名<br>
- 挑戦者名：本名 or ニックネーム
- アイコン画像ファイル選択：アイコン画像ファイル（jpgかpng）を「参照」ボタンから選択（未選択可能）

※アイコン画像ファイルの最大サイズは256*256です。<br>
版権画像は使用できますが、公序良俗に反する画像はご遠慮ください。<br>

これらの任意項目は、挑戦者登録ウィンドウを閉じたあとでも変更可能です。

#### 3. 「作成」ボタン押下

各項目を入力し終えて「作成」ボタンを押すと、挑戦者のAIに必要なデータが作成されます。<br>
フォルダ名、各ファイル名は「Player(3桁の受付番号）」で命名されます。<br>
同時に、挑戦者リスト（Assets/GameAssets/ParticipantList.asset）の0番目の要素に登録され、ゲーム内で挑戦者として選択できるようになります。

例：受付番号 41

```
Assets/
└── Participant/
    └── Player041/
        ├── Player041.cs
        ├── Player041.prefab
        └── Player041.png
```

Prefabで、以下の項目を変更できます。<br>
　・所属名（Your Organization）<br>
　・挑戦者名（Your Name）<br>
　・アイコン画像ファイル（Face Image）<br>

 <img src="https://github.com/user-attachments/assets/790c3ca2-a7c8-497a-98ec-b8d46fcab1e8"><br>

挑戦者作成ウィンドウでアイコン画像ファイルを設定しなかった場合、後から手動で追加してください。<br>
アイコン画像を用意できない場合、サンプルアイコン画像（Assets/GameAssets/Textures/PlayerSampleImage_***.png）を使用しても構いません。

#### 4. AIを作成する

作成されたC#スクリプトを編集して、AIを作成していきます。<br>
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

### 提出方法

・AIデータが入っているフォルダをZIP形式に圧縮する<br>
　例：受付番号 41
```
Assets/
└── Participant/
    └── Player041　← このフォルダをZIPにする
```

・GoogleフォームにZIPを提出<br>
　**connpassエントリー時に発行された受付番号**が必要です

### 注意事項

- 必ずconnpassでエントリーし、受付番号を発行してください
- 受付番号を間違えないよう注意してください
- アイコン画像サイズは最大256*256とし、公序良俗に反する画像はご遠慮ください
- AI作成時にUnityパッケージの追加はできません
- AI提出後、弊社で不正や目立った不具合が無いか審査いたします

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

public virtual void UDON_ReportOnShipping(IList\<FoodType\> foodsList, int tableId, int price, string menuName);

自身の出荷テーブルに出荷されたときに呼び出されます。他のプレイヤーが自分の出荷テーブルに出荷した時も呼び出されます。

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

List\<FoodNowInfo\> SXG_GetFoodsInfoOnStage(FoodState[] targetFoodsState=null);

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
次以降に落ちてくる順番が分かります。<br>
落ちてくるFoodTypeの種類と順番は、ゲーム開始時にランダムで決定されます。ゲームの途中で変わる事はありません。

---

<h3 id="func05">SXG_MoveToTargetPosition</h3>

void SXG_MoveToTargetPosition(Vector3 targetPosition, float speedRate);

目標座標を指定してそこへ移動します。

---

<h3 id="func06">SXG_Kick</h3>

void SXG_Kick();

正面方向にキックします。その後、しばらく硬直します。<br>
キックがヒットしたプレイヤーや食材は吹っ飛びます。

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
領域については、後述するステージ見取り図をご確認ください。

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

### Sample（Assets/Participant/Sample 以下）

■所属名：xeen<br>
■挑戦者名：Sample<br>
■特徴：無難なやつ

ステージ上の食材をランダムに狙います。<br>
ある程度食材を拾うと自身の出荷テーブルへ運びます。<br>
いくらか経っても狙いの食材を拾えない場合、諦めて別の食材を狙います。

### Sample01（Assets/Participant/Sample01 以下）

■所属名：FM728<br>
■挑戦者名：たこ猫<br>
■特徴：蹴りまくるやつ

自身の正面に他のプレイヤーがいるか、ランダムなタイミングでキックします。<br>
ステージ上の食材をランダムに狙います。<br>
メニューが成立するか、手持ちの食材がいっぱいになると自身の出荷テーブルへ運びます。<br>
いくらか経っても狙いの食材を拾えない場合、諦めて別の食材を狙います。

### Sample02（Assets/Participant/Sample02 以下）

■所属名：FM728<br>
■挑戦者名：ルッカ<br>
■特徴：かしこいやつ

食材やプレイヤーの位置関係、残り時間も考えて行動します。<br>
うどん玉を優先して狙います。<br>
メニューが成立するか、手持ちの食材がいっぱいになると自身の出荷テーブルへ運びます。<br>
いくらか経っても狙いの食材を拾えない場合、諦めて別の食材を狙います。

### Sample03（Assets/Participant/Sample03 以下）

■所属名：FM728<br>
■挑戦者名：蹴ルッカ<br>
■特徴：ずるがしこいやつ

Sample02の行動をベースに、キックもします。

### Sample04（Assets/Participant/Sample04 以下）

■所属名：<br>
■挑戦者名：<br>
■特徴：

[追記予定]

### Sample05（Assets/Participant/Sample05 以下）

■所属名：xeen<br>
■挑戦者名：ぼく<br>
■特徴：それなりのやつ

うどん玉を最優先に、自分から近い場所にある食材を狙います。<br>
[追記予定]

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
| エックスうどん   |  2700 | うどん玉<br>海老天 ×2<br>肉<br>レモン     |            | バター         | 

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
