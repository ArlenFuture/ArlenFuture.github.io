---
title: "解決SourceTree無法登入雙因素驗證(2FA)的Github帳號【SourceTree】"
header:
  teaser: "/assets/images/post/2022-11-06-Login-2FA-GitHub-Accounts-with-SourceTree/teaser.jpg"
date: 2022-11-06T00:00:00+08:00
categories:
  - SourceTree
tags:
  - SourceTree
  - GitHub
  - MacOS
---
## 前言
前陣子工作上從.NET大桶餐的環境跳槽到MacOS為主的開發環境，第一個遇到的問題，就是版本控制，雖然自身也有使用MacOS相關產品，但因為通常是OpenSource的關係，可以使用GitKraken去無痛銜接，但在工作環境下，公司不一定備有習慣的版本控制工具的License，今天就是來分享允許在商業環境下使用的免費版控工具SourceTree遇到的問題。

## 問題敘述
我在MacOS上使用SourceTree時，發現無法使用原本預設OAuth登入GitHub，當時對這個錯誤提示有錯誤的理解，我當時因為過去是使用Azure DevOps的平台，過去我是使用SSH解決問題，這個方法暫時可行，但會出現每次重開機SSH Key就會失效的問題，導致需要常常重設，後來專案比較有閒暇時間，重新回頭理解問題，發現是因為2FA設定導致，原本的方式無法登入。

## 解決方法
- 相關設定可以參考底下官方文章。
- 2023年GitHub將全面啟用雙因素驗證。
這篇因為官方寫得很詳細，我就不另外做操作上的敘述，如果有操作上問題也歡迎在底下留言。

## 參考
- [Two-Factor Authentication (2FA) with GitHub in SourceTree](https://confluence.atlassian.com/sourcetreekb/two-factor-authentication-2fa-with-github-in-sourcetree-402033499.html)
- [GitHub將全面啟用雙因素驗證，所有提交程式碼的使用者須在2023年底前啟用2FA](https://www.ithome.com.tw/tech/150854)