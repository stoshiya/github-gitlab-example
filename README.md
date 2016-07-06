# github-gitlab-example

GitHubとGitLabを連携するための手順

1. GitHub/GitLabにベアリポジトリを作成．

2. GitLabが稼働しているホストのgitアカウントからGitHubへSSH接続するための鍵ペアを生成し，GitHubのリポジトリのdeploy keyに公開鍵を設定する．

        % sudo su git
        % cd ~
        % ssh-keygen -C git@gitlab

3. GitLabのリポジトリへ移動し，GitHubのリポジトリをリモートリポジトリとして設定する．

        % sudo su git
        % cd ~/git-data/repositories/stoshiya/github-gitlab-example.git
        % git remote add --mirror github git@github.com:stoshiya/github-gitlab-example.git

4. GitLabのリポジトリにサーバフックを設定する．

        % sudo su git
        % cd ~/git-data/repositories/stoshiya/github-gitlab-example.git
        % mv hooks hooks.orig
        % mkdir hooks
        % echo "exec git push --quiet github &" > hooks/post-receive
        % echo "exec git fetch --quite github 'refs/heads/*:refs/heads/*'" > hooks/pre-receive
        % chmod 755 hooks/post-recieve hooks/pre-recieve
