# ChineseWordVectors
搜集、整理、发布 预训练 中文 词向量/字向量，与 有志之士 共同 促进 中文 自然语言处理 的 发展。

## 使用说明
1. 所有 词向量/字向量 均 采用 [bcolz](http://bcolz.blosc.org/en/latest/) 格式存储，如果还未安装 bcolz，请先通过 `pip install bcolz` 或 `conda install bcolz` 安装
2. 下载相应的 词向量/字向量 zip 压缩包（如 zh.64.zip），并解压到相应的目录中（如 zh.64），解压后的目录中（如 zh.64）应包含 2 个子目录 embeddings 和 words，分别存储 嵌入向量 和 词（字）典。
3. 参考下面的 Python 代码（兼容 Python 3 和 2），加载 词向量/字向量

```python
import bcolz

def load_embeddings(folder_path):
    """从 bcolz 加载 词/字 向量

    Args:
        - folder_path (str): 解压后的 bcolz rootdir（如 zh.64），
                             里面包含 2 个子目录 embeddings 和 words，
                             分别存储 嵌入向量 和 词（字）典

    Returns:
        - words (bcolz.carray): 词（字）典列表（bcolz carray  具有和 numpy array 类似的接口）
        - embeddings (bcolz.carray): 嵌入矩阵，每 1 行为 1 个 词向量/字向量，
                                     其行号即为该 词（字） 在 words 中的索引编号
    """
    folder_path = folder_path.rstrip('/')
    words = bcolz.carray(rootdir='%s/words'%folder_path, mode='r')
    embeddings = bcolz.carray(rootdir='%s/embeddings'%folder_path, mode='r')
    return words, embeddings

folder_path = '解压后_词向量_字向量_所在_文件夹_路径'
words, embeddings = load_embeddings(folder_path)
```    
## 下载链接
[百度网盘](https://pan.baidu.com/s/1tN7152tyFXY1oOu0yB5-Cg)

## 类型、维度、词（字）典

| 名称 | 类型 | 维度 | 词汇总数 | 中文 | 英文 | 数字 | 其他 | 语料 |
| ---- | ---- | ---- | -------- | ---- | ---- | ---- | ---- | ---- |
| facebook_cc | 词 | 300 | 200w | 156w | 27w | 13w | 3.3w |  [Common Crawl](http://commoncrawl.org/) <br /> [Wikipedia](https://www.wikipedia.org/) |
| facebook_wiki | 词 | 300 | 33w | 14w | 17w | 0 | 1.6w | [Wikipedia](https://www.wikipedia.org/) |
| sjl_weixin | 词 | 256 | 35w | 25w | 6w | 2w | 0.3w | 800 万微信公众号文章 <br /> 总词数达 650 亿 |
| polyglot_wiki | 词 | 64 | 10w | 6w | 3w | 0 | 0.2w | [Wikipedia](https://www.wikipedia.org/) |
| polyglot_wiki | 字 | 64 | 10w | 1.2w | 7.8w | 0 | 0.9w | [Wikipedia](https://www.wikipedia.org/) |
| novel_baidubaike_news | 词 | 64 | 611w | 611w | 0 | 0 | 0 | 小说 90G 左右 <br /> 百度百科 800w+ 条, 20G+ <br /> 搜狐新闻 400w+ 条, 12G+ |
| sougou_news | 词 | 200 | 未统计 | 未统计 | 0 | 0 | 0 | 搜狗8个行业各1990篇新闻 <br /> 按行业分别训练 <br /> 包括财经、IT、健康、体育、旅游、教育、招聘、文化、军事 |
| sougou_news | 字 | 200 | 未统计 | 未统计 | 0 | 0 | 0 | 搜狗8个行业各1990篇新闻 <br /> 按行业分别训练（同上） |

## 简繁、全/半角、大小写、特殊符号

| 名称 | 简体 | 繁体 | 全角 | 半角 | 大写 | 小写 | 数字 | 特殊符号 |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | -------- |
| facebook_cc | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | 句末 </s\> |
| facebook_wiki | ✔ | ✔ | ✔ | ✔ | ✘ | ✔ | ✘ | 句末 </s\> |
| sjl_weixin | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | 换行 \n |
| polyglot_wiki | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✘ | 未知 <UNK\>, 句首 <S\>, 句末 </S\>, 补全 <PAD\> |
| polyglot_wiki | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✘ | 未知 <UNK\>, 句首 <S\>, 句末 </S\>, 补全 <PAD\> |
| novel_baidubaike_news | ✔ | ✘ | ✘ | ✘ | ✘ | ✘ | ✘ | |
| sougou_news | ✔ | ✘ | ✔ | ✔ | ✘ | ✘ | ✘ | 换行 \n |

## 作者、语料、（分词及训练）工具 以及 训练参数

| 名称 | 作者 | 分词工具 | 训练工具 | 训练参数 |
| ---- | ---- | ---- | ---- | ---- |
| facebook_cc | [Facebook](https://fasttext.cc/docs/en/crawl-vectors.html)| [Stanford word segmenter](https://nlp.stanford.edu/software/segmenter.html) | [fastText](https://fasttext.cc/) | CBOW with position-weights, character n-grams of length 5 <br /> window of size 5 and 10 negatives |
| facebook_wiki | [Facebook](https://fasttext.cc/docs/en/pretrained-vectors.html) | | [fastText](https://fasttext.cc/) | 论文 [Enriching Word Vectors with Subword Information](https://arxiv.org/abs/1607.04606) 中的默认设置 |
| sjl_weixin | [苏剑林](https://kexue.fm/archives/4304) | [Jieba](https://github.com/fxsjy/jieba) | [Gensim](https://radimrehurek.com/gensim/) | Skip-Gram, Huffman Softmax, 窗口大小 10, 最小词频 64, 迭代 10 次 |
| polyglot_wiki | [Polyglot](https://sites.google.com/site/rmyeid/projects/polyglot) | | [word2embeddings](https://bitbucket.org/aboSamoor/word2embeddings) <br /> [polyglot2](http://polyglot2.readthedocs.org/) |
| novel_baidubaike_news | [dada](https://weibo.com/p/23041816d74e01f0102x77v) | [Jieba](https://github.com/fxsjy/jieba)| [Gensim](https://radimrehurek.com/gensim/) |  window=5, min_count=5, 其他为 Word2Vec 默认参数 |
| sougou_news | [dada]http://www.pudn.com/Download/item/id/1036884.html) | [Jieba](https://github.com/fxsjy/jieba)| [Gensim](https://radimrehurek.com/gensim/) |  window=9, min_count=10, skip-gram,negative=8, hs=1, 其他为 Word2Vec 默认参数 |
