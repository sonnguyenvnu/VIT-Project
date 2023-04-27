# Can An Old Fashioned Feature Extraction and A Light-weight Model Improve Vulnerability Type Identification Performance?
Recent advances in automated vulnerability detection have achieved potential results in helping developers determine vulnerable components. However, after detecting vulnerabilities, investigating to fix vulnerable code is a non-trivial task. In fact, the types of vulnerability, such as buffer overflow or memory corruption, could help developers quickly understand the nature of the weaknesses and localize vulnerabilities for security analysis. In this work, we investigate the problem of vulnerability type identification (VTI). The problem is modeled as the multi-label classification task, which could be effectively addressed by "pre-training, then fine-tuning" framework with deep pre-trained embedding models. We evaluate the performance of the well-known and advanced pre-trained models for VTI on a large set of vulnerabilities. Surprisingly, their performance is not much better than that of the classical baseline approach with an old-fashioned bag-of-word, TF-IDF. Meanwhile, these deep neural network approaches cost much more resources and require GPU. We also introduce a lightweight independent component to refine the predictions of the baseline approach. Our idea is that the types of vulnerabilities could strongly correlate to certain code tokens (distinguishing tokens) in several crucial parts of programs. The distinguishing tokens for each vulnerability type are statistically identified based on their prevalence in the type versus the others. Our results show that the baseline approach enhanced by our component can outperform the state-of-the-art deep pre-trained approaches while retaining very high efficiency. Furthermore, the proposed component could also improve the neural network approaches by up to 92.8% in macro-average F1.


## Dataset

To evaluate VTI approaches, we use <a href="https://github.com/ZeoVan/MSR_20_Code_vulnerability_CSV_Dataset">BigVul</a>, which is one of the largest vulnerability datasets and provides the vulnerability types of each case. The dataset is collected from 348 real-world C/C++ projects on GitHub, such as Chromium, Linux, Android, PHP, OpenSSL, QEMU, and FFmpeg. The dataset includes about 10,900 vulnerable functions in 13 vulnerability types and 44,603 vulnerable lines of code. In this dataset, the types of each vulnerable function are extracted from its corresponding CVE-Details. More information about BigVul could be found at:

``https://doi.org/10.1145/3379597.3387501``

One could download the BigVul dataset at:

``https://drive.google.com/file/d/1-0VhnHBp9IGh90s2wCNjeCMuy70HPl8X/view?usp=sharing``


## Source code

We use <a href="https://jupyter.org/">Jupyter Notebook</a> to perform our experiments.
There are three main files:
<ol>
  <li>[TF_IDF_and_Word2Vec.ipynb](TF_IDF_and_Word2Vec.ipynb): Preprocessing, training, and evaluating the approaches using TF-IDF and Word2Vec. We included Glove in that file, in case you are interested in playing around with Glove.</li>
  <li>[CodeBERT.ipynb](CodeBERT.ipynb): Preprocessing, training, and evaluating the approach using pre-trained model CodeBERT</li>
  <li>[ENHANCED.ipynb](ENHANCED.ipynb): Preprocessing and perform our enhancement method for VIT approaches</li>
</ol>

For each file, you need to put the paths to the training, evaluating, and testing datasets in your machine. 
For ENHANCED.ipynb, you need to run other a VIT approach first, save the results in .csv file before feeding the results to the enhancement step.
