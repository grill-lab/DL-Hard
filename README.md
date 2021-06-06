

<!-- Title -->
<br />
<p align="center">
    <h1 align="center">DL-Hard</h1>
    <h2 align="center">Annotated Deep Learning Dataset For Passage and Document Retrieval</h2>

<!-- TABLE OF CONTENTS -->
  <h5>Table of Contents</h5>
  <ol>
    <li><a href="#overview">Overview</a>
    <li><a href="#paper">Paper</a>
    <li><a href="#dataset">Dataset</a></li>
    <li><a href="#change-log">Change Log</a></li>
    <li><a href="#hard-queries">Hard Queries</a></li>
    <li><a href="#new-judgements">New Judgements</a></li>
    <li><a href="#annotations">Annotations</a></li>
    <li><a href="#entity-links">Entity Links</a></li>
    <li><a href="#evaluation">Evaluation</a></li>
    <li><a href="#baselines">Baselines</a></li>
    <li><a href="#future-work">Future Work</a></li>
  </ol>

Colab demo (Pyserini): <a href="https://colab.research.google.com/drive/1SduCZFg4ha46NOYPAeO2XWWLKtgLhG8C?usp=sharing">link</a>\
Colab demo (PyTerrier): <a href="https://colab.research.google.com/drive/1R-YP4yYfbSE2r1IfbcGnG_s7zTkM7zjM?usp=sharing">link</a>

<!-- Overview -->
<h3 id="overview">Overview</h3>

<p> Deep Learning Hard (DL-HARD) is a new annotated dataset building upon standard deep learning benchmark evaluation 
datasets. It builds on TREC Deep Learning (<a href="https://microsoft.github.io/msmarco/TREC-Deep-Learning-2020.html">DL</a>) 
questions extensively annotated with query intent categories, answer types, wikified entities, topic categories, and 
result type metadata from a leading web search engine. Based on this data, we introduce a framework for identifying 
challenging questions. DL-HARD contains 50 queries from the official 2019/2020 evaluation benchmark, half of 
which are newly and independently assessed. We perform experiments using the official submitted runs to DL on DL-HARD 
and find substantial differences in metrics and the ranking of participating systems. Overall, DL-HARD is a new resource 
that promotes research on neural ranking methods by focusing on challenging and complex queries. </p>

<p align="center">
    <img src="https://github.com/grill-lab/DL-Hard/blob/main/assets/dl_overview_4.png" alt="DL-Hard Diagram" width="700" height="400" >

Note, NIST judged/unjudged DL query counts in the diagram are approximated for simplicity (see track <a href="https://arxiv.org/abs/2105.07975">overview paper</a> for specifics). 
Due to the differences in TREC DL task querysets, DL-HARD provides 25 new document judgments and 27 new passage judgments. 
Both DL-HARD tasks have 50 queries overall.


<!-- Paper -->
<h3 id="paper">Paper</h3>

This work is published as a resource paper in SIGIR 2021.

Preprint available: <a href="https://arxiv.org/abs/2105.07975">link</a>
  
Correct citation: 

@inproceedings{mackie2021dlhard,\
 title={How Deep is your Learning: the DL-HARD Annotated Deep Learning Dataset},\
 author={Mackie, Iain and Dalton, Jeffrey and Yates, Andrew},\
 booktitle={Proceedings of the 44th International ACM SIGIR Conference on Research and Development in Information Retrieval},\
 year={2021}\
}


<!-- Dataset -->
<h3 id="dataset">Dataset</h3>
<p> DL-Hard provides 50 queries for passage and document retrieval: </p> 
  <ul>
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/topics.tsv">Topics</a> (MS Marco format, i.e. Topic id, Query) 
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/dl_hard-passage.qrels">Passage qrels</a></li>
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/dl_hard-doc.qrels">Document qrels</a></li>
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/folds.json">Standard 5-folds</a></li>
  </ul> 

Corpus used is <a href="https://microsoft.github.io/msmarco/">MS Marco Passage and Document Corpus</a>.

Available via ir_datasets: <a href="https://github.com/allenai/ir_datasets">link</a>

Colab demo (Pyserini): <a href="https://colab.research.google.com/drive/1SduCZFg4ha46NOYPAeO2XWWLKtgLhG8C?usp=sharing">link</a>\
Colab demo (PyTerrier): <a href="https://colab.research.google.com/drive/1R-YP4yYfbSE2r1IfbcGnG_s7zTkM7zjM?usp=sharing">link</a>


<!-- Change Log -->
<h3 id="change-log">Change Log</h3>

Major dataset changes historic users should be aware:
<ul>
    <li> <b>4th May 2021</b>: Topic 273695 added for passage and documents (qrels, baselines, topics.tsv, folds, etc.) We wanted a round 50 topics testset vs. original 49. 
    <li> <b>20th May 2021</b>: Topics 1056416 and 1103153 added to passage qrels (see <a href="https://github.com/grill-lab/DL-Hard/issues/1">issue #1</a>)  
</ul> 


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

See paper for more details:  <a href="https://arxiv.org/abs/2105.07975">link</a>

We measure official TREC 2020 document run submissions on DL-HARD overlapping subsets and compare to the original DL 
Track. On an average relative basis for above-median system, DL-HARD NDCG@10 is 21.1% lower, RR is 23.2% lower, and 
Recall@100 is 19.6% lower. This included a new top system (‘ICIP_run1’), and each system changed on average 4.6 places. 
This large number of swaps supports that removing the easier queries allows for a better comparison between 
state-of-the-art retrieval systems.

<p> Top 20 systems TREC 2020 document run submissions (DL-Hard vs. DL TREC):</p>
<p align="center">
    <img src="https://github.com/grill-lab/DL-Hard/blob/main/assets/dl_vs_dl_hard.png" alt="Annotation Diagram" width="600" height="475" >


<!-- New Judgements -->
<h3 id="new-judgements">New Judgements</h3>

The resource uses the full provided NIST assessments for the 25 previously judged queries. There are also new passage and 
document judgments provided for the 25 unjudged queries from TREC DL: 
 <ul>
    <li><i>Passage Judgements</i>: <a href="https://github.com/grill-lab/DL-Hard/blob/main/annotations/new_judgements/new_judgements-passage.passage-level.qrels">link</a> </li>
    <li><i>Document Judgements (Mapping Passage-Level Judgments)</i>: <a href="https://github.com/grill-lab/DL-Hard/blob/main/annotations/new_judgements/new_judgements-doc.passage-level.qrels">link</a> </li>
    <li><i>Document Judgements (Document-Level Judgments)</i>:  <a href="https://github.com/grill-lab/DL-Hard/blob/main/annotations/new_judgements/new_judgements-doc.doc-level.qrels">link</a></li> 
 </ul>
 
Experienced IR researchers perform the annotations following the DL guidelines. We find the Krippendorff’s alpha is 0.47 
 on the passage judgements, which indicates moderate agreement. Krippendorff’s alpha drops to 0.12 when considering the 
 agreement on document judgments, illustrating the difficulty of automatically transferring passage judgements to documents. 
 For this reason, we re-produced document judgments annotating at a document level, which achieved Krippendorff’s alpha of 0.430. 

On further analysis, most disagreements with a difference greater than 1 relevance grade looked related to different query 
interpretations. e.g., accepting any definition of "geon" versus looking for a specific definition (similar to 
"define visceral"). To remove this ambiguity, further work will look to add query descriptions.

Note, the official DL-Hard document qrels (<a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/dl_hard-doc.qrels">link</a>)
 use document-level judgements and passage qrels (<a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/dl_hard-passage.qrels">link</a>)
  use passage-level judgements.  

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

<p> See paper for full details:  <a href="https://arxiv.org/abs/2105.07975">link</a>

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
These runs utilize the <a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/folds.json">standard 5-folds</a> 
for cross-validation (3x train folds, 1x validation fold, 1x test fold) and the outlined trec_eval procedure.</p>

Colab demo (Pyserini): <a href="https://colab.research.google.com/drive/1SduCZFg4ha46NOYPAeO2XWWLKtgLhG8C?usp=sharing">link</a>\
Colab demo (PyTerrier): <a href="https://colab.research.google.com/drive/1R-YP4yYfbSE2r1IfbcGnG_s7zTkM7zjM?usp=sharing">link</a>

<h5> Document Baselines: </h5>

Initial retrieval <i>BM25</i> and <i>BM25+RM3</i> runs use <a href="https://github.com/castorini/pyserini">Pyserini</a>. 

<i>BERT-MaxP(Zero-Shot)</i> and <i>T5-MaxP(Zero-Shot)</i> re-rankers use <a href="https://github.com/castorini/pygaggle">pygaggle</a> 
standard models that are fine-tuned on MS-MARCO (but not fine-tuned on DL-HARD folds). The documents are sharded into 5 sentence chunks with 
no overlap and the max passage score is taken to represent the document (<a href="https://arxiv.org/pdf/2003.06713.pdf">Nogueira et al., 2020</a>) .

<i>BERT-MaxP</i> and <i>Electra-MaxP</i> is firstly fine-tuned on MS Marco, before further fine-tuning on the provided 
DL-HARD training folds. Performance on the validation fold is used to select the optimal epoch for the each corresponding 
test fold. See <a href="https://arxiv.org/pdf/1905.09217.pdf">Dai and Callan (2019)</a> for implementation details.
<i>PARADE-BERT</i> and <i>PARADE-Electra</i> are trained in a similar procedure for DL-HARD. See 
<a href="https://arxiv.org/pdf/2008.09093.pdf">Li at al. (2020)</a> for implementation details.


<table class="tg">
<thead>
  <tr>
    <th class="tg-fymr">System</th>
    <th class="tg-fymr">NDCG@10</th>
    <th class="tg-fymr">RR</th>
    <th class="tg-fymr">MAP</th>
    <th class="tg-fymr">Recall@1000</th>
    <th class="tg-fymr">Run</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">BM25</td>
    <td class="tg-0pky">0.272</td>
    <td class="tg-0pky">0.368</td>
    <td class="tg-0pky">0.174</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25.run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+RM3</td>
    <td class="tg-0pky">0.279</td>
    <td class="tg-0pky">0.365</td>
    <td class="tg-0pky">0.174</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Brm3.run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+BERT-MaxP(Zero-Shot)</td>
    <td class="tg-0pky">0.310</td>
    <td class="tg-0pky">0.405</td>
    <td class="tg-0pky">0.187</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Bbert-mp(zs).run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+BERT-MaxP</td>
    <td class="tg-0pky">0.317</td>
    <td class="tg-0pky">0.402</td>
    <td class="tg-0pky">0.200</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Bbert-mp.run">link</a></td>
  </tr>
  <tr>
    <tr>
    <td class="tg-0pky">BM25+RM3+BERT-MaxP(Zero-Shot)</td>
    <td class="tg-0pky">0.314</td>
    <td class="tg-0pky">0.415</td>
    <td class="tg-0pky">0.188</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Brm3%2Bbert-mp(zs).run">link</a></td>
  </tr>
  <tr>
    <tr>
    <td class="tg-0pky">BM25+RM3+BERT-MaxP</td>
    <td class="tg-0pky">0.295</td>
    <td class="tg-0pky">0.443</td>
    <td class="tg-0pky">0.181</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Brm3%2Bbert-mp.run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+T5-MaxP(Zero-Shot)</td>
    <td class="tg-0pky">0.327</td>
    <td class="tg-0pky">0.367</td>
    <td class="tg-0pky">0.184</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="/Users/iain/LocalStorage/coding/github/DL-Hard/dataset/baselines/doc/bm25+t5-mp(zs).run">link</a></td>
  </tr>
    <tr>
    <td class="tg-0pky">BM25+RM3+T5-MaxP(Zero-Shot)</td>
    <td class="tg-0pky">0.307</td>
    <td class="tg-0pky">0.359</td>
    <td class="tg-0pky">0.170</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Brm3%2Bt5-mp(zs).run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+Electra-MaxP</td>
    <td class="tg-0pky"><b>0.385</b></td>
    <td class="tg-0pky">0.448</td>
    <td class="tg-0pky"><b>0.216</b></td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Belectra-mp.run">link</a></td>
  </tr>
    <tr>
    <td class="tg-0pky">BM25+RM3+Electra-MaxP</td>
    <td class="tg-0pky">0.380</td>
    <td class="tg-0pky">0.461</td>
    <td class="tg-0pky">0.215</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Brm3%2Belectra-mp.run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+PARADE-BERT</td>
    <td class="tg-0pky">0.299</td>
    <td class="tg-0pky">0.413</td>
    <td class="tg-0pky">0.174</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Bparade-bert.run">link</a></td>
  </tr>
    <tr>
    <td class="tg-0pky">BM25+RM3+PARADE-BERT</td>
    <td class="tg-0pky">0.313</td>
    <td class="tg-0pky">0.419</td>
    <td class="tg-0pky">0.187</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Brm3%2Bparade-bert.run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+PARADE-Electra</td>
    <td class="tg-0pky">0.356</td>
    <td class="tg-0pky"><b>0.498</b></td>
    <td class="tg-0pky">0.207</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Bparade-electra.run">link</a></td>
  </tr>
    <tr>
    <td class="tg-0pky">BM25+RM3+PARADE-Electra</td>
    <td class="tg-0pky">0.357</td>
    <td class="tg-0pky">0.489</td>
    <td class="tg-0pky">0.211</td>
    <td class="tg-0pky">0.775</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/doc/bm25%2Brm3%2Bparade-electra.run.eval">link</a></td>
  </tr>
</tbody>
</table>

<h5> Passage Baselines: </h5>

Initial retrieval <i>BM25</i> and <i>BM25+RM3</i> runs use <a href="https://github.com/castorini/pyserini">Pyserini</a>. 

<i>BERT(Zero-Shot)</i> and <i>T5(Zero-Shot)</i> re-rankers use <a href="https://github.com/castorini/pygaggle">pygaggle</a> 
standard models that are fine-tuned on MS-MARCO (not further fine-tuned on DL-HARD folds).

<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky">System</th>
    <th class="tg-0pky">NDCG@10</th>
    <th class="tg-0pky">RR</th>
    <th class="tg-0pky">MAP</th>
    <th class="tg-0pky">Recall@1000</th>
    <th class="tg-0pky">Run</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">BM25</td>
    <td class="tg-0pky">0.304</td>
    <td class="tg-0pky">0.504</td>
    <td class="tg-0pky">0.173</td>
    <td class="tg-0pky">0.669</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/passage/bm25.run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+RM3</td>
    <td class="tg-0pky">0.273</td>
    <td class="tg-0pky">0.409</td>
    <td class="tg-0pky">0.175</td>
    <td class="tg-0pky">0.703</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/passage/bm25%2Brm3.run">link</a></td>
  </tr>
   <tr>
    <td class="tg-0pky">BM25+BERT(Zero-Shot)</td>
    <td class="tg-0pky">0.399</td>
    <td class="tg-0pky">0.558</td>
    <td class="tg-0pky">0.229</td>
    <td class="tg-0pky">0.669</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/passage/bm25%2Bbert(zs).run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+RM3+BERT(Zero-Shot)</td>
    <td class="tg-0pky">0.395</td>
    <td class="tg-0pky">0.559</td>
    <td class="tg-0pky">0.234</td>
    <td class="tg-0pky">0.703</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/passage/bm25%2Brm3%2Bbert(zs).run">link</a></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+T5(Zero-Shot)</td>
    <td class="tg-0pky"><b>0.408</b></td>
    <td class="tg-0pky"><b>0.591</b></td>
    <td class="tg-0pky"><b>0.238</b></td>
    <td class="tg-0pky">0.669</td>
    <td class="tg-0pky"><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/baselines/passage/bm25%2Brm3%2Bt5(zs).run">link</a></td>
  </tr>
    <tr>
    <td class="tg-0pky">BM25+RM3+T5(Zero-Shot)</td>
    <td class="tg-0pky">0.396</td>
    <td class="tg-0pky">0.577</td>
    <td class="tg-0pky"><b>0.238</b></td>
    <td class="tg-0pky">0.703</td>
    <td class="tg-0pky"><a href="">link</a> </td>
  </tr>
</tbody>
</table>

<!-- Future Work -->
<h3 id="future-work">Future Work </h3>

Please suggest any future extensions or bug fixes on github or email (i.mackie.1@research.gla.ac.uk). 

Current planned work:
 <ul>
    <li> Add TREC-style 'descriptions' to queries to disambiguate answers.</li>
    <li> Dense retrieval baselines (ColBERT, DPR, etc.). </li>
    <li> Create MS Marco duplicate passage list. </li>
    <li> Add a complementary entity ranking task. </li>
 </ul>
