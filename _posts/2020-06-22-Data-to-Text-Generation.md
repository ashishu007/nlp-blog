---
toc: true
layout: post
description: Introduction to Data-to-Text Generation.
categories: [nlp, d2t, nlg]
title: Introduction to Data-to-Text Generation
---

# Introduction to Data-to-Text Generation

After wandering in the vast NLP research field for some time, I finally decided to work towards **data-to-text generation** in my PhD. In this blog, I'll try to provide: a brief overview of the task's requirements; some standard public datasets available; and the evaluation metrics used for measuring the performance on these datasets.

<!-- **Table of Contents**

- [Natural Language Generation](#natural-language-generation)
  * [T2T NLG](#t2t-nlg)
  * [D2T NLG](#d2t-nlg)
- [Subtasks in D2T NLG](#subtasks-in-d2t-nlg)
- [Public Datasets and Evaluation Metrics](#public-datasets-and-evaluation-metrics)
  * [RotoWire](#rotowire)
  * [WebNLG](#webnlg)
  * [Meaning Representations](#meaning-representations)
- [Further Steps](#further-steps)
- [References](#references)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small> -->

## Natural Language Generation

First, I'll start with a small introduction on Natural Language Generation (NLG). In NLG, the requirement is to generate a textual document (in some natural language) for the given input (in some format).

There are several real-world applications to automated text generation. Here are some examples. 

<!-- <table>
    <tr>
        <td><img src="/assets/d2t/med.jpg" style="border:1px solid black;" width="500"></td>
        <td>Let's take the <b>Medical Reporting</b> domain - suppose there's a doctor who has to analyse the data from some patients different medical test results. The doctor will have to analyse each test's result in order to make a decision on the patient's condition. A summary of these test results in a textual format highlighting the main parts can be very benificial to the doctor and will reduce a lot of their time and effort required.</td>
    </tr>
</table> -->

  <!-- <img style="vertical-align:middle" src="https://placehold.it/60x60"> -->
  <!-- <img src="/assets/d2t/med.jpg" style="border:1px solid black;vertical-align:middle"> -->

<!-- <div class="box">
  <img src="/assets/d2t/med.jpg" style="border:1px solid black" width="300">
  <span style=""><p style="text-align:right;">Take the <b>Medical Reporting</b> domain for instance - suppose there's a doctor who has to analyse the data from some patients different medical test results. The doctor will have to analyse each test's result in order to make a decision on the patient's condition. A summary of these test results in a textual format highlighting the main parts can be very benificial to the doctor and will reduce a lot of their time and effort required.</p></span>
</div>

<div class="box">
  <span style=""> Take another example of <b>Weather Forecasting</b> - a textual report about the weather conditions summarising the huge numerical data can be very benificial for a meteorologist. Even for the general public, those reports can be very helpful in providing the weather information breifly.</span>
  <img src="/assets/d2t/weather.gif" style="border:1px solid black" width="350">
</div>
 -->

<!-- | ![Medical Domain](/assets/d2t/med.jpg) | Take the **Medical Reporting** domain for instance - suppose there's a doctor who has to analyse the data from some patients different medical test results. The doctor will have to analyse each test's result in order to make a decision on the patient's condition. A summary of these test results in a textual format highlighting the main parts can be very benificial to the doctor and will reduce a lot of their time and effort required. |
| :-----: | :-----:|
| Take another example of **Weather Forecasting** - a textual report about the weather conditions summarising the huge numerical data can be very benificial for a meteorologist. Even for the general public, those reports can be very helpful in providing the weather information breifly. | ![Weather Forecasting](/assets/d2t/weather.gif) | -->

<!-- <img src="/assets/d2t/med.jpg" align="left" style="margin: 0px 10px 0px 0px;"/><p>Take the <b>Medical Reporting</b> domain for instance - suppose there's a doctor who has to analyse the data from some patients different medical test results. The doctor will have to analyse each test's result in order to make a decision on the patient's condition. A summary of these test results in a textual format highlighting the main parts can be very benificial to the doctor and will reduce a lot of their time and effort required.</p>

<img src="/assets/d2t/weather.gif" align="right"/><p>Take another example of <b>Weather Forecasting</b> - a textual report about the weather conditions summarising the huge numerical data can be very benificial for a meteorologist. Even for the general public, those reports can be very helpful in providing the weather information breifly.</p> -->

<!-- <img style="vertical-align:middle" src="https://placehold.it/60x60"> -->
<!-- <img src="/assets/d2t/med.jpg" style="border:1px solid black;vertical-align:middle"> -->

<!-- <p><img src="/assets/d2t/med.jpg" style="border:1px solid black;" width="500">Let's take the <b>Medical Reporting</b> domain - suppose there's a doctor who has to analyse the data from some patients different medical test results. The doctor will have to analyse each test's result in order to make a decision on the patient's condition. A summary of these test results in a textual format highlighting the main parts can be very benificial to the doctor and will reduce a lot of their time and effort required.</p> -->

<table style="margin-left:auto;margin-right:auto;">
  <tr>
    <td><img src="https://ashishu007.github.io/assets/d2t/med.jpg" width="300"></td>
    <td><img src="https://ashishu007.github.io/assets/d2t/weather.gif" width="350"></td>
  </tr>
</table>

<!-- | ![Medical Domain](/assets/d2t/med.jpg) | ![Weather Forecasting](/assets/d2t/weather.gif) |
| :-----: | :-----:| -->

> Take the <b>Medical Reporting</b> domain for instance - suppose there's a doctor who has to analyse the data from some patients different medical test results. The doctor will have to analyse each test's result in order to make a decision on the patient's condition. A summary of these test results in a textual format highlighting the main parts can be very benificial to the doctor and will reduce a lot of their time and effort required.

> Take another example of <b>Weather Forecasting</b> - a textual report about the weather conditions summarising the huge numerical data can be very benificial for a meteorologist. Even for the general public, those reports can be very helpful in providing the weather information breifly.

Based on the input provided to the system, NLG can be broadly categorised into two different categories: first, **text-to-text generation (T2T NLG)**; and second, **data-to-text generation (D2T NLG)**. 

### T2T NLG
As the name suggests, in **text-to-text generation**, our goal is to generate text from unstructured textual input. For example, machine translation, where we take a text document in one natural language as input and produce the same content in different natural language as output.

![T2T NLG](https://ashishu007.github.io/assets/d2t/t2tnlg.jpg){:width="850px" style="display:block;margin-left:auto;margin-right:auto;"}
<!-- <kbd> -->
<!-- <img src="/assets/d2t/t2tnlg.jpg" style="border:1px solid black;margin-left:auto;margin-right:auto;" width="850"> -->
<!-- </kbd> -->
<p style="text-align: center;"><b>Text-to-Text Natural Language Generation (T2T NLG)</b></p>

### D2T NLG
For **data-to-text generation**, the input is presented in a structured format, i.e., tablular, graphical or JSON format. With this structured input, we generate a textual output summarising the input values. For example, summarising NBA match where, for given box- and line-scores as input we have to generate a textual summary of the match as the output.

![D2T NLG](https://ashishu007.github.io/assets/d2t/d2tnlg.jpg){:width="850px" style="display:block;margin-left:auto;margin-right:auto;"}
<!-- <kbd> -->
<!-- <img src="/assets/d2t/d2tnlg.jpg" style="border:1px solid black;margin-left:auto;margin-right:auto;" width="850"> -->
<!-- </kbd> -->
<p style="text-align: center;"><b>Data-to-Text Natural Language Generation (D2T NLG)</b></p>

<!-- As I'm exploring D2T NLG in my PhD, I'll briefly discuss this task in detail in further sections. -->

In general, automated text generation is challenging because **grammar rules** are **very complex**, and also, there can be **several meaning** to **same words** in different context. 

Even after we develop an automated system for text generation, it is challenging to automatically evaluate the texts generated from that system. Unlike most supervised problems, there's **no class knowledge** in form of labels to evaluate the performance. Here the system's goal is to generate **accurate**, **fluent**; and **diverse** texts, not just predicting some label like in most of the other NLP tasks.

<!-- Apart from all this, the real-world applications (such as the automated obituary generator) suffer from data related problems as well. For starter, you might **not** have **any labelled data** to start building your system. There might be requirement of **a domain expert** to manually label some data, and that may be very expensive. After some-time you might collect some labelled data as a part of your deployment process, that data should be used to refine your system.  -->

<!-- No data -->

## Subtasks in D2T NLG

Data-to-Text generation is a long process. It invovles a lot of things - selecting important insights from the data to finally generating the textual document summarising that data. In general, the whole pipeline of D2T can be broadly categorised into these different subtasks:
<!-- <sup>[[1]](#myfootnote1)</sup> shown here: -->

<!-- Let's talk about the subtasks involved in D2T NLG, which can be divided into six different subtasks : -->

- ***Content Determination***: deciding which information from the input will be included in the final text;

- ***Text Structuring***: select the ordering of the selected information in the final text output;

- ***Sentence Aggregation***: selecting which information to be presented in a separate sentence and which two (or more) information can be presented in the same sentence;

- ***Lexicalisation***: finding the correct words and phrases to express the information in a sentence;

- ***Referring Expression Generation***: selecting domain-specific words and phrases; and

- ***Realisation***: Combining all the words and phrases into well-formed sentences.

<!-- ![D2T NLG](/assets/d2t/tasks.jpg){:width="850px" style="display:block;margin-left:auto;margin-right:auto;"} -->
<!-- <kbd> -->

Let's discuss these subtasks with an example. The figure below illustrates a simplified example from the **neonatal intensive care domain**.

<!-- <img src="/assets/d2t/tasks.jpg" style="border:1px solid black;vertical-align:middle;margin:0px 85px" width="850">
<p style="text-align: center;"><b>Subtasks in D2T NLG <a href="https://www.jair.org/index.php/jair/article/download/11173/26378/">(source)</a></b></p>

The tasks that needs to be performed in order to generate the full textual summary from the input data can be described as follows:

> First the system has to decide what the important events are in the data (a, **content determination**), in this case, occurrences of low heart rate (bradycardias). 

> Then it has to decide in which order it wants to present data to the reader (b, **text structuring**) and how to express these in individual sentence plans (c, **aggregation**; **lexicalisation**; **reference**). 

> Finally, the resulting sentences are generated (d, **linguistic realisation**). -->


  <!-- <img style="vertical-align:middle" src="https://placehold.it/60x60"> -->
 
<!-- <div class="box">
  <span style="">
    The tasks that needs to be performed in order to generate the full textual summary from the input data can be described as follows:
    <blockedquote>
      <p>First the system has to decide what the important events are in the data (a, <b>content determination</b>), in this case, occurrences of low heart rate (bradycardias).</p>
    </blockedquote>
    <blockedquote>
      <p>Then it has to decide in which order it wants to present data to the reader (b, <b>text structuring</b>) and how to express these in individual sentence plans (c, <b>aggregation</b>; <b>lexicalisation</b>; <b>reference</b>).</p>
    </blockedquote>
    <blockedquote>
      <p>Finally, the resulting sentences are generated (d, <b>linguistic realisation</b>).</p>
    </blockedquote>
  </span>
  <img src="/assets/d2t/med.jpg" style="border:1px solid black;vertical-align:middle">
</div> -->

<!-- <div class="row">
  <div class="column">
    <img src="/assets/d2t/tasks.jpg" style="border:1px solid black;vertical-align:middle;margin:0px 85px" width="100%">
  </div>
  <div class="column">
    The tasks that needs to be performed in order to generate the full textual summary from the input data can be described as follows:
    <blockedquote>
      <p>First the system has to decide what the important events are in the data (a, <b>content determination</b>), in this case, occurrences of low heart rate (bradycardias).</p>
    </blockedquote>
    <blockedquote>
      <p>Then it has to decide in which order it wants to present data to the reader (b, <b>text structuring</b>) and how to express these in individual sentence plans (c, <b>aggregation</b>; <b>lexicalisation</b>; <b>reference</b>).</p>
    </blockedquote>
    <blockedquote>
      <p>Finally, the resulting sentences are generated (d, <b>linguistic realisation</b>).</p>
    </blockedquote>
  </div>
</div> -->

<!-- | ![subtasks](/assets/d2t/tasks.jpg){:width="750px" style="display:block;margin-left:auto;margin-right:auto;"} |  -->

| ![subtasks](https://ashishu007.github.io/assets/d2t/tasks.jpg){:width="850px" style="display:block;margin-left:auto;margin-right:auto;"} |
|:--:| 
| The tasks that needs to be performed in order to generate the full textual summary from the input data can be described as follows: first the system has to decide what the important events are in the data (a, **content determination**), in this case, occurrences of low heart rate (bradycardias); then it has to decide in which order it wants to present data to the reader (b, **text structuring**) and how to express these in individual sentence plans (c, **aggregation**; **lexicalisation**; **reference**); finally, the resulting sentences are generated (d, **linguistic realisation**). |

<p style="text-align: center;"><b>Subtasks in D2T NLG <a href="https://www.jair.org/index.php/jair/article/download/11173/26378/">(source)</a></b></p>

The specification of these subtasks vary from domain to domain, but the basic idea remains the same. 

Let's take another example, the **NBA match summarisation** (the D2T NLG figure shown above) for instance. Here also, the generation will happen in the following steps:

- first, we need to decide what records from the input table will be dispalyed in the final text (or ***what to say?***); 
- second, we'll have to decide in what order those records will be displayed, which will also include the deciding on which records will have separate senetences and which ones will be included in the same sentence (or ***how to say?***); and 
- finally, generating the text by combining all the decisions made in previous steps (or **saying what's decided**).

## Public Datasets and Evaluation Metrics

Now that we know about the expectations in D2T NLG, let's see some of the standard datasets available in public domain and evaluation metrics used to measure the performance of different methods on these datasets. 

To keep track of the **state-of-the-art** in this field, I would recommend to follow this article on [NLP-progress](https://nlpprogress.com/english/data_to_text_generation.html) or this task category on [Papers with Code](https://paperswithcode.com/task/data-to-text-generation).

### RotoWire
The [dataset](https://github.com/harvardnlp/boxscore-data/blob/master/rotowire.tar.bz2) consists of articles summarizing NBA basketball games, paired with their corresponding box- and line-score tables. It is professionally written, medium length game summaries targeted at fantasy basketball fans. The writing is colloquial, but structured, and targets an audience primarily interested in game statistics. The picture used above for the example of D2T NLG is from this dataset only.
<!-- <sup>[[2]](#myfootnote2)</sup>. -->

The performance is evaluated on two different automated metrics: first, **BLEU score**; and second, a family of **Extractive Evaluations (EE)**. EE contains three different submetrics evaluating three different aspects of the generation. Since EE metrics are comparatively new than others, I'll briefly explain them here:

- **Content Selection (CS)**: precision (P%) and recall (R%) of unique relations extracted from generated text that are also extracted from golden text. This measures how well the generated document matches the gold document in terms of selecting which records to generate.

- **Relation Generation (RG)**: precision (P%) and number of unique relations (#) extracted from generated text that also appear in structured input provided. This measures how well the system is able to generate text containing factual (i.e., correct) records.

- **Content Ordering (CO)**: normalized Damerau-Levenshtein Distance (DLD%) between the sequences of records extracted from golden text and that extracted from generated text. This measures how well the system orders the records it chooses to discuss.

I am not explaining other evaluation metrics here, I'll try to do that in some later post.

<!-- | **Model**           | **BLEU** | **CS (P% & R%)** | **RG (P% & #)** | **CO (DLD%)** |  **Paper / Source** | **Code** |
| ------------- | :-----: | :-----: | :-----: | :-----:| --- | --- |
| **Rebuffel, Clément, et al. (2020)** <sup>[[4]](#myfootnote4)</sup> | 17.50 | 39.47 & 51.64 | 89.46 & 21.17 | 18.90 | [A Hierarchical Model for Data-to-Text Generation](https://link.springer.com/chapter/10.1007/978-3-030-45439-5_5) |[Official](https://github.com/KaijuML/data-to-text-hierarchical) |
| **Puduppully et al. (2019)** <sup>[[3]](#myfootnote3)</sup> | 16.50 | 34.18 & 51.22 | 87.47 & 34.28 | 18.58 | [Data-to-text generation with content selection and planning](https://www.aaai.org/ojs/index.php/AAAI/article/view/4668) |[Official](https://github.com/ratishsp/data2text-plan-py) |
| **Wiseman et al. (2017)** <sup>[[2]](#myfootnote2)</sup> | 14.49 | 22.17 & 27.16 | 71.82 & 12.82 | 8.68 | [Challenges in Data-to-Document Generation](https://www.aclweb.org/anthology/D17-1239.pdf) |[Official](https://github.com/harvardnlp/data2text) | -->

### WebNLG
The [WebNLG challenge](https://webnlg-challenge.loria.fr/) consists in mapping data to text. The training data consists of Data/Text pairs where the data is a set of triples extracted from DBpedia and the text is a verbalisation of these triples. For example, given the three DBpedia triples (as shown in [a]), the aim is to generate a text (as shown in [b]):

* **[a]**. (John_E_Blaha birthDate 1942_08_26) (John_E_Blaha birthPlace San_Antonio) (John_E_Blaha occupation Fighter_pilot)

* **[b]**. John E Blaha, born in San Antonio on 1942-08-26, worked as a fighter pilot.

The performance is evaluated on the basis of **BLEU, METEOR and TER scores**. The data from WebNLG Challenge 2017 can be downloaded [here](https://gitlab.com/shimorina/webnlg-dataset).

<!-- | **Model**           | **BLEU** | **METEOR** | **TER** |  **Paper / Source** | **Code** |
| ------------- | :-----: | :-----: | :-----: | --- | --- |
| **Kale, Mihir. (2020)** <sup>[[9]](#myfootnote9)</sup> | 57.1 | 0.44 |  | [Text-to-Text Pre-Training for Data-to-Text Tasks](https://arxiv.org/pdf/2005.10433v2.pdf) |  |
| **Moryossef et al. (2019)** <sup>[[5]](#myfootnote5)</sup> | 47.4 | 0.391 | 0.631 | [Step-by-Step: Separating Planning from Realization in Neural Data-to-Text Generation](https://www.aclweb.org/anthology/N19-1236.pdf) | [Official](https://github.com/AmitMY/chimera) |
| **Baseline** | 33.24 | 0.235436 | 0.613080 | [Baseline system provided during the challenge](https://webnlg-challenge.loria.fr/challenge_2017/#webnlg-baseline-system) |[Official](https://gitlab.com/webnlg/webnlg-baseline) | -->

<!-- **P.S.**: The **test dataset** of WebNLG consists of **total 15 categories**, out of which 10 (**seen**) catgories are used for training while 5 (**unseen**) are not.  -->
<!-- The results reported here are those obtained on overall test data, i.e., all 15 categories. -->

### Meaning Representations

The dataset was first provided for the [E2E Challenge](http://www.macs.hw.ac.uk/InteractionLab/E2E/) in 2017. It is a crowd-sourced data set of 50k instances in the restaurant domain.Each instance consist of a dialogue act-based meaning representations (MR) and up to 5 references in natural language (NL). For example:

* **MR**: name[The Eagle], eatType[coffee shop], food[French], priceRange[moderate], customerRating[3/5], area[riverside], kidsFriendly[yes], near[Burger King]

* **NL**: “The three star coffee shop, The Eagle, gives families a mid-priced dining experience featuring a variety of wines and cheeses. Find The Eagle near Burger King.”

The performance is evaluated using **BLEU, NIST, METEOR, ROUGE-L, CIDEr scores**. The data from E2E Challenge 2017 can be downloaded [here](https://github.com/tuetschek/e2e-dataset/releases/download/v1.0.0/e2e-dataset.zip).

<!-- | **Model**           | **BLEU** | **NIST** | **METEOR** | **ROUGE-L** | **CIDEr** |  **Paper / Source** | **Code** |
| ------------- | :-----: | :-----: |:-----: |:-----: | :-----: | --- | --- |
| **Shen, Sheng, et al. (2019)** <sup>[[7]](#myfootnote6)</sup> | 68.60 | 8.73 | 45.25 | 70.82 | 2.37 | [Pragmatically Informative Text Generation](https://www.aclweb.org/anthology/N19-1410.pdf) |[Official](https://github.com/sIncerass/prag_generation) |
| **Elder, Henry, et al. (2019)** <sup>[[8]](#myfootnote8)</sup> | 67.38 | 8.7277 | 45.72 | 71.52 | 2.2995 | [Designing a Symbolic Intermediate Representation for Neural Surface Realization](https://www.aclweb.org/anthology/W19-2308.pdf) | |
| **Gehrmann, Sebastian, et al. (2018)** <sup>[[6]](#myfootnote7)</sup> | 66.2 | 8.60 | 45.7 | 70.4 | 2.34 | [End-to-End Content and Plan Selection for Data-to-Text Generation](https://www.aclweb.org/anthology/W18-6505.pdf) |[Official](https://github.com/sebastianGehrmann/diverse_ensembling) |
| **Baseline** | 65.93 | 8.61 | 44.83 | 68.50 | 2.23 | [Baseline system provided during the challenge](http://www.macs.hw.ac.uk/InteractionLab/E2E/#baseline) |[Official](https://github.com/UFAL-DSG/tgen/tree/master/e2e-challenge) | -->

## Further Steps
<!-- - I would recommend looking at the **data-to-text section** of [Papers with Code](https://paperswithcode.com/task/data-to-text-generation). -->
- For a detailed review of the field, I would recommed reading this [survey paper](https://www.jair.org/index.php/jair/article/download/11173/26378/).
- [Here](https://aclweb.org/aclwiki/Data_sets_for_NLG) you can find a list of **public datasets** available for D2T NLG.
- Have a look at the **ACL's Special Interest Group on Natural Language Generation** - [ACL SIGGEN](https://aclweb.org/aclwiki/SIGGEN).
- Would recommend to follow [Prof. Ehud Reiter's Blog](https://ehudreiter.com/blog-index/), he writes a lot on the issues of NLG (alsow w/ ML/DL) research.

<!-- ## References
<a name="myfootnote1">[1]</a> Albert Gatt and Emiel Krahmer. 2018. [Survey of the state of the art in natural language generation: core tasks, applications and evaluation](https://www.jair.org/index.php/jair/article/download/11173/26378/). J. Artif. Int. Res. 61, 1 (January 2018), 65–170.

<a name="myfootnote2">[2]</a> Wiseman, Sam, Stuart M. Shieber, and Alexander M. Rush. "[Challenges in Data-to-Document Generation](https://www.aclweb.org/anthology/D17-1239.pdf)." Proceedings of the 2017 Conference on Empirical Methods in Natural Language Processing. 2017.

<a name="myfootnote3">[3]</a> Puduppully, Ratish, Li Dong, and Mirella Lapata. "[Data-to-text generation with content selection and planning](https://www.aaai.org/ojs/index.php/AAAI/article/view/4668)." Proceedings of the AAAI Conference on Artificial Intelligence. Vol. 33. 2019.

<a name="myfootnote4">[4]</a> Rebuffel, Clément, et al. "[A Hierarchical Model for Data-to-Text Generation](https://link.springer.com/chapter/10.1007/978-3-030-45439-5_5)." European Conference on Information Retrieval. Springer, Cham, 2020.

<a name="myfootnote5">[5]</a> Moryossef, Amit, Yoav Goldberg, and Ido Dagan. "[Step-by-Step: Separating Planning from Realization in Neural Data-to-Text Generation](https://www.aclweb.org/anthology/N19-1236.pdf)." Proceedings of the 2019 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, Volume 1 (Long and Short Papers). 2019.

<a name="myfootnote6">[6]</a> Gehrmann, Sebastian, et al. "[End-to-End Content and Plan Selection for Data-to-Text Generation](https://www.aclweb.org/anthology/W18-6505.pdf)." Proceedings of the 11th International Conference on Natural Language Generation. 2018.

<a name="myfootnote7">[7]</a> Shen, Sheng, et al. "[Pragmatically Informative Text Generation](https://www.aclweb.org/anthology/N19-1410.pdf)." Proceedings of the 2019 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, Volume 1 (Long and Short Papers). 2019.

<a name="myfootnote8">[8]</a> Elder, Henry, et al. "[Designing a Symbolic Intermediate Representation for Neural Surface Realization](https://www.aclweb.org/anthology/W19-2308.pdf)." Proceedings of the Workshop on Methods for Optimizing and Evaluating Neural Language Generation. 2019.

<a name="myfootnote9">[9]</a> Kale, Mihir. "[Text-to-Text Pre-Training for Data-to-Text Tasks](https://arxiv.org/pdf/2005.10433v2.pdf)" arXiv preprint arXiv:2005.10433 (2020).
 -->

 
<!-- <style class="fallback">body{visibility:hidden}</style><script>markdeepOptions={tocStyle:'long'};</script>
Markdeep:<script src="https://casual-effects.com/markdeep/latest/markdeep.min.js?" charset="utf-8"></script> -->
