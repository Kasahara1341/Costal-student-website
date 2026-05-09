# サーバーPCの使い方

## 目次
- [サーバーpcの使い方](#サーバーpcの使い方)
  - [目次](#目次)
  - [VS CodeによるサーバーPCへの接続方法](#vs-codeによるサーバーpcへの接続方法)
  - [基本的な操作方法とルール](#基本的な操作方法とルール)
    - [基本的な操作方法](#基本的な操作方法)
    - [基本的なルール](#基本的なルール)
  - [サーバー上でのLatexによる執筆](#サーバー上でのlatexによる執筆)

## VS CodeによるサーバーPCへの接続方法
VS Codeの拡張機能として「Remote-SSH」をインストールする．
![](figure_howToUseServer/RemoteSSHVScode.png)
*Remote-SSHの導入*
リモートエクスプローラーが追加されるので，クリックしカーソル
をsshに合わせると「新しいリモート」が選択できるのでクリックする．

上中央に入力欄が出るので，ssh "name"@"ipaddress"を入れる．
ここで"name"は接続先のユーザー名であり，"ipaddress"は接続先のアドレスである．例として，ユーザー名"hoge"，アドレス"123.45.678.990"に接続する場合は\
ssh hoge@123.45.678.990 \
と入力する．

Select the platform of the remote hostと出るので，サーバーPCのOSを選択する（基本的にはLinux）

上中央にパスワード入力欄が出るので，所定のパスワードを入力すると接続される．

図のように
1. エクスプローラー
2. フォルダーを開く
3. /data/ubuntu/home/"name"/　でOKを押すことで，VS Code左側のエクスプローラーのカレントディレクトリを設定できる．
![](figure_howToUseServer/FolderSelect.png)
*接続先でのフォルダ選択*


## 基本的な操作方法とルール
### 基本的な操作方法
1. ファイル・フォルダ操作は基本的に左側にあるエクスプローラーの欄で行える右クリックでファイル作成・フォルダ作成・ダウンロードなどが可能
2. フォルダを右クリックで選択し「統合ターミナルで開く」を選択することで，そのフォルダをカレントディレクトリとしてターミナル(windowsでのコマンドプロンプト)を開くことができる
3. ターミナルではファイル作成，複製，gitコマンドなどが実行できる

### 基本的なルール
1. /data/ubuntu/home/"name"/ (ターミナル上では~/と表示される．左側のエクスプローラーでは.bashrcや.profileが存在するディレクトリ(階層))に各ユーザーごとのフォルダを作成し，自身のフォルダ内のみで作業を行うこと．他人のディレクトリは触らない．
2. 他人に誤って削除される恐れがあるため，共有アカウント内に置くファイルは消されても大丈夫なもののみにすること（自身のPCにバックアップを取っておくなど）
3. 上記の条件に沿っていればディレクトリ(フォルダ)・ファイルの作成は自由
4. Pythonは基本的に各ユーザーごとに仮想環境を構築して利用する（構築方法などは後述）．仮想環境は各ユーザーのディレクトリ内に作成すること

## Python仮想環境の作成と起動方法
1. 自身のディレクトリ内でターミナルを起動する
2. ターミナルで"python3 -m venv my_env"を実行する．→ディレクトリ内にmy_envが作成される．
この"my_env"部分は任意の名前で良い．他の名前にした場合はその名前で仮想環境が生成される．
3. source コマンドで作成した環境を起動する．例として，my_envで作成した場合は\
source my_env/bin/activate\
とする．起動するとターミナルに図のような環境名が表示される．\
![](figure_howToUseServer/pythonVenvActivate.png)
*Python 仮想環境の起動*

## サーバー上でのLatexによる執筆
texがインストールされているサーバーPC上でtexファイルを開くと，ファイルを示すタブの右側に緑枠の三角などが表示される． \
これらはtex⇒pdfの作成やpdf表示のショートカットボタンである．\
この機能を利用するにはローカルPCのVS Codeの拡張機能に"LaTeX Workshop"が入っている必要があると思われる．
![](figure_howToUseServer/tefEditDisplay.png)
*texファイル編集画面*
tex⇒pdfの作成は"ctrl + s"による保存でも実行され，pdf表示をしている場合作成されるたびに変更内容が反映される．

### スニペット機能の利用
VS Codeでtexを編集する際の便利な機能の一つとしてスニペット機能が挙げられる．\
これは登録しておいたコード一式の記述を特定の記述で呼び出す機能であり，特に式・図・表のひな型を登録しておくと執筆効率が向上する．
![](figure_howToUseServer/snipet.png)
*スニペットによる呼び出し*
例えば上の図では"figure"というキーワードで図中右側に示される図掲載用のコード一式を呼び出そうとしている．texで式・図・表を記述するためには基本的に\begin{} \end{}が必要なので，複数回式などを記述する場合にはスニペットを利用することで執筆をより効率的に行える．

スニペットはVS Code左下の歯車から登録が可能である．
![](figure_howToUseServer/OpenSnipet.png)
*スニペット設定の開き方*
「スニペット」をクリックすると中央上の欄に「スニペット ファイルの選択かスニペットの作成」とでる．
初めて開く場合は"latex.json"と入力してEnterを押す．二回目以降は"latex.json"があるはずなので選択する(二回目以降でもlatex.jsonと入力してもよい)．

latex.jsonでは下図のようにスニペットを登録できる
163行目”figure”:{　は登録名
Prefixでは呼びだすためのキーワードを指定
Bodyで展開したいコードを書く(バックスラッシュを登録する場合は図のように二回入力する)
Descriptionは説明（空欄でもよい）
![](figure_howToUseServer/snipetEx.png)
*スニペット登録例*
以下にいくつかスニペット登録例を示す．
```json
{
	"source_code":{
		"prefix": "source_code",
		"body":[
			"\\begin{lstlisting}[caption=,label=]",
			"",
			"\\end{lstlisting}",
		],
		"description": "コードのテンプレート"
	},

	"table":{
		"prefix": "table",
		"body":[
			"\\begin{table}[t]",
			"\\centering",
			"\\caption{}",
			"\\label{}",
			"\\begin{tabular}{cc}",
			  "\\hline",
			  "\\hline",
			"\\end{tabular}",
		  "\\end{table}",
		],
		"description": "表のテンプレート"
	},
	"figure":{
		"prefix": "figure",
		"body":[
			"\\begin{figure}[t]",
			"\\centering",
			"\\includegraphics[width=75mm]{}",
			"\\caption{}",
			"\\label{}",
     		"\\end{figure}  ",
		],
		"description": "図のテンプレ"
	},
	"reffig":{
		"prefix": "reffig",
		"body": [
		"\\textbf{図-\\ref{fig:}}",
		],
		"description": "図を本文中で引用する際のテンプレ"
	},
	"figure_tabular":{
		"prefix": "figure_tabular",
		"body":[
			"\\begin{figure}[t]",
			"\\centering",
			"\\begin{tabular}{cc}",
			  "\\begin{minipage}[t]{0.45\\hsize}",
				"\\includegraphics[keepaspectratio, scale=0.5]{}",
			  "\\end{minipage} &",
			  "\\begin{minipage}[t]{0.45\\hsize}",
				"\\includegraphics[keepaspectratio, scale=0.5]{}",
			  "\\end{minipage} \\",
			"\\end{tabular}",
			"\\caption{}",
			"\\label{}",
		  "\\end{figure}  ",
		  
		],
		"description": "図を表の形式で並べる際のテンプレ"
	},
	"equation":{
		"prefix": "equation",
		"body":[
			"\\begin{align}",
			"\\label{}",
     		"\\end{align}  ",
		],
		"description": "式のテンプレート"
	},
	"enumerate":{
		"prefix": "箇条書き",
		"body":[
		"\\begin{enumerate}",
        	"\\item ",
		"\\end{enumerate}",
		],
		"description": "数字の箇条書き"
	}

}
```