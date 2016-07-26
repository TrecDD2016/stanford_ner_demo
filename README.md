# Stanford NER
Stanford NER 的示例代码，在Stanford NER的包里也可以找到。

NER（Named Entity Recognizer）：命名实体分析器，用于把具有实际意义的实体（人名、地名、专有名词等）识别出来。Stanford Named Entity Recognizer是一个斯坦福大学的用Java实现的分析器。通过它可以进行命名实体的标识，也可以自己定义一个特征提取器。Stanford NER对于英语的人名、组织和地名的识别能力非常强。Stanford NER包括命令行启动、服务器和jar包(最新版本SNER需要Java1.8或者更新版本，v3.4.1支持1.6和1.7)形式的实现。Stanford NER对于文本数据和HTML数据都可以进行识别，通过使用预置的分类器，可以对英语中的专有组织、人名和地名做出标记，但是其他的单词都不会被识别。如果想要对自己定义的单词或者词组进行识别，就需要自定义分类器。通过形如

```
Today    0
is       0
Friday   WEEK
.        0
Saturday WEEK
is       0
11/30    DATE
.        0

```
的标记文件和形如

```
#location of the training file
trainFile =testdata.tsv
#location where you would like to save (serialize to) your
#classifier; adding .gz at the end automatically gzips the file,
#making it faster and smaller
serializeTo = ner-model.ser.gz

#structure of your training file; this tells the classifier
#that the word is in column 0 and the correct answer is in
#column 1
map = word=0,answer=1

#these are the features we'd like to train with
#some are discussed below, the rest can be
#understood by looking at NERFeatureFactory
useClassFeature=true
useWord=true
useNGrams=true
#no ngrams will be included that do not contain either the
#beginning or end of the word
noMidNGrams=true
useDisjunctive=true
maxNGramLeng=6
usePrev=true
useNext=true
useSequences=true
usePrevSequences=true
maxLeft=1
#the next 4 deal with word shape features
useTypeSeqs=true
useTypeSeqs2=true
useTypeySequences=true
wordShape=chris2useLC
```

的配置文件可以生成一个分类器

```
java -cp stanford-ner.jar edu.stanford.nlp.ie.crf.CRFClassifier -prop austen.prop
```

最后通过这样的分类器可以得到标记结果

```
I/O like/O Friday/WEEK ,/O I/O also/O like/O Monday/O !/O 
```
要在java工程中使用分类器，只要将依赖的jar包和分类器导入就可以了。具体的示例代码在NERDemo.java中

不同的输出格式：http://nlp.stanford.edu/software/crf-faq.html#j
工具主页：http://nlp.stanford.edu/software/CRF-NER.html 
