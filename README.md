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
