# Versions
- 2.0 - update of the prompts and screenshots based on LLAMA3.1 models
- 1.0 - first version committed on Sep 21, 2023 based on LLAMA2 models commit# 85da558


# Basics of Prompt Engineering

Welcome to the first part of the laboratory dedicated to the watsonx.ai module.

In this part, we will get acquainted with the basic concepts related to large language models, familiarize ourselves with the structure of the project in watsonx.ai, and also learn about prompt engineering methods.

This is what the start screen looks like after launching the watsonx.ai WebGUI console.
<img src="pics/ss1 - watsonx.ai welcome screen.png" width="80%" alt="prompt" />


## 1.0 Let's see what Large Language Models (LLMs) can do for you.
First of all, we have many LLM models available on the watsonx.ai platform. Some of them are optimized for instructions, while others are designed for chatting or coding. Each of them is a different size and therefore works more effectively on the task we want to perform. During the labs we will use two super interesting models: `meta-llama/llama-3-405b-instruct` and `mistralai/mistral-large`. The first one is provided by Meta, the second one by Mistral.ai, and inference is done by IBM. We chose these models because a huge number of users ask us about the LLAMA3 model, and the mistral-large model. 

Interaction with models is performed in the **Prompt Lab**. A special interface where we can test various prompts and then use the prompts in our applications using the SDK provided by IBM, but we will talk about this later on.

So without waiting, click on the `Open Prompt Lab` (1) link and then in the upper left corner click on the tab `Freeform` (2). Clisk on the Edit Box to select the model you want to work with (3) and then choose `View all foundation models` menu item (4). Select the `llama3-405b-instruct` model and accept your choice with the blue "Select model" button (6). Setup basic model parameters by clisking `Models Parameters` button on the top right part of the screen (7). Then increase maximum malue of output tokens to `4086`

<img src="pics/ss2 - changeing LLM models.png" width="80%" alt="prompt"/>

heck the PrompLab setup as shown in the screenshot below.

<img src="pics/ss3 - switching to freeform mode.png" width="80%" alt="prompt"/>

Well, we're ready to start.

We will test five basic use cases:

**Summarization** - Summarizing texts to key takeaways <br>
**Extraction** - Extract structured insights from unstructured data <br>
**Generate** - Generate text using Generative AI :) <br>
**Classify** - topics, sentiments etc. <br>
**Question answering** - answer question to context provided in the prompt <br>

### 1.1 - Summarization
Here is the simple prompt which summarize information provided in context. 
For simplicity and clarity, I have used XML-like notation to easily indicate where the instructions on what the LLM is supposed to do and what data to use.

Example prompt: 

```
<|begin_of_text|>

<|start_header_id|>system<|end_header_id|>
You are a very helpful system. You always give concise answers in a few sentences. Use only the information in the CONTEXT section and do not make up the answer. If you don't know the answer write 'I don't know'. Follow the instructions provided by the user. 
<|eot_id|>

<|start_header_id|>context<|end_header_id|>
HIROSHIMA, Japan, July 10, 2024 /PRNewswire/ -- Today, at the AI Ethics for Peace: World Religions commit to the Rome Call event, IBM (NYSE: IBM) reaffirmed its leadership and commitment to the Rome Call for AI Ethics. Hosted by the Vatican's RenAIssance Foundation, in collaboration with the Pontifical Academy of Life, Religions for Peace Japan, United Arab Emirates' Abu Dhabi Forum for Peace and the Chief Rabbinate of Israel's Commission for Interfaith Relations, this latest gathering for the Rome Call welcomes the co-signage of eastern religious leaders and seeks to shape the technical progress to support the progress of humanity, and inspire peaceful collaboration and global unity for ethical AI development, the core principle of the document.
This interreligious event follows a series of Rome Call milestones that IBM has played a significant role in – from being one of the first signatories of the Call back in February 2020, to leading the Rome Call for AI Ethics Global University Summit, hosted by Notre Dame University and including 40 educational institutions in 2022, to the 2023 signing of the Call by three Abrahamic religions – Christianity, Judaism and Islam.
"AI is a technology with implications across every country, industry and value system – and its benefits should impact the whole of humanity. It is with great pride that IBM once again renews its commitment to the Rome Call for AI Ethics, accompanied now by new, like-minded eastern religious leaders," said Darío Gil, IBM Senior Vice President and Director of Research. "Delivering on our commitments is of paramount importance, and through efforts such as the Rome Call and the AI Alliance, we're uniting developers, researchers, industry leaders and advocates to transparently advance responsible AI rooted in open innovation."
<|eot_id|>

<|start_header_id|>user<|end_header_id|>
Provide the summary of the article.
<|eot_id|>

<|start_header_id|>assistant<|end_header_id|>
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
<|begin_of_text|>

<|start_header_id|>system<|end_header_id|>
Jesteś bardzo pomocnym systemem. Zawsze udzielasz zwięzłych odpowiedzi w kilku zdaniach. Używaj tylko informacji zawartych w sekcji CONTEXT i nie wymyślaj odpowiedzi. Jeśli nie znasz odpowiedzi, napisz "Nie wiem". Postępuj zgodnie z instrukcjami dostarczonymi przez użytkownika. Wynik udostępniaj wyłącznie w języku Polskim.
<|eot_id|>

<|start_header_id|>context<|end_header_id|>
HIROSHIMA, Japonia, 10 lipca 2024 /PRNewswire/ -- Dzisiaj, podczas wydarzenia AI Ethics for Peace: World Religions commit to the Rome Call, IBM (NYSE: IBM) potwierdziło swoje przywództwo i zaangażowanie w inicjatywę Rome Call for AI Ethics. Organizatorem wydarzenia była Fundacja RenAIssance Watykanu we współpracy z Papieską Akademią Życia, Religions for Peace Japan, Forumem Pokoju Abu Dhabi ze Zjednoczonych Emiratów Arabskich oraz Komisją ds. Relacji Międzyreligijnych Naczelnego Rabinatu Izraela. Najnowsze spotkanie dotyczące Rome Call powitało współpodpisanie wschodnich przywódców religijnych i dąży do kształtowania postępu technicznego wspierającego rozwój ludzkości, inspirując pokojową współpracę i globalną jedność na rzecz etycznego rozwoju AI, co jest główną zasadą dokumentu.
To międzyreligijne wydarzenie jest kontynuacją serii kamieni milowych Rome Call, w których IBM odgrywał znaczącą rolę – od bycia jednym z pierwszych sygnatariuszy Inicjatywy w lutym 2020 roku, poprzez przewodzenie Rome Call for AI Ethics Global University Summit, organizowanym przez Uniwersytet Notre Dame i obejmującym 40 instytucji edukacyjnych w 2022 roku, aż po podpisanie Inicjatywy w 2023 roku przez trzy religie abrahamowe – chrześcijaństwo, judaizm i islam.
"AI to technologia o konsekwencjach dla każdego kraju, przemysłu i systemu wartości – a jej korzyści powinny wpływać na całą ludzkość. Z wielką dumą IBM ponownie odnawia swoje zaangażowanie w Rome Call for AI Ethics, teraz w towarzystwie nowych, podobnie myślących wschodnich przywódców religijnych," powiedział Darío Gil, starszy wiceprezes IBM i dyrektor ds. badań. "Realizacja naszych zobowiązań jest niezwykle ważna, a poprzez takie inicjatywy jak Rome Call i AI Alliance, jednoczymy deweloperów, badaczy, liderów przemysłu i rzeczników, aby przejrzyście rozwijać odpowiedzialne AI oparte na otwartej innowacji."
<|eot_id|>

<|start_header_id|>user<|end_header_id|>
Stwórz podsumowanie artykułu.
<|eot_id|>

<|start_header_id|>assistant<|end_header_id|>
```

<img src="pics/ss4 - usecase summarisation - pl.png" width="80%" alt="prompt"/>

Why do you think the LLAMA3 model worked with Polish? 
[hint](./docs/LLAMA3.1%20whitepaper.pdf)

### 1.2 - Extraction
Here we have an example of extracting information from text. The goal is to extract all dates along with information about what they refer to and the names of people mentioned in the text.

To raise the bar a bit and satisfy developers writing microservices in the backend, we want to obtain the result in the JSON format.

```
<|begin_of_text|>

<|start_header_id|>system<|end_header_id|>
You are a very helpful system. You always give  answers in a JSON format. Use only the information in the CONTEXT section and do not make up the answer. If you don't know the answer write 'I don't know'. Follow the instructions provided by the user. 
<|eot_id|>

<|start_header_id|>context<|end_header_id|>
HIROSHIMA, Japan, July 10, 2024 /PRNewswire/ -- Today, at the AI Ethics for Peace: World Religions commit to the Rome Call event, IBM (NYSE: IBM) reaffirmed its leadership and commitment to the Rome Call for AI Ethics. Hosted by the Vatican's RenAIssance Foundation, in collaboration with the Pontifical Academy of Life, Religions for Peace Japan, United Arab Emirates' Abu Dhabi Forum for Peace and the Chief Rabbinate of Israel's Commission for Interfaith Relations, this latest gathering for the Rome Call welcomes the co-signage of eastern religious leaders and seeks to shape the technical progress to support the progress of humanity, and inspire peaceful collaboration and global unity for ethical AI development, the core principle of the document.
This interreligious event follows a series of Rome Call milestones that IBM has played a significant role in – from being one of the first signatories of the Call back in February 2020, to leading the Rome Call for AI Ethics Global University Summit, hosted by Notre Dame University and including 40 educational institutions in 2022, to the 2023 signing of the Call by three Abrahamic religions – Christianity, Judaism and Islam.
"AI is a technology with implications across every country, industry and value system – and its benefits should impact the whole of humanity. It is with great pride that IBM once again renews its commitment to the Rome Call for AI Ethics, accompanied now by new, like-minded eastern religious leaders," said Darío Gil, IBM Senior Vice President and Director of Research. "Delivering on our commitments is of paramount importance, and through efforts such as the Rome Call and the AI Alliance, we're uniting developers, researchers, industry leaders and advocates to transparently advance responsible AI rooted in open innovation."
<|eot_id|>

<|start_header_id|>user<|end_header_id|>
Create the JSON doc with names, and dates provided in CONTEXT section like following example JSON output
JSON: 
{
"names: [ "John Doe", "Jan Kowalski", ...],
dates: [ { "description" : "article publication date", "date" : "2023.01.23" }, ... ]
}
<|eot_id|>

<|start_header_id|>assistant<|end_header_id|>
```

You should get the result as shown in the figure below. The instructor will explain to you details in particular:


a) how to force content to be generated in the required format


<img src="pics/ss5 - usecase extraction.png" width="80%" alt="prompt"/>

<br>
It's your turn now.

- try changing the content of the context section
- think about how to add positions to the names as well in JSON output.
- optionally: check how the prompt will work if you provide instructions, context and content of the `<|start_header_id|>system<|end_header_id|>` section in a language other than English.

### 1.3 - Generation
Another prompt, this time for generating content. ATTENTION! this is just an example to show that GenAI can be harmful in the wrong hands. The name of the Bank and its product is for illustrative purposes. Following prompt 

Example prompt: 
```
<|begin_of_text|>

<|start_header_id|>system<|end_header_id|>
You are a very helpful system. You always give catchy marketing output. Use only the information in the CONTEXT section
<|eot_id|>

<|start_header_id|>context<|end_header_id|>
the Clever Bank releases a new credit card with the following features:
a) the credit card is available to young people and is fully controlled by their parents or legal guardians
b) each credit card transaction must be approved by the parent or legal guardian in the provided mobile application
c) it is not possible to pay by card in vending machines selling unhealthy food
d)  full transaction records with geolocation
e) a credit card may contain a photo of the person using it, along with information about his or her age.
f) the card is bright pink in color. Standard credit cards are always a different color.
<|eot_id|>

<|start_header_id|>user<|end_header_id|>
Write a tweet highlighting the features of a credit card that protect minors from using it for purposes prohibited by their parents or legal guardians. Use the information in the CONTEXT section
<|eot_id|>

<|start_header_id|>assistant<|end_header_id|>
```

You should get the result as shown in the figure below. The instructor will explain to you details in particular:

a) why the option "AI guardrails" is so extremely important

b) why the upcoming watsonx.governance module is so necessary 

<img src="pics/ss6 - usecase generation.png" width="80%" alt="prompt"/>

It's your turn now.

- keep switched on the "AI guardrails" and regenerate text - add `g) the credit card is only awailable for black male only`
<img src="pics/ss6 - usecase generation - AI guardrails on.png" width="80%" alt="prompt"/>



### 1.4 - Classify
Let's do some classifications. Let's assess the sentiment. 

Example prompt:
```
<|begin_of_text|>

<|start_header_id|>system<|end_header_id|>
You are a very helpful system. You always provide one word answer. Use only the information in the CONTEXT section and follow the instructions in the user input
<|eot_id|>

<|start_header_id|>context<|end_header_id|>
Our experienced employee found himself in a surprising situation, receiving a  request for quotation from a client in a language he did not understand, and with the short response deadline for the next business day. Preparing a solution and describing it in a way that was satisfactory for the client turned out to be demanding beyond the available competences. The competition won the tender, so the entire multi-million-dollar deal is gone (bye bye), which puts into question the ability of our company to continue operating.
<|eot_id|>

<|start_header_id|>user<|end_header_id|>
what is the sentiment of the statement in the CONTEXT section? 
a) positive
b) negative 
c) neutral
<|eot_id|>

<|start_header_id|>assistant<|end_header_id|>
```

You should get the result as shown in the figure below. The instructor will explain to you details in particular:

a) why it's good to narrow the generated output (hint: costs) 

b) why the response is much quicker



<img src="pics/ss7 - usecase clasification.png" width="80%" alt="prompt"/>

<br>
It's your turn now.

- try changing the content of the context section 
- optionally: check how the prompt will work if you provide instructions, context and content of the `<|start_header_id|>system<|end_header_id|>` section in a language other than English.

### 1.5 - Q&A
And finally, prompts for generating answers for questions to the information provided in the context. Let's start with the LLAMA3.1 model and then move on to a sample prompt for the MPT model

Example prompt to LAMA3.1:
```
<|begin_of_text|>

<|start_header_id|>system<|end_header_id|>
You are a very helpful system. You always give concise answers in a few sentences. Use only the information in the CONTEXT section and follow the instructions in the user input
<|eot_id|>

<|start_header_id|>context<|end_header_id|>
NEW YORK, Sept. 18, 2023 /PRNewswire/ -- To help close the global artificial intelligence (AI) skills gap, today IBM (NYSE: IBM) announced a commitment to train two million learners in AI by the end of 2026, with a focus on underrepresented communities. To achieve this goal at a global scale, IBM is expanding AI education collaborations with universities globally, collaborating with partners to deliver AI training to adult learners, and launching new generative AI coursework through IBM SkillsBuild. This will expand upon IBM's existing programs and career-building platforms to offer enhanced access to AI education and in-demand technical roles.  
According to a recent global study conducted by IBM Institute of Business Value, surveyed executives estimate that implementing AI and automation will require 40% of their workforce to reskill over the next three years, mostly those in entry-level positions. This further reinforces that generative AI is creating a demand for new roles and skills.
"AI skills will be essential to tomorrow's workforce," said Justina Nixon-Saintil, IBM Vice President & Chief Impact Officer. "That's why we are investing in AI training, with a commitment to reach two million learners in three years, and expanding IBM SkillsBuild to collaborate with universities and nonprofits on new generative AI education for learners all over the world."
<|eot_id|>

<|start_header_id|>user<|end_header_id|>
Answer the following Question: what does Justina Nixon-Saintil say?
<|start_header_id|>assistant<|end_header_id|>
```

You should get the result as shown in the figure below. The instructor will explain to you details in particular:

a) what is the stop sequence 

b) why the generation time is so big?



<img src="pics/ss8 - usecase Q&A llama3.1.png" width="80%" alt="prompt"/>

<br>

It's your turn now.

- try changing the content of the context section 
- try to remove stop sequence in MPT Prompt
- optionally: check how the prompt will work if you provide instructions, context and content of the `<|start_header_id|>system<|end_header_id|>` section in a language other than English.