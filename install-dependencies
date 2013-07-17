#!/usr/bin/env php
<?php
define('CACHEDIR', getenv('DEPCACHEDIR') ?: "{$_SERVER['HOME']}/.install-dependencies/");
define('DEPFILE', 'dependencies.json');

install_dependencies();


function install_dependencies($basedir = '')
{
  foreach (read_dependeciesfile($basedir . DEPFILE) as $dest => $url) {
    install_dependency($url, "$basedir$dest");
  }
}


function read_dependeciesfile($filename)
{
  return file_exists($filename) ? json_decode(file_get_contents($filename)) : array();
}


function install_dependency($url, $dest)
{
  $releasedir = skip_initial_directory(cache_release($url));
  $subpath = parse_url($url, PHP_URL_FRAGMENT);
  install_link("$releasedir/$subpath", $dest);
}


function cache_release($url)
{
  $cachedir = CACHEDIR . hash_url($url);
  if (!file_exists($cachedir)) {
    unlink(unzip(download($url), $cachedir));
    install_dependencies("$cachedir/");
  }
  return $cachedir;
}


function skip_initial_directory($directory)
{
  $files = glob("$directory/*");
  return (1 === count($files) && is_dir($files[0])) ? $files[0] : $directory;
}


function install_link($target, $dest)
{
  if (is_link($dest))
    unlink($dest);
  if (!file_exists(dirname($dest)))
    mkdir(dirname($dest), 0755, true);
  symlink($target, $dest);
}


function hash_url($url)
{
  return sha1(preg_replace('/#.+$/', '', $url));
}


function download($url)
{
  $ch = curl_init($url);
  $filename = tempnam(sys_get_temp_dir(), 'dep');
  $fp = fopen($filename, 'w');
  curl_setopt($ch, CURLOPT_FILE, $fp);
  curl_setopt($ch, CURLOPT_FOLLOWLOCATION, true);
  curl_exec($ch);
  curl_close($ch);
  fclose($fp);
  return $filename;
}


function unzip($filename, $destination)
{
  mkdir($destination, 0755, true);
  $zip = new ZipArchive();
  $zip->open($filename);
  $zip->extractTo($destination);
  $zip->close();
  return $filename;
}

