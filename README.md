

<!-- Title -->
<br />
<p align="center">
    <h1 align="center">DL-Hard</h1>
    <h2 align="center">Annotated Deep Learning Dataset For Passage and Document Retrieval</h2>

<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#overview">Overview</a>
    <li><a href="#dataset">Dataset</a></li>
    <li><a href="#annotations">Annotations</a></li>
    <li><a href="#entity-links">Entity Links</a></li>
    <li><a href="#evaluation">Evaluation</a></li>
    <li><a href="#baselines">Baselines</a></li>

  </ol>
</details>

Paper overview: <a href="">link</a> 

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

<!-- Dataset -->
<h3 id="dataset">Dataset</h3>
<p> DL-Hard provides 49 queries for passage and document retrieval: </p> 
  <ul>
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/topics.tsv">Topics</a> (MS Marco format, i.e. <topic id, query>) 
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/dl_hard-passage.qrels">Passage qrels</a></li>
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/dl_hard-doc.qrels">Document qrels</a></li>
    <li><a href="https://github.com/grill-lab/DL-Hard/blob/main/dataset/folds.json">Standard 5-folds</a></li>
  </ul> 


<!-- Annotations -->
<h3 id="annotations">Annotations</h3>
<p> Annotations are provided for 400 queries from the DL 2019/20 test datasets (<a href="https://github.com/grill-lab/DL-Hard/blob/main/annotations/query/annotations.tsv">link</a>).
The annotations tsv has the following columns: </p> 
  <ul>
    <li>0: Topic id</li>
    <li>1: Query</li>
    <li>2: Query Intent: Recently developed question intent taxonomy developed for web questions 
    [<a href="http://marksanderson.org/publications/my_papers/CHIIR21b.pdf">Cambazoglu et al., 2021</a>]. </li>
    <li>3: Answer Type: Manual annotation of target answer type for web questions. </li>
    <li>4: Topic Domain: Breakdown of questions by topic domain. </li>
    <li>5: SERP Result Type: Answer type provided by the Search Engine Results Page (SERP). HTML of queries found: <a href="https://drive.google.com/file/d/1l6o9U9Qtu21MS9F27bkfEbN95yeDsu9S/view?usp=sharing">here</a>. </li>
  </ul>
  
<p> Diagram of annotations:</p>
<img src="https://github.com/grill-lab/DL-Hard/blob/main/assets/annotation_flow.png" alt="Annotation Diagram">

<p> See paper for more details: <a href="">link</a> </p> 

<!-- Entity Links -->
<h3 id="entity-links">Entity Links</h3>

<p> Golden entity links and high-recall results for SOTA entity linkers 
(REL [<a href="https://arxiv.org/pdf/2006.01969.pdf">Van Hulst et al., 2020</a>], 
BLINK [<a href="https://www.aclweb.org/anthology/2020.emnlp-main.519/">Wu et al., 2020</a>], 
GENRE [<a href="https://arxiv.org/abs/2010.00904">De Cao et al., 2020</a>], 
ELQ [<a href="https://arxiv.org/abs/2010.02413">Li et al., 2020</a>]) are provided for all 400 queries from the DL 
2019/20 test datasets. </p>

<p> Golden entity links can be found: <a href="https://github.com/grill-lab/DL-Hard/blob/main/annotations/entity/gold-entity-judgements.json">here</a></p>

<p> SOTA entity linkers results can be found: <a href="https://github.com/grill-lab/DL-Hard/blob/main/annotations/entity/entity_linker_results.json">here</a></p>

 
<!-- Evaluation -->
<h3 id="evaluation">Evaluation</h3>

<p> Official metrics for DL-Hard are NDCG@10 and RR. For binary metrics, labels of two or greater should be considered as 
relevant. Thus, trec_eval command: <i>"trec_eval -l 2 -o -c -M1000 -q -m all_trec"</i>. </p>

<!-- Baselines -->
<h3 id="baselines">Baselines</h3>

<p>Baseline runs and trec_evals can be found in the baselines directory: <a href="https://github.com/grill-lab/DL-Hard/tree/main/dataset/baselines/">link</a>. 
These runs utilities the standard 5-folds for cross-validation and the outlined trec_eval procedure.</p>

<h5> Document Baselines: </h5>

<table class="tg">
<thead>
  <tr>
    <th class="tg-fymr">System</th>
    <th class="tg-fymr">NDCG@10</th>
    <th class="tg-fymr">RR</th>
    <th class="tg-0lax">Recall@1000</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">BM25</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+RM3</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0pky">BERT</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0pky">PARADE</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
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
    <th class="tg-0lax">Recall@1000</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">BM25</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0pky">BM25+RM3</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
  </tr>
  <tr>
    <td class="tg-0pky">BERT</td>
    <td class="tg-0pky"></td>
    <td class="tg-0pky"></td>
    <td class="tg-0lax"></td>
  </tr>
</tbody>
</table>



  

