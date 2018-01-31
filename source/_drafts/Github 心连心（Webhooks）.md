---
title: Github 心连心（Webhooks）
date: 2018-01-25 14:35:05
tags:
---

ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
git clone xxxxxxxxxxxxxxxxxxx
sudo chown -R www-data:www-data /workspace/heyforyou/
vim deploy.php
```
<?php
$path = "/workspace/heyforyou/";
$dir = "/workspace/gitlog";

$requestBody = file_get_contents("php://input");

if (empty($requestBody)) {
    die('send fail');
}
$content = json_decode($requestBody, true);

if ($content['ref']=='refs/heads/master') {

    $res = shell_exec("cd {$path} && git checkout -f master &&  git pull 2>&1");

    $res_log = '------------start-------------'.PHP_EOL;
    $res_log .= '上一个版本是: ' . $content['before'].PHP_EOL;
    $res_log .= '下一个版本是: ' . $content['after'].PHP_EOL;
    $res_log .= '提交者: ' .  $content['pusher']['name'].PHP_EOL;
    $res_log .= '提交者邮箱: ' . $content['pusher']['email'].PHP_EOL;
    $res_log .= $res.PHP_EOL;
    $res_log .= '------------end-------------'.PHP_EOL;
    $file_path="$dir".'/'.date("Y").'/'.date("m").'/'.date("d").'/'.date('Ymd_H_i').'_log.txt';
    file_force_contents($file_path, $res_log);
}

function file_force_contents($dir, $contents){
    $parts = explode('/', $dir);
    $file = array_pop($parts);
    $dir = '';
    foreach($parts as $part)
        if(!is_dir($dir .= "/$part")) mkdir($dir);
    file_put_contents("$dir/$file", $contents, FILE_APPEND);
}
把 ~/.ssh/ 下面的所有都复制到 /var/www/.ssh 文件夹下
然后把文件的用户也改成 www-data
```