# SXGプログラミングバトル2024　めざせ最強うどん職人！！

![画面_タイトル](https://github.com/user-attachments/assets/2581da80-0fa1-4c2a-b707-048a0b369406)

## 概要

[『Sanuki X Game 2024』](https://www.showxguys.org/)イベントの一般参加企画です。<br>
ゲーム内に登場するAIプレイヤーを募集し、イベント当日、集まったAIプレイヤーたちでトーナメントを開催します！<br>
最強のAIプレイヤーを作って応募してみませんか？

### ゲーム内容

ステージ上の食材を拾って、うどんメニューを作って出荷しよう！<br>
制限時間内にたくさん自分の出荷テーブルに出荷できたAIプレイヤーの勝利！<br>

拾う食材の組み合わせによって、スペシャルな高価格うどんメニューも作れるぞ！<br>
ステージはつるつる滑るので、間違って他のプレイヤーの出荷テーブルに出荷しないように気をつけて！<br>
他プレイヤーをキックで吹っ飛ばして妨害も可能！？<br>

[試合の様子はこちらから](https://youtu.be/5TRa4eK_FKI)

- 一試合4人のAIプレイヤーで対戦
- 一試合の制限時間は1分30秒
- 食材は一度に最大5つ持てる
- プレイヤーは「走る」「食材を拾う」「キック」が可能

### 募集要項

基礎的なC#プログラミングができれば、年齢・職業問わず、誰でも参加可能です！

### 本番の進行方法

- 会場開催/インターネット配信の想定
- 16人まででトーナメント
- 参加者が多い場合は事前に予選を行い、本番では決勝のみ配信

![ルッカ4](https://github.com/user-attachments/assets/dedcf021-fadd-4109-a6c4-d0ad22ba9a66)

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
│   │   ├── ComPlayerSample03.cs
│   │   └── ComPlayerSample03.prefab
│   └── Sample04/
│   │   ├── ComPlayerSample04.cs
│   │   ├── ComPlayerSample04.png
│   │   └── ComPlayerSample04.prefab
│   └── Sample05/
│       ├── ComPlayerSample05.cs
│       ├── ComPlayerSample05.png
│       └── ComPlayerSample05.prefab
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

<img src="https://github.com/user-attachments/assets/2581da80-0fa1-4c2a-b707-048a0b369406" width="50%">

### 挑戦者選択画面（Assets/Scenes/ParticipantSelection.scene）

その試合でバトルさせるAIを選択する画面です。<br>
AIは必ず4人選ぶ必要があります（重複可）。4人選ぶと「決定」ボタンを押せるようになります。<br>
「決定」ボタンを押すと、ゲーム画面へ遷移します。

<img src="https://github.com/user-attachments/assets/1b12f8c8-4996-4ee0-8fef-4460d8bab753" width="50%">

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

![ルッカ3](https://github.com/user-attachments/assets/dbf8e9ab-1804-4913-8b7f-1b74f426b470)

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

<img src="https://github.com/user-attachments/assets/ad24760f-41e6-4327-84f2-b5a54f507f77" width="50%"><br>

#### 2. 各項目を入力

■必須項目
- 受付番号： **connpassエントリー時に発行された受付番号** を入力<br>
[作成する前に](#entrypoint) を確認

■任意項目
- 所属名：実際に所属している会社名や学校名 or 架空の所属名<br>
- 挑戦者名：本名 or ニックネーム
- アイコン画像ファイル選択：アイコン画像ファイル（jpgかpng）を「参照」ボタンから選択（未選択可能）

※所属名・挑戦者名は、全角半角問わず最大10文字としてください。<br>
※アイコン画像ファイルの最大サイズは256*256です。<br>
※公序良俗に反する画像や名前は設定しないでください。<br>

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
- アイコン画像サイズは最大256*256とします
- 公序良俗に反する画像や名前は設定しないでください。
- AI作成時にUnityパッケージの追加はできません
- AI提出後、不正や目立った不具合が無いか弊社で審査いたします

![ルッカ2](https://github.com/user-attachments/assets/0ae8e351-9a1a-4658-8f33-78cf766dab17)

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

void UDON_ReportOnShipping(IList\<FoodType\> foodsList, int tableId, int price, string menuName);

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

AI作成時に扱う座標は全てローカル座標になります。<br>
ステージ中央を原点とし、どのプレイヤーから見ても必ず自身の出荷テーブルが後ろ側（Z座標がマイナス）に位置します。<br>

<img src="https://github.com/user-attachments/assets/b3e4d9d1-d247-4c91-917b-dd1888f762c4" width="50%"><br>

ステージ幅と出荷テーブル幅も、AI作成時に参考にしてください。

<img src="https://github.com/user-attachments/assets/c04f1c8e-86f2-45d1-8aad-6ee37789c858" width="50%">

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
■特徴：ちょっとかしこいやつ

食材やプレイヤーの位置関係、残り時間も考えて行動します。<br>
うどん玉を優先して狙います。<br>
メニューが成立するか、手持ちの食材がいっぱいになると自身の出荷テーブルへ運びます。<br>
いくらか経っても狙いの食材を拾えない場合、諦めて別の食材を狙います。

### Sample03（Assets/Participant/Sample03 以下）

■所属名：FM728<br>
■挑戦者名：蹴ルッカ<br>
■特徴：ずるがしこいやつ

Sample02の行動をベースに、他のプレイヤーに触れたらキックしようとします。

### Sample04（Assets/Participant/Sample04 以下）

■所属名：XEEN<br>
■挑戦者名：ぴよまる<br>
■特徴：オールラウンダーなやつ

出荷価格が高くなる食材を狙い、目の前に他プレイヤーがいたら蹴ります。<br>
他プレイヤーの出荷テーブルに近寄らないよう安全圏内を走り、ステージ外（出荷テーブルの外側）に出てしまった場合はステージから落ちます。

### Sample05（Assets/Participant/Sample05 以下）

■所属名：xeen<br>
■挑戦者名：ぼく<br>
■特徴：それなりのやつ

うどん玉を最優先に、自分から近い場所にある食材を狙おうとします。<br>
方向転換する際に速度を落として、滑りすぎないようにします。<br>
自分の出荷テーブルに向けて他プレイヤーを蹴ったり、うどんメニューが完成していないプレイヤーを蹴って誤って出荷させようとしたりします。<br>

![ルッカ1](https://github.com/user-attachments/assets/b4d7cc14-be64-4d1f-8a6f-5f75f73dfb50)

---

## 食材一覧

プレイヤーが拾う食材は、`FoodType`というenumで管理されています。

| 食材       | FoodType    | |
| ---------- | ------------- | --- | 
| うどん玉   | Noodle         | ![食材_うどん玉](https://github.com/user-attachments/assets/7c00b4e9-9a62-4b1f-84e7-c5b66e0872d7) | 
| 海老天     | ShrimpTempura  | ![食材_海老天](https://github.com/user-attachments/assets/a561dfb0-9f66-4c25-aa2a-5afb6fe8ac03) |
| ちくわ天   | ChikuwaTempura | ![食材_ちく天](https://github.com/user-attachments/assets/ee58b7a6-f826-41bf-bb21-4a14fc4ce709) |
| きつね     | Kitsune        | ![食材_きつね](https://github.com/user-attachments/assets/4ba7428b-47a1-4ce2-a1ef-a6357f48368b) |
| 大根おろし | GratedDaikon   | ![食材_大根](https://github.com/user-attachments/assets/4694fda8-cad9-4f21-a463-6fc4aca5ff21) |
| 卵         | Egg            | ![食材_卵](https://github.com/user-attachments/assets/a1301555-8d6e-4450-a253-4194e06339f7) | 
| 肉         | Meat           | ![食材_肉](https://github.com/user-attachments/assets/07c9dfa6-57cc-4766-886e-fcc10a251e05) |
| バター     | Butter         | ![食材_バター](https://github.com/user-attachments/assets/395ee572-58fd-46ca-b2d0-372b9ab473c5) |
| レモン     | Lemon          | ![食材_レモン](https://github.com/user-attachments/assets/bcc252cf-f29c-4d19-bdf0-1fc11b5657a7) |
| カレー     | Curry          | ![食材_カレー](https://github.com/user-attachments/assets/05d7a9a5-4dcd-4d7a-8070-853a59f54bb7) |

---

## うどんメニュー一覧

### うどんメニュー価格一覧

| メニュー名       | 価格 | 必要食材                                  | Bonus食材  | Bad食材        | |
| --------------- | ---- | ---------------------------------------- | ---------- | ------------- | --- |
| かけうどん       | 200  | うどん玉                                  |            | バター        | ![メニュー_かけうどん](https://github.com/user-attachments/assets/f3f84a97-cd06-413f-a465-5e1f8f83ae61) |
| おろしぶっかけ   | 320  | うどん玉<br>大根おろし                     |            | バター        | ![メニュー_おろしぶっかけ](https://github.com/user-attachments/assets/8ecfa1fa-2fc3-425a-8ea9-44178250213d) |
| 海老天うどん     | 400  | うどん玉<br>海老天                        | 海老天      | バター         | ![メニュー_海老天うどん](https://github.com/user-attachments/assets/1dd96691-d4f2-467f-8c30-b5fbf1821ca7) |
| ちく天ぶっかけ   | 550  | うどん玉<br>ちくわ天                      | ちくわ天    | バター         | ![メニュー_ちく天ぶっかけ](https://github.com/user-attachments/assets/17a7a671-a950-47f0-b139-3dbf24c893c4) |
| きつねうどん     | 320  | うどん玉<br>きつね                        | きつね     | バター         | ![メニュー_きつねうどん](https://github.com/user-attachments/assets/76a85321-4e88-4453-8399-6758b57ed83e) |
| 特上天ぷらうどん | 780  | うどん玉<br>海老天<br>ちくわ天             |            | バター         | ![メニュー_特上天ぷらうどん](https://github.com/user-attachments/assets/99538fbc-ea8a-419b-8085-762fd7cad244) |
| 釜玉うどん       | 300  | うどん玉<br>卵                           |            | バター         | ![メニュー_釜玉うどん](https://github.com/user-attachments/assets/e5e98512-71c9-4a12-9111-22bbfdf779c5) |
| 釜バターうどん   | 520  | うどん玉<br>卵<br>バター                  |            |                | ![メニュー_釜バターうどん](https://github.com/user-attachments/assets/d1543ea0-b336-4052-9fbe-885c1a03f32d) |
| 肉うどん         | 450  | うどん玉<br>肉                           | 肉         | バター         | ![メニュー_肉うどん](https://github.com/user-attachments/assets/89eb34de-2a69-4359-a739-ce8979eedf07) |
| 肉ぶっかけ       | 500  | うどん玉<br>肉<br>レモン                  | 肉         | バター         | ![メニュー_肉ぶっかけ](https://github.com/user-attachments/assets/80772ddf-111a-4411-9058-6ea341b0443d) |
| 肉釜玉うどん     | 550  | うどん玉<br>肉<br>卵                      | 肉         | バター         | ![メニュー_肉釜玉](https://github.com/user-attachments/assets/5c78b862-7bef-40ef-8e02-9ef7b5a83552) |
| カレーうどん     | 400  | うどん玉<br>カレー                        |            | バター<br>大根 | ![メニュー_カレーうどん](https://github.com/user-attachments/assets/759b32a4-8e70-4b4b-b014-2c1a6a543076) |
| 肉カレーうどん   | 970  | うどん玉<br>肉<br>カレー                  | 肉         | バター<br>大根 | ![メニュー_肉カレーうどん](https://github.com/user-attachments/assets/792a5a6c-c63a-40ec-a7eb-032e56ea5ab3) |
| エックスうどん   |  2700 | うどん玉<br>海老天 ×2<br>肉<br>レモン     |            | バター         | ![メニュー_エックスうどん](https://github.com/user-attachments/assets/a6a4e21e-6e38-4028-9932-16fd3d0b0ba2) |

※ゲーム内では拾った食材を積み上げているため、メニュー画像はイメージです。

![ルッカ5](https://github.com/user-attachments/assets/94b21063-2448-46a1-b3ff-cc40732b96a4)

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
