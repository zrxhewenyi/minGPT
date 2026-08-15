配置AutoDL加速

```Linux
source /etc/network_turbo
```

安装uv

```Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

```Linux
uv --version
```

把代码放在数据盘下面

```Linux
cd /root/autodl-tmp
```

下载仓库进入仓库

```Linux
git clone git@github.com:zrxhewenyi/minGPT.git
```

```Linux
cd minGPT
```

同步环境

```uv
uv sync
```

进入大容量数据盘

```Linux
cd /root/autodl-tmp

mkdir -p data && cd data
```

关闭临时代理

```Linux
unset http_proxy https_proxy
```

下载数据

```Linux
pip install modelscope

modelscope download --dataset ddzhu123/seq-monkey --local_dir ./
```

解压数据

```Linux
tar -xvf mobvoi_seq_monkey_general_open_corpus.jsonl.tar.bz2
```

提取前50000步

```Linux
head -n 50000 mobvoi_seq_monkey_general_open_corpus.jsonl > /root/autodl-tmp/data/mini_50k.jsonl
```

删除缓存

```Linux
rm mobvoi_seq_monkey_general_open_corpus.jsonl.tar.bz2
```

直接运行

```python
python train.py
```

后台运行

```python
nohup python train.py > train.log 2>&1 &
```

查看实时训练进度

```Linux
tail -f train.log
```