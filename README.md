# getjump

[![PyPI version](
  https://badge.fury.io/py/getjump.svg
  )](
  https://badge.fury.io/py/getjump
) [![Maintainability](
  https://api.codeclimate.com/v1/badges/8d8c16d52b49885dad8c/maintainability
  )](
  https://codeclimate.com/github/eggplants/getjump/maintainability
) [![pre-commit.ci status](
  https://results.pre-commit.ci/badge/github/eggplants/getjump/master.svg
  )](
  https://results.pre-commit.ci/latest/github/eggplants/getjump/master
)

- Retrieve and save images from manga distribution sites using [GigaViewer](https://prtimes.jp/main/html/searchrlp/company_id/6510)
   - If you read retrieved comics as conbined PDF, use: [eggplants/mkbook](https://github.com/eggplants/mkbook)

_Note: Redistribution of downloaded image data is prohibited. Please keep it to private use._

## Valid URL Formats

- `<host>/{episode,magazine,volume}/<number>`
  - e.g. <https://shonenjumpplus.com/episode/13932016480028799982>
- `<host>/(episode|magazine|volume)/<number>.json`
  - e.g. <https://shonenjumpplus.com/episode/13932016480028799982.json>

## Available Hosts

- `https://www.corocoro.jp`
- `https://comic-action.com`
- `https://comic-days.com`
- `https://comic-gardo.com`
- `https://comic-trail.com`
- `https://comic-zenon.com`
- `https://comicborder.com`
- `https://comicbushi-web.com`
- `https://feelweb.jp`
- `https://kuragebunch.com`
- `https://magcomi.com`
- `https://pocket.shonenmagazine.com`
- `https://shonenjumpplus.com`
- `https://tonarinoyj.jp`
- `https://viewer.heros-web.com`
- `https://www.sunday-webry.com`

## Install

```bash
pip install getjump
```

## Library

To download all series at once:

```python
from getjump import GetJump as g

G = g()
next_uri = "https://shonenjumpplus.com/episode/13932016480028799982.json"
while next_uri:
    next_uri, prev_title, saved = G.get(next_uri, overwrite=False)
    # next_uri, prev_title, saved = G.get(..., username="***", password="***")
    if saved:
        print("saved:", prev_title)
    print("next:", next_uri)
```

### Login

To get purchaced or login required works:

```python
from getjump import GetJump as g

G = g()
G.login("https://shonenjumpplus.com", username="***", password="***")
G.login("https://comic-days.com", username="***", password="***")
...
G.get(...)
```

## CLI

### Usage

```shellsession
$ jget https://shonenjumpplus.com/episode/13932016480028799982.json
get: https://shonenjumpplus.com/episode/13932016480028799982.json
saved: ./阿波連さんははかれない/[1話]阿波連さんははかれない
done.

$ jget -b https://shonenjumpplus.com/episode/10833519556325021912.json
get: https://shonenjumpplus.com/episode/10833519556325021912.json
saved: ./こちら葛飾区亀有公園前派出所/[第1話]こちら葛飾区亀有公園前派出所
next: https://shonenjumpplus.com/episode/10833519556325022016.json
saved: ./こちら葛飾区亀有公園前派出所/[第2話]こちら葛飾区亀有公園前派出所
next: https://shonenjumpplus.com/episode/10833519556325022128.json
saved: ./こちら葛飾区亀有公園前派出所/[第3話]こちら葛飾区亀有公園前派出所
next: https://shonenjumpplus.com/episode/10833519556325022500.json
...
saved: ./こちら葛飾区亀有公園前派出所/[第1950話]こちら葛飾区亀有公園前派出所
next: https://shonenjumpplus.com/episode/13932016480028744844.json
saved: ./こちら葛飾区亀有公園前派出所/[第1951話]こちら葛飾区亀有公園前派出所
next: https://shonenjumpplus.com/episode/13932016480028744845.json
saved: ./こちら葛飾区亀有公園前派出所/[第1952話]こちら葛飾区亀有公園前派出所
next: https://shonenjumpplus.com/episode/13932016480028744846.json
saved: ./こちら葛飾区亀有公園前派出所/[第1953話]こちら葛飾区亀有公園前派出所
done.
```

### Help

```shellsession
$ jget -h
usage: jget [-h] [-b] [-d DIR] [-f] [-o] [-u USERNAME] [-p PASSWORD] url

Get images from jump web viewer

positional arguments:
  url                    target url

optional arguments:
  -h, --help             show this help message and exit
  -b, --bulk             download series in bulk (default: False)
  -d DIR, --savedir DIR  directory to save downloaded images (default: .)
  -f, --first            download only first page (default: False)
  -o, --overwrite        overwrite (default: False)
  -u USERNAME, --username USERNAME
                         username if you want to login (default: None)
  -p PASSWORD, --password PASSWORD
                         password if you want to login (default: None)

available urls:
  - https://www.corocoro.jp
  - https://comic-action.com
  - https://comic-days.com
  - https://comic-gardo.com
  - https://comic-trail.com
  - https://comic-zenon.com
  - https://comicborder.com
  - https://comicbushi-web.com
  - https://feelweb.jp/episode
  - https://kuragebunch.com
  - https://magcomi.com
  - https://pocket.shonenmagazine.com
  - https://shonenjumpplus.com
  - https://www.sunday-webry.com
  - https://tonarinoyj.jp
  - https://viewer.heros-web.com
```

## Screenshot

![image](https://user-images.githubusercontent.com/42153744/149342180-1131ac3f-2d9b-4938-bf5c-c1b8fb52072b.png)

## License

MIT

---

## Reference

- [fa0311/jump-downloader](https://github.com/fa0311/jump-downloader)
- [少年ジャンププラスの漫画をダウンロードするライブラリ - yuki0311.com](https://blog.yuki0311.com/jumppuls_downloader/)
- [はてな開発の新マンガビューワを「少年ジャンプ＋」が採用。集英社と共同でサイト成長、マネタイズの両面を加速 - プレスリリース - 株式会社はてな](https://hatenacorp.jp/press/release/entry/2017/01/18/113000)
- [はてな、集英社「少年ジャンプ＋」ブラウザ版への機能提供を拡張。ブラウザ版への電子版「週刊少年ジャンプ」定期購読が可能に｜株式会社はてなのプレスリリース](https://prtimes.jp/main/html/rd/p/000000078.000006510.html)
- [GigaViewer の検索結果 - プレスリリース - 株式会社はてな](https://hatenacorp.jp/press/release/search?q=GigaViewer)
- [GigaViewer（ギガビューワー）を作るにあたって - daily thinking running](https://jusei.hatenablog.com/entry/2018/01/09/172026)
