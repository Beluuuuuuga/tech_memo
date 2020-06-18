## はじめに 
Global Wheat Detectionは物体検出コンペで、画像内の小麦を検出します。

このコンペティションでは、CSVの提出方法がカーネルでの提出になっており、コンペのディスカッションでもSubmission Scoring Errorについての質問が
多く挙げられてるなど、提出にくせがあります。

今回、カーネル内での提出方法を記述しています。

## 方法
1. NoteBookを作成
2. モデルの重みファイルをアップロード
3. 重みファイルをロードし推論し、submission.csvを作成（異なる名前だと提出できないので注意）
4. NoteBookの設定でInternetを接続可能にする
5. 保存の際にSaveVersionでCommitを選択する
5. 自分のNoteBook一覧に移動し、subimission.csvをSubmitするラジオボタンを押して提出
