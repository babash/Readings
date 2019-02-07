# A Semantically Enriched Context-Aware OER Recommendation Strategy and Its Applicationto a Computer Science OER Repository
## Almudena Ruiz-Iniesta, Guillermo Jiménez-Díaz, and Mercedes Gómez-Albarrán
https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=6774489
___
### Abstract
> —This paper describes a knowledge-based strategy for recommending educational resources—worked problems,exercises, quiz questions, and lecture notes—to learners in the first two courses in the introductory sequence of a computer science major (CS1 and CS2). The goal of the recommendation strategy is to provide support for personalized access to the resources that exist in open educational repositories. The strategy uses: 1) a description of the resources based on metadata standards enriched by ontology-based semantic indexing, and 2) contextual information about the user (her knowledge of that particular field of learning). The results of an experimental analysis of the strategy’s performance are presented. These demonstrate that the proposed strategy offers a high level of personalization and can be adapted to the user. An application of the strategy to a repositoryof computer science open educational resources was well received by both educators and students and had promising effects on the student performance and dropout rates.
___
### Recommendation engine

**Open ressources modeling**
The OERs are modeled using IEEE Meta-data LOM and ontologies created by expert with OWL language and validated via the OOPS! platform.
**Domain ontology**
Can be described by three main points:
1. Similarity beetween concepts
:   Recover domain concepts from ontologies validated by expert and organise them in hirearchic network capturing taxonomy between concepts;
2. Link beetween OER and concepts
:   OER are linked like with concepts depending inner concepts validated by expert;
3. Pedagogical knowledge
: Defined wht's a successfull leraning path, can capture precedance among concept (for example _has previous_, _has next_).

**User knowledge modeling**
The user knowledge is defined as a overlay in concepts.
The initial user context elicitation is achieved by asking the user directly about her mastery levels. The user kwowledge is periodically updated using quizz.

**Recomender system**
Query is made using concepts picking by the user (as 2hard4me idea). This sets of concepts represent a short term learning goal. The sytem selects then the ressources which match with the query concepts. Even if it's confuse in the article, a ressources "match" if:
- any concepts of the ressources match with the query;
- a subset of query concepts (same or similar -according to similarity-) matchs with the ressources;
Then, the selected OER concepts have to be reachable form the student knowledge. It means not already explored and reflected a minimum mastery level in the concepts that are needed to acces this OER, according to the learning paths defined in the ontology. on-tology.

Now we have to order these recommdations using a _Quality_ evaluation, the paper assumes give the priority to the OER most similar to the user query.
For an OER _R_, an user _U_, and a query _Q_
>![](https://latex.codecogs.com/gif.latex?Quality(R,&space;U,&space;Q)&space;=&space;\frac{1}{\frac{\alpha}{Sim(R,&space;Q)}&plus;\frac{1&space;-&space;\alpha}{PU(R,&space;U)}})

_Sim(R, Q)_ is the normalized cardinal of common concepts beetween _Q_ and R.
>![](https://latex.codecogs.com/gif.latex?Sim(R,&space;Q)&space;=&space;\frac{|\cup&space;Q\cap&space;\cup&space;R|}{\sqrt{|\cup&space;Q|}\sqrt{|\cup&space;R|}})

And _PU_ evaluate the pedagogcial utility of _R_ for _U_, logicaly more _U_ has a low level in the concepts of _R_ more _PU(R, U)_ growth.
>![](https://latex.codecogs.com/gif.latex?PU%28R%2C%20U%29%20%3D1%20-%20normalized%28%5Csum_%7Bc%20%5Cin%20R%7Dlevel%28U%2C%20c%29%29)

The parameter \alpha lead the trade-off between user personlized recommendation and query answering.

Finally, the k highest quality OER are returned.

### Evaluation of recommendation strategy
The normalized discounted cumulative gain (NDCG) is a metric to evaluate usefulness of a result list based on revelance and rank in list of retrieved ressource.

![](https://latex.codecogs.com/gif.latex?NDGC%28k%2C%20L%29%20%3D%20%5Cfrac%7Bscore%28L_1%29%20%5Csum_%7Bi%3D2%7D%5Ek%5Cfrac%7Bscore%28L_i%29%29%7D%7B%5Clog_2%28i%29%7D%7D%7BIDCG%28k%2C%20L%29%7D) with IDCG the NDCG of the ideal order of the list L.

