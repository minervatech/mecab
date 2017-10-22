# mecab
Yet another Japanese morphological analyzer

# installation
First compile mecab.
```
git clone https://github.com/minervatech/mecab.git
cd mecab/mecab
./configure  --enable-utf8-only
make
make check
sudo make install
```

Mecab will be deployed to
```
/usr/local/etc/mecabrc
/usr/local/bin/mecab
/usr/local/bin/mecab-config
```

Then, compile dictionary. Use minerva/mecab as the original code have encoding problem.
```
cd mecab/mecab-ipadic
./configure --with-charset=utf8
make
sudo make install
sudo ldconfig
```

# Custom dictionary
Add arbitrary CSV file below mecab/mecab-ipadic and re-build dictionary
```
vim mecab/mecab-ipadic/Noun.new.csv
make clean
make
sudo make install
sudo mv /usr/local/lib/mecab/dic/ipadic /usr/local/lib/mecab/dic/ipadic_default
```

# Use mecab-ipadic-neologd
```
cd mecab
git clone https://github.com/neologd/mecab-ipadic-neologd
echo `mecab-config --dicdir`"/mecab-ipadic-neologd" # Check target dir
./mecab-ipadic-neologd/bin/install-mecab-ipadic-neologd -n -a
```

## Comparison
- ipadic
mecab -d /usr/local/lib/mecab/dic/ipadic
10日放送の「中居正広のミになる図書館」（テレビ朝日系）で、SMAPの中居正広が、篠原信一の過去の勘違いを明かす一幕があった。
10      名詞,数,*,*,*,*,*
日      名詞,接尾,助数詞,*,*,*,日,ニチ,ニチ
放送    名詞,サ変接続,*,*,*,*,放送,ホウソウ,ホーソー
の      助詞,連体化,*,*,*,*,の,ノ,ノ
「      記号,括弧開,*,*,*,*,「,「,「
中居    名詞,固有名詞,人名,姓,*,*,中居,ナカイ,ナカイ
正広    名詞,固有名詞,人名,名,*,*,正広,マサヒロ,マサヒロ
の      助詞,連体化,*,*,*,*,の,ノ,ノ
ミ      名詞,一般,*,*,*,*,ミ,ミ,ミ
に      助詞,格助詞,一般,*,*,*,に,ニ,ニ
なる    動詞,自立,*,*,五段・ラ行,基本形,なる,ナル,ナル
図書館  名詞,一般,*,*,*,*,図書館,トショカン,トショカン
」      記号,括弧閉,*,*,*,*,」,」,」
（      記号,括弧開,*,*,*,*,（,（,（
テレビ朝日      名詞,固有名詞,組織,*,*,*,テレビ朝日,テレビアサヒ,テレビアサヒ
系      名詞,接尾,一般,*,*,*,系,ケイ,ケイ
）      記号,括弧閉,*,*,*,*,）,）,）
で      助詞,格助詞,一般,*,*,*,で,デ,デ
、      記号,読点,*,*,*,*,、,、,、
SMAP    名詞,固有名詞,組織,*,*,*,*
の      助詞,連体化,*,*,*,*,の,ノ,ノ
中居    名詞,固有名詞,人名,姓,*,*,中居,ナカイ,ナカイ
正広    名詞,固有名詞,人名,名,*,*,正広,マサヒロ,マサヒロ
が      助詞,格助詞,一般,*,*,*,が,ガ,ガ
、      記号,読点,*,*,*,*,、,、,、
篠原    名詞,固有名詞,人名,姓,*,*,篠原,シノハラ,シノハラ
信一    名詞,固有名詞,人名,名,*,*,信一,シンイチ,シンイチ
の      助詞,連体化,*,*,*,*,の,ノ,ノ
過去    名詞,副詞可能,*,*,*,*,過去,カコ,カコ
の      助詞,連体化,*,*,*,*,の,ノ,ノ
勘違い  名詞,サ変接続,*,*,*,*,勘違い,カンチガイ,カンチガイ
を      助詞,格助詞,一般,*,*,*,を,ヲ,ヲ
明かす  動詞,自立,*,*,五段・サ行,基本形,明かす,アカス,アカス
一幕    名詞,一般,*,*,*,*,一幕,ヒトマク,ヒトマク
が      助詞,格助詞,一般,*,*,*,が,ガ,ガ
あっ    動詞,自立,*,*,五段・ラ行,連用タ接続,ある,アッ,アッ
た      助動詞,*,*,*,特殊・タ,基本形,た,タ,タ
。      記号,句点,*,*,*,*,。,。,。
EOS


- mecab-ipadic-neologd
mecab -d /usr/local/lib/mecab/dic/mecab-ipadic-neologd/
10日    名詞,固有名詞,一般,*,*,*,10日,トオカ,トオカ
放送    名詞,サ変接続,*,*,*,*,放送,ホウソウ,ホーソー
の      助詞,連体化,*,*,*,*,の,ノ,ノ
「      記号,括弧開,*,*,*,*,「,「,「
中居正広のミになる図書館        名詞,固有名詞,一般,*,*,*,中居正広のミになる図書館,ナカイマサヒロノミニナルトショカン,ナカイマサヒロノミニナルトショカン
」      記号,括弧閉,*,*,*,*,」,」,」
（      記号,括弧開,*,*,*,*,（,（,（
テレビ朝日      名詞,固有名詞,組織,*,*,*,テレビ朝日,テレビアサヒ,テレビアサヒ
系      名詞,接尾,一般,*,*,*,系,ケイ,ケイ
）      記号,括弧閉,*,*,*,*,）,）,）
で      助詞,格助詞,一般,*,*,*,で,デ,デ
、      記号,読点,*,*,*,*,、,、,、
SMAP    名詞,固有名詞,一般,*,*,*,SMAP,スマップ,スマップ
の      助詞,連体化,*,*,*,*,の,ノ,ノ
中居正広        名詞,固有名詞,人名,*,*,*,中居正広,ナカイマサヒロ,ナカイマサヒロ
が      助詞,格助詞,一般,*,*,*,が,ガ,ガ
、      記号,読点,*,*,*,*,、,、,、
篠原信一        名詞,固有名詞,人名,*,*,*,篠原信一,シノハラシンイチ,シノハラシンイチ
の      助詞,連体化,*,*,*,*,の,ノ,ノ
過去    名詞,副詞可能,*,*,*,*,過去,カコ,カコ
の      助詞,連体化,*,*,*,*,の,ノ,ノ
勘違い  名詞,サ変接続,*,*,*,*,勘違い,カンチガイ,カンチガイ
を      助詞,格助詞,一般,*,*,*,を,ヲ,ヲ
明かす  動詞,自立,*,*,五段・サ行,基本形,明かす,アカス,アカス
一幕    名詞,一般,*,*,*,*,一幕,ヒトマク,ヒトマク
が      助詞,格助詞,一般,*,*,*,が,ガ,ガ
あっ    動詞,自立,*,*,五段・ラ行,連用タ接続,ある,アッ,アッ
た      助動詞,*,*,*,特殊・タ,基本形,た,タ,タ
。      記号,句点,*,*,*,*,。,。,。
EOS
