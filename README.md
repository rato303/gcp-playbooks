# 準備

1. GCPでansible実行用のサービスアカウントを作成
2. ${project}/.ssh/配下にansible用の鍵を作成
    - `ssh-keygen -t ed25519 -f .ssh/id_ed25519_ansible -C "準備1で作成したサービスアカウントのメールアドレス"`
    - ※. 1で準備したサービスアカウント用のssh鍵
3. ${project}/inventory配下に次のファイルを作成
    - inventory/inventory.gcp.yml
        - 参考：https://docs.ansible.com/ansible/2.7/plugins/inventory/gcp_compute.html
    - inventory/group_vars/all/vars.yml
4. ${project}/credential.jsonファイルを作成
    - GCPでansible用のサービスアカウントの認証用jsonファイルをダウンロードして配置する

ex.) inventory/group_vars/all/vars.yml
```
gcp_project: 利用するプロジェクトID
gcp_cred_kind: serviceaccount
gcp_cred_file: ../credential.json
gce_service_account_email: プロジェクトのGCEのデフォルトサービスアカウントを指定する
service_account_email: 準備1で作成したサービスアカウントのメールアドレス
gce_ssh_keys: |-
  ansible: 準備の2で作成したsshの公開鍵を貼り付ける。複数行記載可
```