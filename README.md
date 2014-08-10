# Ansibleサンプル

## Vagrant準備

```
$ vagrant box add opscode-centos-6.5 http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_centos-6.5_chef-provisionerless.box
```

## playbook実行

#### すべて実行

```
$ ansible-playbook -i production site.yml
```

#### webserversグループのみ実行

```
$ ansible-playbook -i production webserver.yml
```

もしくは

```
$ ansible-playbook -i production site.yml -limit webservers
```

## inventory file

* porduction
* stage

このサンプルはVagrantを使ってて、`production`も`stage`も同じ設定。

`webservers`と`dbservers`の２つのグループを設定

## Role

### common

共通ロール

* epel, remiリポジトリ追加
* libselinux-pythonインストール（これ無いとどっかでエラーになる。忘れた…
* vimインストール
* gitインストール

### web

Webサーバー

* nginxインストール
* rbenvインストール
* rubyインストール

### db

dbサーバー

* mysqlインストール

## ansible.cfg

ぼくの環境だとsshの時に`Too many authentication failures for`ってエラーがよく出るのでsshの引数を設定している。

## TODO

* nginxのconf
* mysqlのconf
* iptable設定

