# Email Response Project
Zhuoyi Zhan, Sovann Chang, Dara Kuno

## Overview	
**Prompt Engineering**, also known as **In-Context Prompting**, refers to methods for how to communicate with LLMs to steer its behavior for desired outcomes without updating the model weights. It is an empirical science and the effect of prompt engineering methods can vary a lot among models, thus requiring heavy experimentation and heuristics.

**LangChain** is a tool that allows answering questions over specific documents by only utilizing the information in those documents to construct an answer. The following steps are involved in the process:


## Task
Create a Q&A solution to craft emails from Data Science Undergraduate students on behalf of the Data Science Institute.  The goal is to feed emails into a model, use prompt engineering to craft a response, and send the results back to the DSI.  Either the model finds the correct answer and drafts the appropriate response, or, it tells the DSI that further review is needed.


## Implementation
**Lang Chain**
1. Load the document into memory.
2. Split the document into smaller chunks of text using the "CharacterTextSplitter" class from the "text_splitter" module.
3. Compute embeddings (i.e., vector representations) of the text chunks using the "HuggingFaceEmbeddings" class from the "embeddings" module.
4. Build an index of the embeddings using the "FAISS" class from the "vectorstores" module, allowing for efficient similarity search.
5. Find the most similar text chunks to a given query using the index and print the content of the top-ranked chunk.

**ChatGPT**
1.  Select 4 generative models to test.
2.  Try various methods of prompting to find best result.  This can include step-by-step prompting or batch prompting using various context, tone and direction.
3.  Select the top 2 models based on accuracy and fine tune.
4.  Couple this with the results from Lang Chain to produce final result. 


## Prompt Engineering Approaches and Observations
**First approach:** provide each chatbot with a few questions of context to test performance. Use synthetic emails to fit the questions. 

> **Bing Chat:**
Struggled to obtain the right information and hallucinations were present.
Fine tuning ultimately led to the conclusion Bing cannot access or use specific links. 

![image](https://user-images.githubusercontent.com/59686399/233250654-542d400e-4b9f-4fde-93b4-00d1e0a8a8e0.png)
<br>

> **ChatGPT:**
[Link](https://poe.com/s/dx8Nep1p8GQviwy8S7rZ)

Note: Sage performed very similarly to ChatGPT

<br>

> **Claude:**
[Link](https://poe.com/s/2bVVKW3rn9qgmfS7bbTq)

<br>

**Second approach:** test AI performance on emails not directly specified on the FAQ page.  Use only the top two performing GPTs -- ChatGPT and Sage.  The instructions stated that if the answer to the email’s question couldn’t be found in the FAQs, the chatbot should respond that it cannot answer the question.

> **ChatGPT:**
[Link](https://poe.com/s/fhZP7avLBdmoFy3VWwMD)

> **Sage:**
[Link](https://poe.com/s/DMrg9Ca6vIBk5TpXkujO)

<br>

**Third approach:** test all FAQs as context. Ultimately, Poe cannot handle the entire text of the FAQ page; it crashes and reloads to the period before the message was sent. ChatGPT's website, on the other hand, does not succumb to this limitation. According to the site, ChatGPT should support ~4096 tokens of context at once, which is around 3000 words. The entire FAQ page is ~1500 words.

**Example with Fine Tuning** 
> Upload the FAQs and asking for a one-sentence summary of each answer with subsequent prompts:
[Link](https://sharegpt.com/c/dYfys52)

<br>

> This result shows that the GPT goes beyond the scope of the FAQs.  In the next step, intruct the GPT more explicitly to only use the provided FAQs as context -- and no other information:
[Link](https://sharegpt.com/c/FAfZoKK)
[Link](https://sharegpt.com/c/j1gpAmy)

<br>

> It appeared to know its task, but forgot it after the long message with the FAQs. This insight requires further testing:
[Link](https://sharegpt.com/c/n8Soce0)
[Link](https://sharegpt.com/c/3EG6Fri)

<br>

Although ChatGPT claims to be able to handle long contexts, the long context message appears to reset it such that everything from the chat that happened before the message is forgotten!

<br>

**Fourth Approach:** Try a straight forward approach with a general outline and subsequent prompts.  After about 7 attempts, the first potential solution is reached.

<img width="499" alt="image" src="https://user-images.githubusercontent.com/71733399/233374141-9e627718-8447-479b-947e-cf4a6b8f6d49.png">

<img width="517" alt="image" src="https://user-images.githubusercontent.com/71733399/233373799-c7084141-7684-46ca-adae-e64b191eee5d.png">

<br>

**Fifth Approach:** Ask the AI how it wants to be directed. Determine what information ChatGPT needs and then slowly feed it into the prompt. The prompt starts with the request and asking the AI to provide information it would need to complete the task.  Providing the FAQs with answers led the AI to repeat these back in one long email word-for-word.  Subsequent prompting leads to the preferred format but because it cannot access the internet, the content is outdated.
[Link](https://docs.google.com/document/d/1x89t2VrNO85YjO_DLuEuel7O_QYhlF9IGQq6BwJivGQ/edit?usp=sharing)

<img width="582" alt="image" src="https://user-images.githubusercontent.com/71733399/233377658-f6e5a76d-d402-4a71-ad29-4b1eb6d57201.png">

<br>

**Sixth Approach:** Ask the AI to generate its own prompts.  Like previous attempts, ChatGPT admits feeeding the FAQs into the prompt will not improve performance.  But, with prompting the prompt, the AI can arrive at a format and tone that is acceptable to the project requirements.  This approach could work with Lang Chain where Lang Chain finds the closest match and then that response is fed into a batch prompt with minimal fine tuning to produce the needed email.
[Link](https://docs.google.com/document/d/1N21yo0AoQlAfFhjsT_EzQnCXXHCR-0TR3lz8o_fpgTY/edit?usp=sharing)

![image](https://user-images.githubusercontent.com/71733399/233380831-aa7e83c9-b4c4-47df-95a2-d3bcfeb5319e.png)


<img width="1040" alt="image" src="https://user-images.githubusercontent.com/71733399/233381525-437451c0-f511-40c8-b692-63c85e9df16e.png">

** LangChain
[notebook implementation 


## Final Conclusions 

**Generative Models:**
| Low Accuracy | Medium Accuracy | High Accuracy |
| -------- | -------- | -------- |
| Bing GPT   | Sage   | ChatGPT 
| Claude |

**Lang Chain:**
- Strong Results: Occurs when you have keywords from the FAQ page directly in the question.
- Weak Results: Because it is a similarity search, if the keywords are not specifically in the text, results drop dramatically.

**ChatGPT:** 
 * Use small prompts 
 * Use less context
 * Use a conversational tone and reinforcement (treat it like the human it was trained to be!)
 * Ask for directions 

ChatGPT responds best to a more conversational tone with instructions split into small segments. This is similar to how a human often responds best to a complex problem: break it onto small pieces to arrrive at the final answer. 

## Suggested Approach
Combine lang chain and chatGPT to create the best output.  Lang Chain will reduce the input length which significantly improves chatGPT.  Then, ChatGPT can help determine if the similarity approach is accurate and it could potentially find related words that Lang Chain could not.  Finally, ChatGPT can create the response email that either yields an appropriate response or tells the user that further research is needed as it is outside the scope of the FAQ page.


## Critical Analysis

**Project Impact:**
-  After incorporating LangChain with ChatGPT API and expanding the frequently asked question list, we can build an application to automatically generate email responses for replying emails on inquiring about data science minor. It can be applied to any question answering settings with user-provided text.

**Project Revelations:**
- The technology is not yet as adept to this specific task without further prompting.  This leads to some difficulty creating Q&A email responses solely from a GPT.  Also, because ChatGPT was trained on older data and does not access the internet, an up-to-date FAQ page would need to be provided.  This goes for Lang Chain as well.  Lang Chain can provide accurate results but needs to be fed into ChatGPT to vary the answers and draft the email responses.

**Next step(s):**
- Build an application to connect with OpenAI API to directly pass the email question and relevant documents to GPT-3 to generate a final answer.
Expand the frequently asked question list with AI-generated results


## Resource links
- [Prompt Engineering Guide](https://github.com/dair-ai/Prompt-Engineering-Guide)
- [JailBreak Chat](https://www.jailbreakchat.com/)
- [Lang Chain Notebook](https://github.com/hwchase17/langchain)
- [Lang Chain Tutorial](https://www.python-engineer.com/posts/langchain-crash-course/)
	
