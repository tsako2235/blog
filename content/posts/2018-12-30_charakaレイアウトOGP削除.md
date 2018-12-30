---
title: "2018 12 30_charakaレイアウトOGP削除"
date: 2018-12-30T16:13:43+09:00
draft: false
---

abountの画面にて、個人的に不要と思われるOGP（Open Graph Protcol）がある、  
右上のツイッター、GitHubとTwitterだけで十分だろうと思い、削除に踏み切る

    tsako2235@DESKTOP-LV0F0HG MINGW64 /c/project/blog/themes/charaka/layouts (blog_marktime)
    $ ls -ltr;pwd
    total 3
    -rw-r--r-- 1 tsako2235 197121  566 Dec 22 15:55 404.html
    drwxr-xr-x 1 tsako2235 197121    0 Dec 22 15:55 _default
    -rw-r--r-- 1 tsako2235 197121 1305 Dec 22 15:55 index.html
    drwxr-xr-x 1 tsako2235 197121    0 Dec 22 15:55 partials
    drwxr-xr-x 1 tsako2235 197121    0 Dec 22 15:55 section
    /c/project/blog/themes/charaka/layouts

まずはレイアウトの確認、部品はpartialsにある筈なので、中身をのぞいてみる

    tsako2235@DESKTOP-LV0F0HG MINGW64 /c/project/blog/themes/charaka/layouts/partials (blog_marktime)
    $ find . | xargs grep twitter
    grep: .: Is a directory
    ./jsshare.html:            shares: ["email", "twitter", "facebook", "googleplus", "linkedin", "pinterest", "stumbleupon", "whatsapp"]

あった、このjsshare.htmlだな、ふむふむ
.Site.Params.shareがenabledのときに設置されるのか…


    tsako2235@DESKTOP-LV0F0HG MINGW64 /c/project/blog/themes/charaka/layouts/partials (blog_marktime)
    $ cat jsshare.html
    <div class="container has-text-centered">
        {{ if .Site.Params.share.enabled }}
        <aside><div id="share"></div></aside>
        <script type="text/javascript">
            $("#share").jsSocials({
                showLabel: false,
                showCount: false,
                shares: ["email", "twitter", "facebook", "googleplus", "linkedin", "pinterest", "stumbleupon", "whatsapp"]
            });
        </script>
        {{ end }}
    </div>

多分、configに、あったと…あった

    tsako2235@DESKTOP-LV0F0HG MINGW64 /c/project/blog (blog_marktime)
    $ cat ./config.toml | grep share -2
    style = "zenburn"

    [params.share]
    enabled = "true"

よし、変更

    tsako2235@DESKTOP-LV0F0HG MINGW64 /c/project/blog (blog_marktime)
    $ cat ./config.toml | grep share -2
    style = "zenburn"

    [params.share]
    enabled = "false"


