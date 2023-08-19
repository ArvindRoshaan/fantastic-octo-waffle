# Expert answers in a fash: Building domain-specifc Information Retrieval (IR) and Question Answering (QA) system

IIT Hyderabad contingent participated in the Inter IIT Tech Meet 2023 AI/ ML challenge sponsored by [DevRev](https://devrev.ai/). Teams from 20+ IITs participated and we ranked 4th on presentation, report and code work!

### Problem Statement
Given a domain specific-query, retrieve the most relevant passage from a multi-domain corpus and extract the answer from the passage. The challenge had certain incredible restrictions:
1) Training and Inference can ONLY use a Standard Google Colab CPU. *Yes, NO GPUs allowed for even training the models!*   
2) Inference time to be within 1 second per query. Quicker the better!

Example #1:  
*[Input] Query from domain* "Solar Energy": "What are the insolation levels of most populated areas?"  
*[Desired Output] Most relevant passage from domain* "Solar Energy": "The Earth receives 174,000 terawatts (TW) of incoming solar radiation (insolation) at the upper atmosphere. Approximately 30% is reflected back to space while the rest is absorbed by clouds, oceans and land masses. The spectrum of solar light at the Earth's surface is mostly spread across the visible and near-infrared ranges with a small part in the near-ultraviolet. Most people around the world live in areas with insolation levels of 150 to 300 watts per square meter or 3.5 to 7.0 kWh/m2 per day."  
*[Desired Output] Can the query be answerd with a passage from the same domain*: "Yes"  
*[Desired Output] Answer (if exists)*: "150 to 300 watts per square meter or 3.5 to 7.0 kWh/m2 per day"  

### Data
The data had the following attributes  
1) Theme (a.k.a domain): x unique themes. Example: Solar Energy, , etc.,  
2) Paragraph (a.k.a passage): x paragraphs per theme on an average with minimum and maximum as x and x respectively. x words on an average per paragraph with minimum and maximum as x and x respectively  
3) Question (a.k.a query): x query per paragraphs on an average with minimum and maximum as x and x respectively. x query per theme on an average with minimum and maximum as x and x respectively. x words on an average per query with minimum and maximum as x and x respectively  
4) Answer_possible: True/ False  
5) Answer_text:  
6) Answer_start:  

### Approach
We approach this problem in a two-step fashion keeping in mind the hard compute constraints. First, we attempt to extract top 5 passages from the theme (of the query) using various information retrieval techniques, both classical as well as neural: TF-IDF (Term Frequency - Inverse Document Frequency), Latent Semantic Indexing (LSI), Elastic Search and pre-trained multi-qa-mpnet-base-dot-v1 model from sentence-transformers (This model was tuned for semantic search: Given a query/question, if can find relevant passages. It was trained on a large and diverse set of (question, answer) pairs). Then we re-rank the top-5 passages first among classical IR methods and then re-rank them again against the neural mathod. Thus this novel two-stage ensemble of top-5 passages from classical and neural information retrieval models enables effcient re-ranking of passages compared to expensive cross-encoder methods. Based on this ensemble strategy we find top 1 passage for our query

Second, we pass the (query, potential_passage) pair to a pre-trained neural question answering model (SqueezeBERT - as we found it to be extremely efficient and accurate). This model can handle the case when the query cannot be answered by the potential_passage.

### Result


### IIT Hyderabad Contingent:
1) [Arvind Roshaan](https://www.linkedin.com/in/arvind-roshaan/)
2) [Ayush Kumar Singh](https://www.linkedin.com/in/ayush-kumar-singh-272a471b9/)
3) [Srikaran P](https://www.linkedin.com/in/srikaran-p-b82221214/)
4) [Tadipatri Uday Kiran Reddy](https://www.linkedin.com/in/tadipatri-uday-kiran-reddy/)
5) [Sayantan Biswas](https://www.linkedin.com/in/sayantan-biswas-14949b203/)
6) [Shrey Satapara](https://www.linkedin.com/in/shreysatapara/)
7) [Saumya Mundra](https://www.linkedin.com/in/saumya-mundra/)
8) [Pranav Sai Ananthoju](https://www.linkedin.com/in/pranav-sai-ananthoju-683225214/)
9) [Dishank Jain](https://www.linkedin.com/in/dishank-jain-567b9b213/)
10) [Lokesh J K](https://www.linkedin.com/in/lokesh-jk/)
11) [Anmol Rastogi](https://www.linkedin.com/in/anmol-rastogi-492184283/)
