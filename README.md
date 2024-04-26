# SuperRAG

This repo is intended to demonstrate how to leverage Azure OpenAI as a reranking layer in the RAG pattern to improve the accuracy of the retrieved search resuts.

##Why SuperRAG?

Hybrid and Vector retrieval approaches are typically very good at helping to retrieve content semantically similar to the users question, however they are not typically great at identifying the intent of the users question and prioritizing content retrievaly that best matches the intent of the question. SuperRAG intends to solve this by leveraging Azure OpenAI's ability to understand intent and help to rerank results that best match the intent.

##Semantics vs Intent

The semantics of a question refer to the meaning or the interpretation of the words and phrases within the question. It's about understanding what the question is asking on a linguistic level, considering the vocabulary, grammar, and structure. Semantics focuses on the literal meaning conveyed by the elements of the question. 

The intent of a question, on the other hand, goes beyond the literal meaning to understand the purpose or the reason why the question is being asked. It's about grasping what the asker is looking for or hoping to achieve with the question. 

###Example
Take the following example a user might ask:

```
Question: "Where's a good place to eat around here?"
```

From with the following content might be retrieved from the Hybrid or Vector database:
```
Doc1: There are many places to eat in this city.
Doc2: If you're in the mood for Italian, Mario's on 5th Street is fantastic. Their pasta is the best in town, and they have a lovely atmosphere
```

Doc1 matches the Semantic of question with words like “Eat” and “Around here” being semantically similar to “this city”, but Doc2 is better because it matches the intent of the question.

 

