

<!-- Title -->
<br />
<p align="center">
    <h1 align="center">DL-Hard</h1>
    <h2 align="center">Annotated Deep Learning Dataset For Passage and Document Retrieval</h2>

<!-- TABLE OF CONTENTS -->
  <h5>Table of Contents</h5>
  <ol>
    <li><a href="#overview">Overview</a>
    <li><a href="#dataset">Dataset</a></li>
    <li><a href="#hard-queries">Hard Queries</a></li>
    <li><a href="#annotations">Annotations</a></li>
    <li><a href="#entity-links">Entity Links</a></li>
    <li><a href="#evaluation">Evaluation</a></li>
    <li><a href="#baselines">Baselines</a></li>
  </ol>

Paper overview: <a href="">link</a> 

Colab demo: <a href="https://colab.research.google.com/drive/1SduCZFg4ha46NOYPAeO2XWWLKtgLhG8C?usp=sharing">link</a> 

<!-- Overview -->
<h3 id="overview">Overview</h3>

<p> Deep Learning Hard (DL-HARD) is a new annotated dataset building upon standard deep learning benchmark evaluation 
datasets. It builds on TREC Deep Learning (<a href="https://microsoft.github.io/msmarco/TREC-Deep-Learning-2020.html">DL</a>) 
questions extensively annotated with query intent categories, answer types, wikified entities, topic categories, and 
result type metadata from a leading web search engine. Based on this data, we introduce a framework for identifying 
challenging questions. DL-HARD contains forty nine queries from the official 2019/2020 evaluation benchmark, half of 
which are newly and independently assessed. We perform experiments using the official submitted runs to DL on DL-HARD 
and find substantial differences in metrics and the ranking of participating systems. Overall, DL-HARD is a new resource 
that promotes research on neural ranking methods by focusing on challenging and complex queries. </p>

<p align="center">
    <img src="https://github.com/grill-lab/DL-Hard/blob/main/assets/dl_hard.png" alt="DL-Hard Diagram" width="700" height="400" >


<!-- Dataset -->
<h3 id="dataset">Dataset</h3>
<p> DL-Hard provides 49 queries for passage and document retrieval: </p> 
  <ul>
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/topics.tsv">Topics</a> (MS Marco format, i.e. Topic id, Query) 
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/dl_hard-passage.qrels">Passage qrels</a></li>
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/dl_hard-doc.qrels">Document qrels</a></li>
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/folds.json">Standard 5-folds</a></li>
  </ul> 

Corpus used is <a href="https://microsoft.github.io/msmarco/">MS Marco Passage and Document Corpus</a>.

Colab demo: <a href="https://colab.research.google.com/drive/1SduCZFg4ha46NOYPAeO2XWWLKtgLhG8C?usp=sharing">link</a> 

<!-- Hard Queries -->
<h3 id="hard-queries">Hard Queries</h3>

To differentiate system performance between large neural ranking models new challenging and complex benchmark queries 
are required. Hard queries were identified within the DL 2019/20 testsets through: 
<ol>
    <li><i>Automatic Hard Criteria</i>: Because manually reviewing all candidate queries is time consuming, we explore 
    the use of annotated metadata only, without requiring knowledge of system effectiveness. Google’s web search answer 
    type as a base with additional List and Reason query intents added to improve recall. Intent types matching 
    Quantity, Weather, and Language (mostly dictionary lookups) are excluded.</li> 
    <li><i>Manual Hard Criteria</i>: Each candidate question, generated from Automatic Hard Criteria, is manually 
    labeled by multiple authors and candidate hard queries discussed by all authors. Guidelines include: non-factoid, 
    beyond single passage, answerable, text-focused, mostly well-formed, and possibly complex. </li> 
</ol>

For example:
<ul>
    <li>Easy query from TREC DL 2020: <i>what is reba mcentire's net worth</i>. BM25 achieves Recall@100 = 1.0 
     and neural re-rankers achieve NDCG@10 > 0.9. </li>
    <li>Hard query from DL-Hard: <i>symptoms of different types of brain bleeds</i>. BM25 achieves Recall@100 < 0.7
     and neural re-rankers achieve NDCG@10 < 0.25.</li>
</ul>

See paper for more details: <a href="">link</a> 

We measure official TREC 2020 document run submissions on DL-HARD overlapping subsets and compare to the original DL 
Track. On an average relative basis for above-median system, DL-HARD NDCG@10 is 21.1% lower, RR is 23.2% lower, and 
Recall@100 is 19.6% lower. This included a new top system (‘ICIP_run1’), and each system changed on average 4.6 places. 
This large number of swaps supports that removing the easier queries allows for a better comparison between 
state-of-the-art retrieval systems.

<p> TREC 2020 document run submissions (DL-Hard vs. DL TREC):</p>
<p align="center">
    <img src="https://github.com/grill-lab/DL-Hard/blob/main/assets/dl_hard_dl_comparison.png" alt="Annotation Diagram" width="500" height="600" >


<!-- Annotations -->
<h3 id="annotations">Annotations</h3>
<p> Annotations are provided for 400 queries from the DL 2019/20 test datasets (<a href="https://github.com/grill-lab/DL-Hard/blob/main/annotations/query/annotations.tsv">link</a>).
The annotations tsv has the following columns: </p> 
  <ul>
    <li>0: <i>Topic id</i></li>
    <li>1: <i>Query</i></li>
    <li>2: <i>Query Intent</i>: Recently developed question intent taxonomy developed for web questions 
    [<a href="http://marksanderson.org/publications/my_papers/CHIIR21b.pdf">Cambazoglu et al., 2021</a>]. </li>
    <li>3: <i>Answer Type</i>: Manual annotation of target answer type for web questions. </li>
    <li>4: <i>Topic Domain</i>: Breakdown of questions by topic domain. </li>
    <li>5: <i>SERP Result Type</i>: Answer type provided by the Search Engine Results Page (SERP). HTML of queries found: <a href="https://drive.google.com/file/d/1l6o9U9Qtu21MS9F27bkfEbN95yeDsu9S/view?usp=sharing">here</a>. </li>
  </ul>
  
<p> Diagram of annotations:</p>
<p align="center">
    <img src="https://github.com/grill-lab/DL-Hard/blob/main/assets/annotation_flow.png" alt="Annotation Diagram" width="700" height="350" >

<p> See paper for full details: <a href="">link</a> </p> 

<!-- Entity Links -->
<h3 id="entity-links">Entity Links</h3>

<p> Golden entity links and high-recall results for SOTA entity linkers 
(REL [<a href="https://arxiv.org/pdf/2006.01969.pdf">Van Hulst et al., 2020</a>], 
BLINK [<a href="https://www.aclweb.org/anthology/2020.emnlp-main.519/">Wu et al., 2020</a>], 
GENRE [<a href="https://arxiv.org/abs/2010.00904">De Cao et al., 2020</a>], 
ELQ [<a href="https://arxiv.org/abs/2010.02413">Li et al., 2020</a>]) are provided for all 400 queries from the DL 
2019/20 test datasets. </p>

<p> Golden entity links to Wikipedia (2021/02/27) can be found: <a href="https://github.com/grill-lab/DL-Hard/blob/main/annotations/entity/gold-entity-judgements.json">here</a>. 
Also included are annotations: (1) <i>Answer in Link</i>: whether question is answered within linked Wikipedia page, and (2) <i>Core 
Entities in Wiki</i>: whether any core entities of the question were not found in Wikipedia. </p>

<p> SOTA entity linkers results can be found: <a href="https://github.com/grill-lab/DL-Hard/blob/main/annotations/entity/entity_linker_results.json">here</a></p>

<!-- Evaluation -->
<h3 id="evaluation">Evaluation</h3>

<p> Official metrics for DL-Hard are NDCG@10 and RR. For binary metrics, labels of two or greater should be considered as 
relevant. Thus, trec_eval command: <i>"trec_eval -l 2 -o -c -M1000 -q -m all_trec"</i>. </p>

<!-- Baselines -->
<h3 id="baselines">Baselines</h3>

<p>Baseline runs, tuned parameters and trec_evals can be found in the baselines directory: <a href="https://github.com/grill-lab/DL-Hard/tree/main/dataset/baselines/">link</a>. 
These runs utilize the <a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/folds.json">standard 5-folds</a> for cross-validation and the outlined trec_eval procedure.</p>

Colab demo: <a href="https://colab.research.google.com/drive/1SduCZFg4ha46NOYPAeO2XWWLKtgLhG8C?usp=sharing">link</a> 

*** More baselines coming soon!

<h5> Document Baselines: </h5>

<table class="tg">
<thead>
  <tr>
    <th class="tg-fymr">System</th>
    <th class="tg-fymr">NDCG@10</th>
    <th class="tg-fymr">RR</th>
    <th class="tg-0lax"><span style="font-weight:bold">MAP</span></th>
    <th class="tg-0pky"><span style="font-weight:bold">Recall@1000</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">BM25</td>
    <td class="tg-0pky">0.262</td>
    <td class="tg-0pky">0.347</td>
    <td class="tg-0lax">0.168</td>
    <td class="tg-0pky">0.817</td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+RM3</td>
    <td class="tg-0pky">0.310</td>
    <td class="tg-0pky">0.333</td>
    <td class="tg-0lax">0.248</td>
    <td class="tg-0pky">0.778</td>
  </tr>
  <tr>
    <td class="tg-0pky">BERT</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0pky"></td>
  </tr>
  <tr>
    <td class="tg-0pky">PARADE</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0pky"></td>
  </tr>
</tbody>
</table>

<h5> Passage Baselines: </h5>

<table class="tg">
<thead>
  <tr>
    <th class="tg-fymr">System</th>
    <th class="tg-fymr">NDCG@10</th>
    <th class="tg-fymr">RR</th>
    <th class="tg-0lax"><span style="font-weight:bold">MAP</span></th>
    <th class="tg-0pky"><span style="font-weight:bold">Recall@1000</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">BM25</td>
    <td class="tg-0pky">0.304</td>
    <td class="tg-0pky">0.508</td>
    <td class="tg-0lax">0.174</td>
    <td class="tg-0pky">0.654</td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+RM3</td>
    <td class="tg-0pky">0.261</td>
    <td class="tg-0pky">0.410</td>
    <td class="tg-0lax">0.158</td>
    <td class="tg-0pky">0.688</td>
  </tr>
  <tr>
    <td class="tg-0pky">BERT</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
    <td class="tg-0pky"></td>
  </tr>
</tbody>
</table>

