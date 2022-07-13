ansibleのローカルテスト環境

起動
$ docker-compose --compatibility up -d --build


停止
$ docker-compose down


ログイン
dev-ansible-managerにアタッチ。
$ su ansible-manager
$ cd /home/ansible-manager/ansible

テスト実行（dev-ansible-managerからdev-ansible-targetに向かって実行している。）
$ ansible-playbook -i inventories/dev/hosts playbooks/dev/dev.yml


困った時
CentOSで、docker container内で、Systemdを利用する方法
https://hub.docker.com/_/centos?tab=description


Docker for mac (ver 4.3以降) で「Failed to get D-Bus connection」エラーが出たときの対処法
→CGroupV2ではなく、CGroupV1を利用するように切り替える。
https://qiita.com/NaoyaMiyagawa/items/22a870112377a91e1c99

