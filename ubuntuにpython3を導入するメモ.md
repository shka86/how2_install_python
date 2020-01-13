ubuntuにpython3を導入するメモ
===

もともと入っているpython2系とか、自分で入れたpython3系とかと共存させる方法。
メモ書きです。

```sh
su

apt install -y build-essential libsqlite3-dev sqlite3 bzip2 libbz2-dev zlib1g-dev libssl-dev openssl libgdbm-dev libgdbm-compat-dev liblzma-dev libreadline-dev libncursesw5-dev libffi-dev uuid-dev

cd /tmp
wget https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tar.xz
tar xvf Python-3.8.1.tar.xz

cd Python-3.8.1
./configure --prefix=/usr/local/lib/python-3.8.1
make
make altinstall

cd /usr/bin
ln -fs /usr/local/lib/python-3.8.1/bin/python3.8
ln -fs python3.8 python3

cd /tmp
wget https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py

cd /usr/bin
ln -fs /usr/local/lib/python-3.8.1/bin/pip3.8
ln -sf pip3.8 pip3

pip3 -V
```

- 多分この作業をするのはマシン立ち上げの流れの中だと思うので、
su のパスワードをまだ設定していないと思う。
その時は`sudo passwd root` で設定する。

- ubuntuはzlib1gでも、他ではzlibだったりする。
途中でおかしくなったらmake cleanしてみるとか。

- 多分みんなlsb_releaseがあーでこーで躓くはずで、
その時はvi /usr/bin/lsb_releaseでPythonのversionを
pathが通っているものに置き換える必要がある。

私は#!/usr/bin/python3 -Es→#!/usr/bin/python3.6 -Esとした。
net上にはpython2にするとうまく行くって情報が上がっているが、
コードを見る限りpython3系が正しそう。

この作業の寸前で、多分python3.8.4が使用可能になっているだろうから、
それを指定しても解決するような気もする。がうまくいかなかった。なんで？

- ついでにnumpyを入れてみるのならsudo pip3 install numpy

