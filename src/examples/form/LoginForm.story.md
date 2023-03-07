# ex. Login Form

シンプルなログインフォームの実装サンプルです。
Emailに `example@example.com` を入力すると成功時の挙動を、それ以外のアドレスを入力すると失敗時の挙動を試すことができます。

## 利用しているコンポーネント

### layout/CCover

フォーム全体をページの上下中央寄せにするために利用しています

### layout/CCenter

フォーム全体を、ページの左右中央寄せにするために利用しています

### layout/CBox

フォーム全体にpaddingを取るために利用しています

### layout/CStack

フォーム内の部品同士の間に一定のmarginを取りつつ、上下方向へ配置するために利用しています

### layout/CCluster

ログインボタンとパスワードリセットリンクの２つの要素を以下のように配置するために利用しています

* 表示画面幅に余裕がある場合（デスクトップなど）は左右方向へ
* 表示画面幅に余裕のない場合（モバイル端末など）は上下方向へ

### form/CTextField

メールアドレスとパスワードの入力フィールドとして利用しています

### form/CButton

ログインボタンとして利用しています