# Email Response Project
Zhuoyi Zhan, Sovann Chang, Dara Kuno

## Overview	
**Prompt Engineering**, also known as **In-Context Prompting**, refers to methods for how to communicate with LLMs to steer its behavior for desired outcomes without updating the model weights. It is an empirical science and the effect of prompt engineering methods can vary a lot among models, thus requiring heavy experimentation and heuristics.

**LangChain** is a tool that allows answering questions over specific documents by only utilizing the information in those documents to construct an answer. The following steps are involved in the process:

## Task

We want to create a Q&A solution to craft emails from Data Science Undergraduate students on behalf of the Data Science Institute.  The goal is to feed emails into a model, use prompt engineering to craft a response, and send the results back to the DSI.  Either the model finds the correct answer and drafts the appropriate response, or, it tells the DSI that further research is needed.

## Implementation
First idea - give each potential chatbot a few questions of context and see how they performed on those. Use emails that we made up to fit the questions. 

**Bing Chat:**
Seemed to have trouble getting the right information. Hallucinated and made up things that didn’t exist.
An attempt to fix it led us to realize that we can't direct it towards a specific link.

![image](https://user-images.githubusercontent.com/59686399/233250654-542d400e-4b9f-4fde-93b4-00d1e0a8a8e0.png)
<br>

**ChatGPT:**
https://poe.com/s/dx8Nep1p8GQviwy8S7rZ

Note: Sage performed very similarly to ChatGPT

<br>

**Claude:**
https://poe.com/s/2bVVKW3rn9qgmfS7bbTq

<br>

We decided to move forward with the two best models: ChatGPT and Sage. To test its performance on emails that aren't answered by the FAQs, we made it clear that if the answer to the email’s question couldn’t be found in the FAQs, the chatbot should respond that it cannot answer the question.

**ChatGPT:**
https://poe.com/s/fhZP7avLBdmoFy3VWwMD

**Sage:**
https://poe.com/s/DMrg9Ca6vIBk5TpXkujO

<br>

### Testing all FAQs as context

We discovered that Poe cannot handle the entire text of the FAQ page; it crashes and reloads to before the message was sent. Instead, we migrated to ChatGPT's website. ChatGPT was supposed to support up to 4096 tokens of context at the time, which is around 3000 words. The entire FAQ page is ~1500 words, so it should easily fit.
<br><br>
We uploaded the FAQs and ask for a one-sentence summary of each answer:

https://sharegpt.com/c/dYfys52

<br>

This is weird - was ChatGPT confusing itself by trying to pull other FAQs as context? We instructed it more explicitly to only use the provided FAQs as context - no other information:

https://sharegpt.com/c/FAfZoKK

https://sharegpt.com/c/j1gpAmy

<br>

It appeared to know its task, but forgot it after the long message with the FAQs. To take this to the extreme, we ran two more tests:

https://sharegpt.com/c/n8Soce0

https://sharegpt.com/c/3EG6Fri

<br>

This is proof of a very weird concept - although ChatGPT claims to be able to handle long contexts, the long context message appears to sort of reset it, such that it forgets everything from the chat that happened before the message!

<br><br><br>

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
| Bing GPT   | Sage   | ChatGPT 
| Claude |

**ChatGPT:** 
 * Informal, casual language works best
 * Small prompts and less context also yield the best results
 * A conversational tone yields the best results (treat it like the human it was trained to be!)

**Lang Chain:**
- Strong Results: Occurs when you have keywords from the FAQ page directly in the question.
- Weak Results: Because it is a similarity search, if the keywords are not specifically in the text, results drop dramatically.

## Suggested Approach
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
