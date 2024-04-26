# SuperRAG

This repo is intended to demonstrate how to leverage Azure OpenAI as a reranking layer in the RAG pattern to improve the accuracy of the retrieved search resuts.

## Why SuperRAG?

Hybrid and Vector retrieval approaches are typically very good at helping to retrieve content semantically similar to the users question, however they are not typically great at identifying the intent of the users question and prioritizing content retrievaly that best matches the intent of the question. SuperRAG intends to solve this by leveraging Azure OpenAI's ability to understand intent and help to rerank results that best match the intent.

## Semantics vs Intent

The semantics of a question refer to the meaning or the interpretation of the words and phrases within the question. It's about understanding what the question is asking on a linguistic level, considering the vocabulary, grammar, and structure. Semantics focuses on the literal meaning conveyed by the elements of the question. 

The intent of a question, on the other hand, goes beyond the literal meaning to understand the purpose or the reason why the question is being asked. It's about grasping what the asker is looking for or hoping to achieve with the question. 

### Example
Take the following example a user might ask:

```
Question: "Where's a good place to eat around here?"
```

From with the following content might be retrieved from the Hybrid or Vector database:
```
Doc1: There are many places to eat in this city.
Doc2: If you're in the mood for Italian, Mario's on 5th Street is fantastic. Their pasta is the best in town, and they have a lovely atmosphere
```

Doc1 matches the *semantics* of question with words like “Eat” and “Around here” being semantically similar to “this city”, but Doc2 is better because it matches the *intent* of the question.

## Azure OpenAI and Intent

Let's now look at how we can potentially use Azure OpenAI to help with the intent matching. Using Azure AI Studio we can see in this image how a simple prompt can be used to not only find the likelihood (confidence) that the response matched the intent, but also generate a reason why.

 ![image](https://github.com/liamca/superrag/assets/3432973/868ce37c-5f28-4c36-bf1c-efa1d816bb17)

 Here is a good starting point for a prompt. You will likely need to adjust based on your own needs.

```
I am going to supply you with a set of potential answers and your goal is to determine which of them is best able to answer the question:
""" +  question + """
Please respond in JSON format with a "confidence" score for each example indicating your confidence the text answers the question as well as the "id" of the text.  
Include a field called "relevent_text" which includes the text that is relevent to being able to answer the question.  
Each example will include an answer id as well as the text for the potential answer, separated by a colon.
```

## Architecture

The following diagram outlines the architectural flow.
![image](https://github.com/liamca/superrag/assets/3432973/18b08c1a-e7c3-430c-9ddd-91f4e7494685)


