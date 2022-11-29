---
title: "在MySQL啟用語法執行紀錄【MySQL】"
header:
  teaser: "/assets/images/post/2022-11-29-How-to-enable-query-log-in-MySQL/teaser.jpg"
date: 2022-11-29T00:00:00+08:00
categories:
  - MySQL
tags:
  - MySQL
---
## 前言
最近工作使用到MySQL，加上專案有使用到ORM相關工具，導致執行語法，不能很直觀的追蹤到，這邊會教你如何開啟MySQL的語法執行紀錄。

## 設定
### 確認log的啟用狀態

~~~sql
show variables like 'general%';
~~~

如果`general_log`是`ON`，代表你已經開啟了，只要確認存到哪裡去即可。

### 開啟general_log

~~~sql
SET global log_output = 'table';
-- 寫入至mysql.general_log，預設是寫入file內。
SET global general_log=1;
-- 開啟general_log。
~~~

這邊的話，如果是自己測試用，我個人會把log寫入至Table，這樣在查詢時比較方便，但建議沒在使用的時候記得關閉，會佔用相當大的容量。

### 查詢語法

~~~sql
SELECT
    *
FROM
    mysql.general_log;
~~~

~~~sql
CONVERT(sql_text USING utf8);
-- blob型態的可以用這個語法轉換。
~~~

## 心得
在轉換各種環境時，常常需要Ready各式的測試方式，但其實大同小異，如果接下來有時間的話，我在整理slow_query在production環境上的設定，供大家參考。