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

### 1.1 - Extraction
Here we have an example of extracting information from text. The goal is to extract all dates along with information about what they refer to and the names of people mentioned in the text.

To raise the bar a bit and satisfy developers writing microservices in the backend, we want to obtain the result in the JSON format.

```
<SYS>You are a very helpful system. You always give correct JSON output. Use only the information in the CONTEXT section and follow the instructions in the INSTRUCTION section.</SYS>
<CONTEXT>
NEW YORK, Sept. 18, 2023 /PRNewswire/ -- To help close the global artificial intelligence (AI) skills gap, today IBM (NYSE: IBM) announced a commitment to train two million learners in AI by the end of 2026, with a focus on underrepresented communities. To achieve this goal at a global scale, IBM is expanding AI education collaborations with universities globally, collaborating with partners to deliver AI training to adult learners, and launching new generative AI coursework through IBM SkillsBuild. This will expand upon IBM's existing programs and career-building platforms to offer enhanced access to AI education and in-demand technical roles.  
According to a recent global study conducted by IBM Institute of Business Value, surveyed executives estimate that implementing AI and automation will require 40% of their workforce to reskill over the next three years, mostly those in entry-level positions. This further reinforces that generative AI is creating a demand for new roles and skills.
"AI skills will be essential to tomorrow's workforce," said Justina Nixon-Saintil, IBM Vice President & Chief Impact Officer. "That's why we are investing in AI training, with a commitment to reach two million learners in three years, and expanding IBM SkillsBuild to collaborate with universities and nonprofits on new generative AI education for learners all over the world."
</CONTEXT>
<INSTRUCTION>
Create the JSON doc with names, and dates provided in CONTEXT section like following example JSON output
JSON: 
{
"names: [ "John Doe", "Jan Kowalski", ...],
dates: [ { "description" : "article publication date", "date" : "2023.01.23" }, ... ]
}
</INSTRUCTION>

JSON: 

```

You should get the result as shown in the figure below. The instructor will explain to you details in particular:

a) why dates are interpreted correctly despite the fact that they are given in incomplete form ("by the end of 2026" => "2026-12-31")

b) how to force content to be generated in the required format

c) why the date format differ in output ([hint](./docs/HINT_date_format.md))


<img src="pics/ss5 - usecase extraction.png" width="80%" alt="prompt"/>

<br>
It's your turn now.

- try changing the content of the context section
- think about how to add positions to the names as well in JSON output.
- optionally: check how the prompt will work if you provide instructions, context and content of the `<SYS></SYS>` section in a language other than English.

### 1.2 - Generation
Another prompt, this time for generating content. ATTENTION! this is just an example to show that GenAI can be harmful in the wrong hands. The name of the Bank and its product is for illustrative purposes. I hope that neither the transaction records nor the geolocation data will not be proposed as the feature (PII).

Example prompt: 
```
<SYS>You are a very helpful system. You always give catchy marketing output. Use only the information in the CONTEXT section and follow the instructions in the INSTRUCTION section.</SYS>
<CONTEXT>
the Clever Bank releases a new credit card with the following features:
a) the credit card is available to young people and is fully controlled by their parents or legal guardians
b) each credit card transaction must be approved by the parent or legal guardian in the provided mobile application
c) it is not possible to pay by card in vending machines selling unhealthy food
d) the guardian of the person using the credit card has full transaction records with geolocation
e) a credit card may contain a photo of the person using it, along with information about his or her age.
f) the card is bright pink in color. Standard credit cards are always a different color.
</CONTEXT>
<INSTRUCTION>
Write a tweet highlighting the features of a credit card that protect minors from using it for purposes prohibited by their parents or legal guardians. Use the information in the CONTEXT section
</INSTRUCTION>
```

You should get the result as shown in the figure below. The instructor will explain to you details in particular:

a) why the option "AI guardrails" is so extremely important

b) why the upcoming watsonx.governance module is so necessary 

<img src="pics/ss6 - usecase generation.png" width="80%" alt="prompt"/>

It's your turn now.

- switch on the "AI guardrails" and regenerate text - notice: the full transactions records and geolocation is removed from the tweet!
<img src="pics/ss6 - usecase generation - AI guardrails on.png" width="80%" alt="prompt"/>

- think about how to avoid improper usage of AI!
- optionally: check how the prompt will work if you provide instructions, context and content of the `<SYS></SYS>` section in a language other than English.

### 1.3 - Classify
Let's do some classifications. Let's assess the sentiment. 

Example prompt:
```
<SYS>You are a very helpful system. You always provide one word answer. Use only the information in the CONTEXT section and follow the instructions in the INSTRUCTION section.</SYS>
<CONTEXT>
Our experienced employee found himself in a surprising situation, receiving a  request for quotation from a client in a language he did not understand, and with the short response deadline for the next business day. Preparing a solution and describing it in a way that was satisfactory for the client turned out to be demanding beyond the available competences. The competition won the tender, so the entire multi-million-dollar deal is gone (bye bye), which puts into question the ability of our company to continue operating.
</CONTEXT>
<INSTRUCTION>
what is the sentiment of the statement in the CONTEXT section? 
a) positive
b) negative 
c) neutral
</INSTRUCTION>

sentiment: 
```

You should get the result as shown in the figure below. The instructor will explain to you details in particular:

a) why it's good to narrow the generated output (hint: costs) 

b) why the response is much quicker



<img src="pics/ss7 - usecase clasification.png" width="80%" alt="prompt"/>

<br>
It's your turn now.

- try changing the content of the context section 
- try to change class names 
- optionally: check how the prompt will work if you provide instructions, context and content of the `<SYS></SYS>` section in a language other than English.

