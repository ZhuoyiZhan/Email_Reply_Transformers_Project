# Email Response Project
Zhuoyi Zhan, Sovann Chang, Dara Kuno

## Overview	
**Prompt Engineering**, also known as **In-Context Prompting**, refers to methods for how to communicate with LLMs to steer its behavior for desired outcomes without updating the model weights. It is an empirical science and the effect of prompt engineering methods can vary a lot among models, thus requiring heavy experimentation and heuristics.

**LangChain** is a tool that allows answering questions over specific documents by only utilizing the information in those documents to construct an answer. The following steps are involved in the process:

## Task

We want to create a Q&A solution to craft emails from Data Science Undergraduate students on behalf of the Data Science Institute.  The goal is to feed emails into a model, use prompt engineering to craft a response, and send the results back to the DSI.  Either the model finds the correct answer and drafts the appropriate response, or, it tells the DSI that further research is needed.

## Implementation
**Lang Chain**
1. Load the document into memory.
2. Split the document into smaller chunks of text using the "CharacterTextSplitter" class from the "text_splitter" module.
3. Compute embeddings (i.e., vector representations) of the text chunks using the "HuggingFaceEmbeddings" class from the "embeddings" module.
4. Build an index of the embeddings using the "FAISS" class from the "vectorstores" module, allowing for efficient similarity search.
5. Find the most similar text chunks to a given query using the index and print the content of the top-ranked chunk.

**ChatGPT**
1.  Select 4 generative models to test.
2.  Try various methods of prompting to find best result.  This can include step-by-step prompting or batch prompting using various words, phrases, tones and sentences.
3.  Select the top 2 models based on tone and accuracy and fine tune.
4.  Couple this with the results from Lang Chain to produce final result. 


## Conclusion 
**Generative Models:**
| Low Accuracy | Medium Accuracy | High Accuracy |
| -------- | -------- | -------- |
| Bing GPT   | Sage [exp1](https://poe.com/s/NdsKGQuyAjWgW3KklRnV) [exp2](https://poe.com/s/DMrg9Ca6vIBk5TpXkujO)  | ChatGPT [exp1](https://poe.com/s/dx8Nep1p8GQviwy8S7rZ) [exp2](https://poe.com/s/fhZP7avLBdmoFy3VWwMD)  |
| Claude [exp1](https://poe.com/s/2bVVKW3rn9qgmfS7bbTq) [exp2](https://poe.com/s/ZkLhjtam31IZiwnBIl34)  |   |    |

**ChatGPT:** 
 * Informal, casual language works best
 * Small prompts and less context also yield the best results
 * A conversational tone yields the best results (treat it like the human it was trained to be!)

**Lang Chain:**
- Strong Results: Occurs when you have keywords from the FAQ page directly in the question.
- Weak Results: Because it is a similarity search, if the keywords are not specifically in the text, results drop dramatically.

## Final Approach
Combine lang chain and chatGPT to create the best output.  Lang Chain will reduce the input length which significantly improves chatGPT.  Then, ChatGPT can help determine if the similarity approach is accurate and it could potentially find related words that Lang Chain could not.  Finally, ChatGPT can create the response email that either yields an appropriate response or tells the user that further research is needed as it is outside the scope of the FAQ page.

## Critical Analysis

**Project Impact:**
-  After incorporating LangChain with ChatGPT API and expanding the frequently asked question list, we can build an application to automatically generate email responses for replying emails on inquiring about data science minor. It can be applied to any question answering settings with user-provided text.

**Project Revelations:**
- The technology is not as adept.  Also, because ChatGPT cannot connect to the internet yet, an up-to-date FAQ page would need to be provided.  This goes for Lang Chain as well since you need to feed the data to the architecture.

**Next step(s):**
- Build an application to connect with OpenAI API to directly pass the email question and relevant documents to GPT-3 to generate a final answer.
Expand the frequently asked question list with AI-generated results


## Resource links
- [Prompt Engineering Guide](https://github.com/dair-ai/Prompt-Engineering-Guide)
- [JailBreak Chat](https://www.jailbreakchat.com/)
- [Lang Chain Notebook](https://github.com/hwchase17/langchain)
- [Lang Chain Tutorial](https://www.python-engineer.com/posts/langchain-crash-course/)

## Code demonstration	
