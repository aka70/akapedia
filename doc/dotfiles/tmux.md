# tmux

- prefix + c : 新しくウィンドウを作成する。
- prefix + & : カレントウィンドウを削除する。
- prefix + d : デタッチ

- `tmux ls`でデタッチしたセッション一覧を表示
- `tmux attach -t ${番号}`で指定したセッションに再接続
- `tmux new-session`で新しくセッションを開く
- `tmux kill-session -t ${番号}`でセッションの削除
