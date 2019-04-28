
## Compositional Word Vectors  

Presenter : 연선우 (KAIST)  

### Overview  
Propose more accurate word embedding model  
![
](https://lh3.googleusercontent.com/Zx2et2qcLUDfUPQ2f3yh-dgiXAXQSS-tfhnf2xVQoMtq8gWRdSJr4nEoCpQJjleJE4gvzVDT7f6X "cwv1")  

Propose conditions of compositional word vectors  
![
](https://lh3.googleusercontent.com/YucsRHBRqChe_8pH7u5kwq0KBUP9qgSxC9gFQY_vdmy6PjLbe7DW6nY2zi1ZOY-2uqGXICiOknsl "cwv2")  

Our model satisfies Compositionality  
![
](https://lh3.googleusercontent.com/L5oxx0oImBqtOkv9LSJsEogGqXxO4hc5DCnxtESP8LXysI93ba5QI8Emd-AWYWh0jrN0uxPD1fip "cwv3")  

### Problems  

- Arora 2016 prove compositionality of Skip-Gram and GloVe on **isotropy assumption** of word vector space.  
- Gitten 2017 prove compositionality of Skip-Gram on **uniform word frequency distribution assumption**, p(w) = 1/|v|.  

isotropy assumption, uniform word frequency distribution assumption → **Necessity of unrealistic assumptions**  

### Compositionality  
- In Gitten 2017 ACL, they propose definition of compositionality of word vectors.  
![
](https://lh3.googleusercontent.com/0RLQtauAfT1JAhTBUcJ4esgzeYJO3viUIvUpreeH8MemiKOCkKo3U3kjZUVhd_p_9Ir_76SdWBlw "cwv4")  
Word( c ) and its paraphrase( C )  
![
](https://lh3.googleusercontent.com/hawhr5CqTVqJOSM6rGsjVxa8gtJkfU4he3YnXdSKG1F0gOsV-v9ke22vCQ4bLShCgiLXW0X55Xmx "cwv5")  

- In Gitten 2017 ACL, they propose two conditions of compositional word vectors.  
**But it Requires additional unrealistic assumption**  
![
](https://lh3.googleusercontent.com/3NPRFZskO2KtHB3xmxSTWCjh_k6uLYryM-Qq_PJXb9inf9g7qt1gHtowvktr2f0Mn6wI-f3NyoFe "cwv6")  

### Proposed Conditions for compositional word vectors  
- **Theorem.** *If a word embedding model satisties conditionis below, then the word embedding vector can be represented by the vector sum of words their paraghrase sentence.*  
![
](https://lh3.googleusercontent.com/N4OFsZJgC9gWrRf1f1dVeQXREvE8aNC48KyLGMYxpL3QX8G_GBhfWbpftlkoqg0kzP0BUo54E6Nd "cwv7")  

### Proposed Word Embedding Models  
- **Theorem.** *Our model satisfies compositionality*  
![
](https://lh3.googleusercontent.com/WJ62-PjuFR9zBGFemyek-k4WIetn205pbS9dVLB_Nbo4_EQjvoZoD7TOcbnfYfmZRnlGU3EK_fMT "cwv8")  

### Experiment  
**Word Similarity**  
Propose more accurate word embedding model  
![
](https://lh3.googleusercontent.com/Zx2et2qcLUDfUPQ2f3yh-dgiXAXQSS-tfhnf2xVQoMtq8gWRdSJr4nEoCpQJjleJE4gvzVDT7f6X "cwv1")  

**Sentence Similarity**  
Propose conditions of compositional word vectors  
![
](https://lh3.googleusercontent.com/YucsRHBRqChe_8pH7u5kwq0KBUP9qgSxC9gFQY_vdmy6PjLbe7DW6nY2zi1ZOY-2uqGXICiOknsl "cwv2")  

Our model satisfies Compositionality  
![
](https://lh3.googleusercontent.com/L5oxx0oImBqtOkv9LSJsEogGqXxO4hc5DCnxtESP8LXysI93ba5QI8Emd-AWYWh0jrN0uxPD1fip "cwv3")  

### Word Similarity Results  
- Spearman's rank correlation on various word similarity datasets (6.2 Million Vocabulary size.)  

|  | FastText | Skep-Gram | Glove | Our(sub) | Our(word) |  
|--|--|--|--|--|--|  
|MTurk-287|62.46|63.38|60.77|64.33|67.22|  

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgxNTk2NzIzLDg5OTc4MDc3OF19
-->