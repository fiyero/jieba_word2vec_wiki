# Apply Jieba on build word2vec model in Chinese content :smile:
https://medium.com/@patrickhk/practice-ntlk-word2vec-pca-wordcloud-jieba-on-harry-potter-series-and-chinese-content-ca6f845b3293

I will briefly demonstrate how to Jieba on build word2vec model in Chinese content<br/>

## Data:
From wikipedia we can obtain its backup in different time steps with different languages. I use the Chinese backup at 1st Jan 2019 as the raw data. We can make use of the gensim.corpora.WikiCorpus function to read and extract the corpus easily.<br/>
![p1](https://cdn-images-1.medium.com/max/800/1*pmnrsiXH31_KQx5XHXcHpA.png)<br/>
As you can see, even the Chinese backup contained English. Initially I think of filtering away the English to avoid being potential noise to the word2vec model, but I find the result is fine therefore at the end I didn’t filter the English.<br/>

## Convert into traditional Chinese:
I am HongKonger and we use traditional Chinese not simplified Chinese, I have to convert the content into traditional Chinese. We can apply whatever way to convert from simplified Chinese to traditional Chinese. Since the corpus is large (~1.2GB), I suggest you use python package such as opencc to do the conversion. Also load the big5 dictionary from jieba github for better cutting. Actually there is a Cantonese version of wikipedia backup to be downloaded, I am not sure it use proper written language or spoken language therefore I choose the normal Chinese version.<br/>
![p2](https://cdn-images-1.medium.com/max/800/1*r7gJTpUR3-L8WsqAiqyhdA.png)

## Apply stopwords and tokenization:
This part is similar to the word2vec example in Harry Potter, but this time we use Jieba to apply stopwords and tokenization instead of NLTK/gensim<br/>
![p3](https://cdn-images-1.medium.com/max/800/1*c7qJjKcyxJQoFvB4nQuhEw.png)

## Put into gensim word2vec model:
Same as the English version

## Cosine similarity:
Let’s test the word “China", words such as Chinese gov, TV station, Shanghai are returned, it makes sense.<br/>
![p4](https://cdn-images-1.medium.com/max/800/1*-LAlD07BkmQiF-RRUpKiHw.png)<br/>
Let’s make some fun to test “China,Hong Kong and Taiwan“<br/>
![p5](https://cdn-images-1.medium.com/max/800/1*C-IDaD5F_0dBenET7_Jasw.png)<br/>

According to this word2vec model by using 2019 wiki backup, Hong Kong is more related to China than Taiwan, which is true.<br/>

When I apply the word “Deep learning” or “Machine Learning”, it shows error as no such word in the vocabulary.<br/>
![p6](https://cdn-images-1.medium.com/max/800/1*ZpbzBWM5Dnd3jSUWZ6glvA.png)<br/>
If I apply “Artificial Intelligence” I can get the following result, I see a weird term called “機器人學", I guess this “maybe” our machine learning. I don’t believe Chinese Wikipedia doesn’t contain much information for Deep learning/Machine learning.<br/>
![p7](https://cdn-images-1.medium.com/max/800/1*igFfPqR9SLW5OUrVOr5WSw.png)

## Why have this error?
(Most likely) Possibly during tokenization, the term “深度學習" is cut into different words. Can solve this by adding userdict with jieba.load_userdict(txt_file)<br/>
May have encoding error during conversion from simplified Chinese to traditional Chinese (less likely)

-------------------------------------------------------------------------------------------------------------------------------------
### More about me
[[:pencil:My Medium]](https://medium.com/@patrickhk)<br/>
[[:house_with_garden:My Website]](https://www.fiyeroleung.com/)<br/>
[[:space_invader:	My Github]](https://github.com/fiyero)<br/>
