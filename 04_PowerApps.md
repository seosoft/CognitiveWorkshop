# PowerApps で画像解析アプリを開発する

[**PowerApps**](https://powerapps.microsoft.com/ja-jp/) は簡単にアプリケーションを開発できるツールです。

<img src="Assets/Images/powerapps_toppage.png" width="420px" />
<img src="Assets/Images/powerapps_designpage.png" width="420px" />

PowerApps は「ノンコーディング」と言われることもありますが、Excel の関数を活用する程度の知識はあるほうが有利です。 <br />
とはいえ、PowerApps で利用する関数はそれほど数が多くはありません。少しずつ理解を深めることは可能でしょう。<br /><br />

---
このハンズオンでは、前の手順で作成した [**土器判定 Custom Vision**](02_CustomVision.md) を利用するアプリケーションを作ります。 <br /><br />

カメラで撮影した土器が、縄文土器なのか弥生土器なのかを判定するアプリです。<br />
（実際の土器を持っている人はあまりいないと思います・・・ので、今回はスマホに表示した土器の写真を PC のカメラに向けることにします）

<img src="Assets/Images/dokiapp_sample.png" width="420px" />

---

## Custom Vision の Project ID、キーを確認

PowerApps から Custom Vision を利用するには、Project ID および Prediction Key が必要になります。<br />
アプリを作り始める前に、まずこれらの値を確認しておきます。<br />

1. Custom Vision にサインインします。<br />
[**Custom Vision**](https://customvision.ai/) を開いてサインインします。<br />
<img src="Assets/Images/cv_toppage_for_getting_key.png" width="420px" /><br /><br />

2.  Custom Vision の Project ID と Prediction Key とを確認します。<br />
サインインに成功したら、前の手順の [**土器判定 Custom Vision**](02_CustomVision.md) プロジェクトを選択します。 <br />
**Settings** アイコン (歯車アイコン)をクリックして設定画面を開き、**Project ID** および **Prediction Key** をメモ帳などにコピーします。これらの値は後で使います。<br />
<img src="Assets/Images/cv_selectproject_for_getting_key.png" width="420px" /><br />
<img src="Assets/Images/cv_projectid_predkey.png" width="420px" /><br /><br />

---

## PowerApps で Custom Vision に接続

PowerApps では、外部の Web サービスを利用するには、事前にそのサービスの Connector を登録しておく必要があります。<br />
PowerApps のアプリで Custom Vision を利用する際には、以下の手順で Connector を登録します。<br />

1. [**PowerApps**](https://web.powerapps.com/) にサインインします。<br />
<img src="Assets/Images/powerapps_homepage.png" width="420px" />

2. ホームページの左ペインで **データ** - **接続** をクリックします。 <br />
<img src="Assets/Images/powerapps_select_connector.png" width="420px" />

3. **新しい接続** をクリックします。<br />
<img src="Assets/Images/pa_new_connector.png" width="420px" />

4. **検索窓** に「custom vision」と入力してから、**Custom Vision** をクリックします。<br />
<img src="Assets/Images/pa_new_connector_cv.png" width="420px" />

5. **Custom Vision** の設定をします。<br />
Custom Vision のサイトでコピーしておいた **Prediction Key** を入力します。<br />
(Project ID は後で使います。ここでは Prediction Key だけです)<br />
<img src="Assets/Images/pa_cv_setting.png" width="420px" />

---

## 新しいアプリの開発

ここまでで、新しく PowerApps アプリ開発の準備が整いました。<br /><br />

1. PowerApps のホームページで、左ペインの **アプリ** をクリックします<br />
<img src="Assets/Images/pa_menu_app_for_newapp.png" width="420px" />

2. **アプリの作成** をクリックします。<br />
<img src="Assets/Images/pa_newapp_button.png" width="420px" />

3. レイアウトを選択してアプリを作成します。<br />
今回は **空のアプリ** の **携帯電話レイアウト** を選択します。<br />
<img src="Assets/Images/pa_newapp_blank_phone_template.png" width="420px" />

4. PowerApps アプリのデザイン画面が開きます。<br />
<img src="Assets/Images/pa_newapp_design.png" width="420px" />

---

## アプリの設定

アプリの画面デザインをする前に、アプリ名とアイコンを設定して、まず一度保存しておきます。

1. PowerApps アプリのデザイン画面で **ファイル** を選択します。<br />
<img src="Assets/Images/pa_menu_file.png" width="420px" />

2. **アプリの設定** を選択して、アプリ名およびアイコンを設定します。<br />
<img src="Assets/Images/pa_appsettings.png" width="420px" />

3. アプリを保存します。<br />
**名前を付けて保存** をクリックしてから、**保存** ボタンをクリックします。<br />
<img src="Assets/Images/pa_saveas_and_save.png" width="420px" />
<br /><br />
PowerApps では保存が自動的に実行されるので、普段は保存についてはあまり意識する必要はありません。<br />
ただしアプリに大きく手を入れた時やアプリ開発の中断・終了の前には、念のため明示的に保存するのがいいかもしれません。

4. アプリのデザイン画面に戻ります。<br />
保存に成功したら、左上の **←** (Web ブラウザーの戻るボタンではありません) をクリックして、デザイン画面に戻ります。<br />
<img src="Assets/Images/pa_back_to_design.png" width="420px" />

---

## 画面のデザイン

いよいよ PowerApps 開発の本体に入ります。

1. コントロールを配置して、画面をデザインします。<br /><br />
配置するコントロールは、今回は 4個です。<br />
デザイン画面のメニューの **挿入** を選択するとコントロールの一覧が表示されます。<br />
コントロールを選択するとスクリーン上に置かれます。位置やサイズを適宜変更してください。<br />
<img src="Assets/Images/pa_layout_control.png" width="420px" />
<img src="Assets/Images/pa_layout_all_controls.png" width="420px" /><br />

- カメラ ・・・ **メディア** - **カメラ**
- 画像 ・・・ **メディア** - **画像**
- ラベル ・・・ コントロール一覧の **一番左**
- ラベル (※ラベルは 2個配置)

---

## アプリのプレビュー (カメラコントロールの動作確認)

ここで一度、アプリをプレビュー実行してみます。

1. 右上の **アプリのプレビュー** をクリックします。<br />
PowerApps の画面が、アプリのプレビューのみになり、実際に動作します。<br />
<img src="Assets/Images/pa_app_start_to_preview.png" width="420px" />
<img src="Assets/Images/pa_app_previewing.png" width="420px" />
<br />
コントロールを配置しただけですが、カメラコントロールが動作していることが分かります。

2. プレビューを閉じます。<br />
プレビューの右上の **×** をクリックしてプレビューを閉じます。デザイン画面に戻ります。

---

## Custom Vision をデータに追加

カメラで撮影した画像を Custom Vision に送信するために、PowerApps のデータに Custom Vision を追加します。<br /><br />
先ほどは PowerApps 環境全体で Custom Vision に接続する設定をしました。<br />
ここでは **作成しているアプリ** で Custom Vision に接続するための手順です。

1. メニューの **ビュー** - **データソース** を選択して、データパネルが開いたら **データソースの追加** をクリックします。<br />
<img src="Assets/Images/pa_view_datasource_addds.png" width="420px" />

2. **新しい接続** をクリックします。<br />
<img src="Assets/Images/pa_datapanel_addconnection.png" width="420px" />

3. **Custom Vision** をクリックします。<br />
<img src="Assets/Images/pa_datapanel_cv.png" width="420px" />

4. Custom Vision の **Prediction Key** を入力します。<br />
Prediction Key は先ほどの手順で、Custom Vision の設定ページからメモ帳などにコピーしているはずです。<br />
<img src="Assets/Images/pa_datapanel_cv_predictkey.png" width="420px" />

以上の手順で、作成しているアプリから Custom Vision に接続できるようになりました。

---

## プロパティ値の設定（カメラコントロールの OnSelect）

PowerApps ではいわゆるコーディングは行いませんが、**Excel の関数** と似た感じで、コントロールの **プロパティに変数の名前や関数などを設定** していきます。<br />
以下の手順が、一般的なアプリケーション開発におけるコーディングに相当します。

1. 配置したカメラコントロールをクリックしてアクティブにし、左上の **プロパティ選択** で **OnSelect** を選択します。<br /><br />
カメラコントロールの OnSelect とは、アプリ実行時にカメラコントロールでクリックまたはタップした時に実行される処理のことです。<br /><br />
<img src="Assets/Images/pa_camera_onselect.png" width="420px" />

2. **プロパティ値** (デフォルトでは "False" と表示されている) を選択して、ここで実行する関数を以下のように入力します。<br />
以下の **<<Custom Vision の Project ID>>** の部分は、メモ帳などにコピーしておいた Custom Vision の Project ID に置き換えます。<br />
<img src="Assets/Images/pa_camera_onselect_func.png" width="420px" /><br />

```
Set(pic, Camera1.Photo);
Set(predres, CustomVision.PredictImage("<<Custom Vision の Project ID>>", pic).Predictions)
```

1 行目: カメラコントロールの画像を pic という名前の変数に代入<br />
2 行目: pic 変数の中身 (= カメラコントロールの画像) を Custom Vision に渡して、戻ってきた値を predres 変数に代入
<br /><br />

3. プレビュー実行して、手順の間違いやタイプミスなどがないことを確認します。<br />
**Alt キー** を押しながら、カメラココントロールをクリックします。<br /><br />
PowerApps は画面右上のプレビュー実行アイコンで実行する以外にも、**Alt キー** を押しながらマウス操作することで、デザイン画面のままでもプレビュー実行可能です。<br />
タイプミスがないかを確認する程度ならば、画面切り替えが不要である Alt キーを押しながらのプレビュー実行が便利です。<br />
<img src="Assets/Images/pa_preview_with_altkey.png" width="420px" /><br /><br />
※タイプミスなどのエラーがある場合は、Alt + クリックすると、エラーがあるコントロールの左肩に **×** アイコンが表示されます。x アイコンにカーソルを合わせるとエラー内容が表示されます。<br />
<img src="Assets/Images/pa_preview_with_error.png" width="420px" /><br />

5. プレビュー実行に成功したことを確認します。<br /><br />
カメラコントロールの OnSelect プロパティでは、カメラ画像を **pic** 変数に代入し、Custom Vision の結果を **predres** 変数に代入する処理を書きました。<br />
メニューの **ビュー** - **変数** をクリックすると、これらの変数が生成されています。これでプレビュー実行に成功したことが分かります。<br />
<img src="Assets/Images/pa_view_variables.png" width="420px" />
<img src="Assets/Images/pa_show_variables.png" width="420px" />
<br /><br />
**変数を選択** の pic をクリックすると、実際に代入されたカメラ画像を確認することができます。<br />
<img src="Assets/Images/pa_variables_pic.png" width="420px" />

---

## プロパティ値の設定（残りのコントロール）

カメラコントロール以外のコントロールについてもプロパティを設定して、アプリを完成させます。

1. 画像コントロールのプロパティを設定します。<br />
画像コントロールをクリックして、プロパティ選択が **Image** になっていることを確認します。プロパティ値として **pic** と入力します。<br />
前の手順で確認した pic 変数の画像が表示されます。もし画像が表示されなかったら、プロパティの選択が間違っているか、タイプミスがあります。<br />
<img src="Assets/Images/pa_image_property.png" width="420px" />

2. ラベルコントロールのプロパティを設定します。<br />
一つ目のラベルを選択して、プロパティ選択が **Text** になっていることを確認し、プロパティ値には **First(predres).Tag** と入力します。<br />
二つ目のラベルのプロパティ値は **First(predres).Probability** とします。<br /><br />
<img src="Assets/Images/pa_label1_property.png" width="420px" />
<img src="Assets/Images/pa_label2_property.png" width="420px" /><br />
プロパティ値としてどちらも先頭に **First** を付けています。<br />
Custom Vision は画像の分類で複数の候補を返してくるため、一番可能性が高い分類を選択するために指定するのが **First** です。<br /><br />

以上で、PowerApps アプリ作成は完了です。最後にもう一度プレビュー実行してみます。

---

## プレビュー実行でアプリの完成を確認

手順通りに作っていれば、[**土器判定 Custom Vision**](02_CustomVision.md) プロジェクトを呼び出しています。<br />
今回作ったアプリケーションは、カメラで撮影したものが、縄文土器か弥生土器かに分類します。<br /><br />

アプリを PC で実行する場合は、スマホで土器の写真を検索して、それを PC のカメラに向けることにします。<br /><br />

1. アプリをプレビュー実行します。
2. スマホで、土器の写真を検索して PC のカメラに向けます。
3. アプリのカメラコントロールをクリックします。
4. 撮影されたものが画像コントロールに表示され、Custom Vision を呼び出します。少し待つと、"Jomon" または "Yayoi" の分類とその可能性が表示されます。<br />
<img src="Assets/Images/pa_preview_final.png" width="420px" />

---
PowerApps を使うと、複雑なコーディングをしなくてもアプリケーションを作成できることが分かったと思います。<br /><br />

この後は、PowerApps アプリの **発行** (＝アプリをクラウドに配置) して、権限のあるユーザーがアプリを利用できるようにする手順があります。<br />
このワークショップは Custom Vision プロジェクトの操作を主な目的としているので、PowerApps アプリの発行の手順は扱いません。

**考察** <br />
PowerApps アプリの発行の手順や、スマホでの利用の手順について、調査してみましょう。