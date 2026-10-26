# Active Directory ユーザー管理

## 概要

Active Directory を構築し、ユーザーを作成し、組織単位（OU）を利用して管理する。

## 構成図

```text
vegeshop.local
│
├─ Vegetable
│   ├─ Carrot
│   ├─ Tomato
│   └─ Onion
│
└─ Fruit
    ├─ Apple (Administrators)
    ├─ Orange
    └─ Grape
```

## 実施内容

- Active Directory Domain Services（AD DS）インストール
- ドメインコントローラー構築
- ドメイン作成
- OU（組織単位）作成
- ユーザー作成
- グループ管理
- ドメインユーザーでのログオン確認
- Administrators グループへのユーザー追加
- リモートデスクトップ接続の検証
- Administrator と admin ユーザーの同時接続確認

---

## 1. Active Directory を構築する

### 1-1. AD DS をインストールする

[サーバーマネージャー ] > [ 管理 ] > [ 役割と機能の追加 ]
![画像](../Images/ActiveDirectory/1.jpg)

### 1-2. インストールの種類を選択する

[開始する前に ] > [ 次へ ]
[ インストールの種類の選択 ] > [ 役割ベースまたは機能ベースのインストール ]
![画像](../Images/ActiveDirectory/2.jpg)

### 1-3. Active Directory Domain Services を選択する

[ 対象サーバーの選択 ] > [ サーバープールからサーバーを選択 ] > [ 次へ ]
![画像](../Images/ActiveDirectory/3.jpg)

[ サーバーの役割の選択 ] > [ Active Directory Domain Services ] > [ 機能の追加 ] > [ 次へ ] 
![画像](../Images/ActiveDirectory/4.jpg)

### 1-4. インストールする

[ 機能 ] > [ 次へ ]
![画像](../Images/ActiveDirectory/5.jpg)

[ Active Directoryドメインサービス ] > [ 次へ ]
![画像](../Images/ActiveDirectory/6.jpg)

[ インストール オプションの確認 ] > [ 必要に応じて対象サーバーを自動的に再起動する✓ ] > [ はい ] > [ インストール ]
![画像](../Images/ActiveDirectory/7.jpg)
![画像](../Images/ActiveDirectory/8.jpg)

インストールが完了した後 [ 閉じる ]
![画像](../Images/ActiveDirectory/9.jpg)

### 1-5. ドメインコントローラーへ昇格する

ダッシュボードにて、[ AD DS ]がインストールされたことを確認
右側上部の 🚩（旗） ] > [ このサーバーをドメインコントローラーに昇格する ]
![画像](../Images/ActiveDirectory/10.jpg)

### 1-6. 新しいフォレストを作成する

[ 配置構成 ] > [ 新しいフォレストを追加する ] > [ ルートドメイン名（vegeshop.local） を入力 ] > [ 次へ ] 
![画像](../Images/ActiveDirectory/11.jpg)

### 1-7. DSRM パスワードを設定する

[ ドメインコントローラーオプション ] > [ ディレクトリサービス復元モード（DSRM）のパスワードを記入 ] > [ 次へ ] 
![画像](../Images/ActiveDirectory/12.jpg)

[ DNSオプション ] > [ OK ]  > [ 次へ ] 
![画像](../Images/ActiveDirectory/13.jpg)

[ 追加オプション ] > [ 次へ ] 
![画像](../Images/ActiveDirectory/14.jpg)

[ パス ] > [ 次へ ] 
![画像](../Images/ActiveDirectory/15.jpg)

[ オプションの確認 ] > [ 次へ ] 
![画像](../Images/ActiveDirectory/16.jpg)

[ 前提条件のチェック ] > [ インストール ] 
![画像](../Images/ActiveDirectory/17.jpg)

### 1-8. ドメイン作成完了

正常にフォレストが追加され、[ ドメイン ] が [ vegeshop.local ] になっている。
![画像](../Images/ActiveDirectory/18.jpg)

---

## 2. ユーザーを作成し、OUで管理する

### 2-1. Active Directory ユーザーとコンピューターを開く

[サーバーマネージャー ] > [ ツール ] > [ Active Directory ユーザーとコンピューター ]
![画像](../Images/ActiveDirectory/19.jpg)

### 2-2. ユーザーを作成する

[ vegeshop.local（右クリック） ] > [ Users ] > [ 新規作成 ] > [ ユーザー ]
![画像](../Images/ActiveDirectory/20.jpg)

[ フルネーム（Carrot）] > [ ユーザーログオン名（Carrot） ] > [ 次へ ]
![画像](../Images/ActiveDirectory/21.jpg)

[ パスワード（任意の条件確認） ] > [ 次へ ] > [ 完了 ]
ユーザー（Carrot）作成済み
![画像](../Images/ActiveDirectory/22.jpg)
![画像](../Images/ActiveDirectory/23.jpg)
![画像](../Images/ActiveDirectory/24.jpg)

# 2-3. OU（組織単位）を作成する

[ vegeshop.local（右クリック） ] > [ 新規作成 ] > [ 組織単位(OU) ]
![画像](../Images/ActiveDirectory/25.jpg)

[ 名前（Vegetable）] > [ OK ]
![画像](../Images/ActiveDirectory/26.jpg)

組織単位(OU)（ Vegetable ）（ Fruit ） 作成済み
![画像](../Images/ActiveDirectory/27.jpg)

### 2-4. OU 配下にユーザーを作成する

[ 組織単位(OU)（右クリック） ] > [ 新規作成 ] > [ ユーザー ]
![画像](../Images/ActiveDirectory/28.jpg)

組織単位(OU)（ Vegetable ）にユーザー（Carrot）（Tomato）（Onion） 作成済み
![画像](../Images/ActiveDirectory/29.jpg)

組織単位(OU)（ Fruit ）にユーザー（Apple）（Orange）（Grape） 作成済み
![画像](../Images/ActiveDirectory/30.jpg)

---

## 3. ドメインユーザーでログオンする

### 3-1. Apple を Administrators に追加する

一般グループ（Domain Users）ではログオン権限が不足するため、
ユーザー（Apple）のみ管理者グループ（Administrators）に所属させADサーバー（vegeshop.local）にサインインする。
![画像](../Images/ActiveDirectory/31.jpg)
![画像](../Images/ActiveDirectory/32.jpg)

[サーバーマネージャー ] > [ ツール ] > [ Active Directory ユーザーとコンピューター ] > [ Fruit（右クリック） ] > [ ユーザー（Apple） ] > [ プロパティ ] > [ 所属するグループ ] > [ Administrators ] > [ 名前の確認 ] > [ 適用 ] > [ OK ]
![画像](../Images/ActiveDirectory/33.jpg)
![画像](../Images/ActiveDirectory/34.jpg)

### 3-2. Apple でサインインする

[ スタートメニュー ] > [ サインアウト ] > [ ユーザー（Apple）でサインイン ]し成功！
![画像](../Images/ActiveDirectory/35.jpg)
![画像](../Images/ActiveDirectory/36.jpg)

---

## 参考

- [ActiveDirectory構築、ADユーザー作成を実施する（GUI） #AWS - Qiita](https://qiita.com/gorilla_infra/items/9140b8bdef871f875eea#はじめに)

---

## 4. 管理者ユーザーを作成し、リモートデスクトップ接続を検証する

### 4-1. 管理者ユーザーを作成する

ユーザー **admin** を作成し、Administrators グループへ追加した。

```text
vegeshop.local
↓
Users
↓
admin
↓
プロパティ
↓
所属するグループ
↓
Administrators
```
![画像](../Images/ad-users/1.png)

---

### 4-2. 接続確認（成功パターン）

#### 検証内容

- 仮想マシン：Administrator でログイン
- ローカルPC：admin でリモートデスクトップ接続

#### 結果

✅ 同時ログイン成功
仮想マシンではAdministratorでログイン、ローカルではユーザーadminでリモートデスクトップからログイン、同接可！！
![画像](../Images/ad-users/2.png)
![画像](../Images/ad-users/3.png)
![画像](../Images/ad-users/5.png)

---

### 4-3. 接続確認（失敗パターン）

#### 検証内容

- 仮想マシン：Administrator
- ローカルPC：Administrator

#### 結果

❌ 同時ログイン不可
同一アカウント（Administrator）での同時接続はできなかった。
![画像](../Images/ad-users/4.png)

---

## 学んだこと

- Active Directory Domain Services（AD DS）のインストール方法を学んだ。
- ドメインコントローラーへの昇格手順を学んだ。
- 新しいフォレストとドメインを作成できるようになった。
- OU（組織単位）を利用してユーザーを論理的に管理できることを学んだ。
- Active Directory からユーザーアカウントを作成できるようになった。
- ユーザーを Administrators グループへ追加する方法を学んだ。
- ドメインユーザーで Windows Server にサインインできることを確認した。
- OU を活用することで組織や部署ごとにユーザー管理できることを理解した。
- Administrator とは別の管理者ユーザーを作成することで同時接続できることを確認した。
- リモートデスクトップ接続時は利用するアカウントによって接続結果が異なることを学んだ。

