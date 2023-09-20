# Basics of Prompt Engineering

Welcome to the first part of the laboratory dedicated to the watsonx.ai module.

In this part, we will get acquainted with the basic concepts related to large language models, familiarize ourselves with the structure of the project in watsonx.ai, and also learn about prompt engineering methods.

This is what the start screen looks like after launching the watsonx.ai WebGUI.
<img src="pics/ss1 - watsonx.ai welcome screen.png" width="80%" alt="prompt" />


## 1.0 Let's see what Large Language Models (LLMs) can do for you.
First of all, we have many LLM models available on the watsonx.ai platform. Each of them is a different size and therefore works more effectively on the task we want to perform. During the labs we will use two super interesting models: `llama-2-70b-chat` and `mpt-7b-instruct2`. First one is provided by Meta, second one by Mosaic and tuned by IBM. We chose these models because a huge number of users ask us about the LLAMA2 model, and the MPT-7B-Instruct2 model is a retrained version of the original MPT-7B-Instruct model available under the `Apache 2.0 License`. Yes, we must admit the type of license does matters.

Interaction with models is performed in the **Prompt Lab**. A special interface where we can test various prompts and then use the prompts in our applications using the SDK provided by IBM, but we will talk about this later on.

So without waiting, click on the `Experiment with foundation models ...` tile and then in the upper right corner click on the edit box `model: ...`. Select the `llama-2-70b-chat` model and accept your choice with the blue "Select model" button. 

<img src="pics/ss2 - changeing LLM models.png" width="80%" alt="prompt"/>

Now, click on the tab marked in red in the figure below. The system will ask you to confirm changing the mode to "freeform", accept this choice - it will be more fun when we write prompts in raw text.

<img src="pics/ss3 - switching to freeform mode.png" width="80%" alt="prompt"/>

Well, we're ready to start.

We will test five basic use cases:

**Summarization** - Summarizing texts to key takeaways
**Extraction** - Extract structured insights from unstructured data
**Generate** - Generate text using Generative AI :) 
**Classify** - topics, sentiments etc.
**Question answering** - answer question to context provided in the prompt

### 1.1 - Summarization
Here is the simple prompt which summarize information provided in context. 
For simplicity and clarity, I have used XML-like notation to easily indicate where the instructions on what the LLM is supposed to do and what data to use.

Example prompt: 

```
<SYS>You are a very helpful system. You always give concise answers in a few sentences. Use only the information in the CONTEXT section and follow the instructions in the INSTRUCTION section.</SYS>
<CONTEXT>
NEW YORK, Sept. 18, 2023 /PRNewswire/ -- To help close the global artificial intelligence (AI) skills gap, today IBM (NYSE: IBM) announced a commitment to train two million learners in AI by the end of 2026, with a focus on underrepresented communities. To achieve this goal at a global scale, IBM is expanding AI education collaborations with universities globally, collaborating with partners to deliver AI training to adult learners, and launching new generative AI coursework through IBM SkillsBuild. This will expand upon IBM's existing programs and career-building platforms to offer enhanced access to AI education and in-demand technical roles.  
According to a recent global study conducted by IBM Institute of Business Value, surveyed executives estimate that implementing AI and automation will require 40% of their workforce to reskill over the next three years, mostly those in entry-level positions. This further reinforces that generative AI is creating a demand for new roles and skills.
"AI skills will be essential to tomorrow's workforce," said Justina Nixon-Saintil, IBM Vice President & Chief Impact Officer. "That's why we are investing in AI training, with a commitment to reach two million learners in three years, and expanding IBM SkillsBuild to collaborate with universities and nonprofits on new generative AI education for learners all over the world."
</CONTEXT>
<INSTRUCTION>
Create summary of information provided in CONTEXT section
</INSTRUCTION>

Summary:

```

You should get the result as shown in the figure below. The instructor will explain to you details in particular:

a) how the LLM output is delivered
b) how the LLM model is parameterized
c) how big the prompt can be, how big the answer will be and how long it took to generate the content.

<img src="pics/ss4 - usecase summarisation.png" width="80%" alt="prompt"/>

<br>
It's your turn now (if you have access to the watsonx.ai platform. If you don't have it, ask. Obtaining one is very simple.)

- try changing the content of the context section
- increase the amount of text for the summary
- optionally: check how the prompt will work if you provide instructions, context and content of the `<SYS></SYS>` section in a language other than English. 

for Polish language it works like this:
```
<SYS>Jesteś bardzo pomocnym systemem. Zawsze udzielasz zwięzłych odpowiedzi w kilku zdaniach. Korzystaj wyłącznie z informacji zawartych w sekcji KONTEKST i postępuj zgodnie z instrukcjami zawartymi w sekcji INSTRUKCJA.</SYS>
<KONTEKST>
NOWY JORK, 18 września 2023 r. /PRNewswire/ -- Aby pomóc w uzupełnieniu globalnej luki w umiejętnościach w zakresie sztucznej inteligencji (AI), IBM (NYSE: IBM) ogłosił dzisiaj zobowiązanie do przeszkolenia dwóch milionów uczniów w zakresie sztucznej inteligencji do końca 2026 r., przy czym chce się skupić na osobach wykluczonych. Aby osiągnąć ten cel w skali globalnej, IBM rozszerza współpracę edukacyjną dotyczącą sztucznej inteligencji z uniwersytetami na całym świecie, współpracuje z partnerami w celu zapewniania szkoleń w zakresie sztucznej inteligencji dla dorosłych uczniów oraz uruchamia nowe zajęcia z generatywnej sztucznej inteligencji w ramach IBM SkillsBuild. Stanowi to rozszerzenie istniejących programów i platform budowania kariery IBM, zapewniając lepszy dostęp do edukacji w zakresie sztucznej inteligencji. Według niedawnego globalnego badania przeprowadzonego przez IBM Institute of Business Value ankietowani menedżerowie szacują, że wdrożenie sztucznej inteligencji i automatyzacji będzie wymagało przekwalifikowania 40% ich pracowników w ciągu najbliższych trzech lat, głównie tych na stanowiskach podstawowych. To jeszcze bardziej potwierdza, że generatywna sztuczna inteligencja stwarza popyt na nowe role i umiejętności.„Umiejętności wykorzystania sztucznej inteligencji będą niezbędne dla przyszłych pracowników” – powiedziała Justina Nixon-Saintil, wiceprezes i dyrektor ds. wpływu IBM. „Dlatego inwestujemy w szkolenia w zakresie sztucznej inteligencji, zobowiązując się do dotarcia do dwóch milionów uczniów w ciągu trzech lat, a także rozwijając program IBM SkillsBuild, aby współpracować z uniwersytetami i organizacjami non-profit w zakresie nowej generatywnej edukacji w zakresie sztucznej inteligencji dla uczniów na całym świecie”.
</CONTEXT>
<INSTRUKCJA>
Utwórz podsumowanie informacji zawartych w sekcji KONTEKST
</INSTRUKCJA>

Podsumowanie: 

```

<img src="pics/ss4 - usecase summarisation - pl.png" width="80%" alt="prompt"/>

Why do you think the LLAMA2 model worked with Polish? 
[hint](./docs/Llama%202%20white%20paper.pdf)