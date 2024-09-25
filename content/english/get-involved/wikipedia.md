---
title: "Mirroring Wikipedia"
date: 2024-09-07T09:59:33+10:00
---

The simplest way to mirror Wikipedia is using the [Kiwix tools](https://kiwix.org/) and a [Zim](https://en.wikipedia.org/wiki/ZIM_(file_format)) format snapshot.

#### Getting a snapshot

Downloading one of these snapshots is fairly simple - the Kiwix site [maintains pages with links](https://download.kiwix.org/zim/wikipedia/) to "zim" files for various facets of Wikipedia. They're broken down by language ("en", in the filename), topic-specific (eg [Chemistry](https://download.kiwix.org/zim/wikipedia/wikipedia_en_chemistry_mini_2024-06.zim)) and other variations (options like "mini", "maxi", "nopic" allow us to further control how much data we're willing download.)

So to download that Chemistry snapshot, we could use a command like this:

```
curl -L https://download.kiwix.org/zim/wikipedia/wikipedia_en_chemistry_mini_2024-06.zim -o wikipedia_en_chemistry_mini_2024-06.zim
```

(The '-L' flag tells Curl to follow redirects (which the Kiwix links are) and the '-o' allows us to specify the filename for the downloaded file.)

#### Serving the snapshot

On a Debian-based system (like Ubuntu or RaspberryPi OS) you can install the Kiwix Tools (including their server) like this:

```
sudo apt-get install kiwix-tools
```

...and then run the serving app with our snapshot like this:

```
kiwix-serve -p 8080 wikipedia_en_chemistry_mini_2024-06.zim
```

...which will print out a URL (something like ''http://192.168.1.223:8080/'') where we can view our site.

(The '-p' flag allows us to specify the port we'll find our site on - if we omit this option ''kiwix-serve'' will try to run on the normal HTTP port (80) which will fail, unless we also run the command as root, by prepending ''sudo'' to it.)
