# git-allsync

Copyright 2023 Kenshi Muto

## 概要

カレントの直下にある複数の Git リポジトリフォルダに対し、`git pull` をかけます。リポジトリがたくさんあって、作業前の各 pull を忘れがちという場面を想定しています。

この手のツールとしては Debian の Joey Hess 氏が作った [myrepos](http://myrepos.branchable.com/) が有名ですが、もう少し手元用に軽量なのがほしくて作りました。Ruby で書いていますが、中身は単純なので bash などでも書き換えられるのではないかと思います。

## 設定

デフォルトではブランチ名が master または main のときのみ pull を実行するようにしています。develop など別のブランチ名を通常使うルールのときには、`git-allsync` ファイルの頭のほうにある `target_branches` 設定を適宜変更してください。

## インストール

Ruby で書いているので、Ruby 実行環境が必要です。

`git-allsync` ファイルをパスの通ったところにコピーし、実行権限を付けてください。

例
```
$ sudo cp git-allsync /usr/local/bin
$ sudo chmod a+x /usr/local/bin/git-allsync
```

## 実行

複数の独立した Git リポジトリフォルダがある環境で、`git allsync` を実行します。これで、`git pull` が各リポジトリに対して順次施行されます。

- 「設定」でも説明したとおり、master または main ではないブランチ名のときにはスキップされます。
- 単純に `git pull` をしているので、local changes 競合が発生することもあります。そのようなときにはエラー出力されます。

```
$ git allsync
[adventcalendar]...main pulled
[mackerel-agent]...master pulled
[mackerel-agent-plugins]...master pull error
error: Your local changes to the following files would be overwritten by merge:
        packaging/deb/debian/rules
Please commit your changes or stash them before you merge.
Aborting
Updating f6817a6..9b891c4
[mackerel-plugin-f2b]...master pulled
[mkr]...test-modify (skip)
```

## Overview

**git-allsync** is a tool that simply performs `git pull` on each of several Git repository folders located in the current folder. It will help those who have many repositories and forget to pull before working.

There is already a tool of this kind, [myrepos](http://myrepos.branchable.com/), created by Joey Hess. However, I wanted something git-specific and lightweight for me, so I created this.

It is written in Ruby, but the logic is simple enough to be rewritten in bash or other languages.

## Configuration

By default, pull are only performed when the branch name is master or main; if you'd like to use a different branch name (e.g. develop), change the `target_branches` setting in the `git-allsync` file.

## Installation

Of course, you will need Ruby runtime environment.

Copy `git-allsync` file to a location where the PATH is set and give it execute permission.

Example
```
$ sudo cp git-allsync /usr/local/bin
$ sudo chmod a+x /usr/local/bin/git-allsync
```

## Usage

Run `git allsync`. This will cause `git pull` to be performed on each repository.

- As described above, it will skip any branch name that is not `master` or `main`.
- Since this runs `git pull` simply, your local changes conflicts may occur. In such cases, an error will be printed.

```
$ git allsync
[adventcalendar]...main pulled
[mackerel-agent]...master pulled
[mackerel-agent-plugins]...master pull error
error: Your local changes to the following files would be overwritten by merge:
        packaging/deb/debian/rules
Please commit your changes or stash them before you merge.
Aborting
Updating f6817a6..9b891c4
[mackerel-plugin-f2b]...master pulled
[mkr]...test-modify (skip)
```

## ライセンス / License

```
Permission is hereby granted, free of charge, to any person obtaining a
copy of this software and associated documentation files (the "Software"),
to deal in the Software without restriction, including without limitation
the rights to use, copy, modify, merge, publish, distribute, sublicense,
and/or sell copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL
SOFTWARE IN THE PUBLIC INTEREST, INC. BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
DEALINGS IN THE SOFTWARE.
```
