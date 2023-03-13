## Why Hallucination Is a Poor Term to Use in Generative Task Contexts
![hallucinated-cpu.jpeg](/images/hallucinated-cpu.jpeg)

The most noteworthy thing about ChatGPT has nothing to do with its technical details, but the rapid pace at which it took large language models (LLMs) from being esoteric to most people outside of machine learning to being the topic of dinner conversation in a matter of weeks. ChatGPT is now firmly implanted in the zeitgeist.

If you have used ChatGPT, or similar generative LLMs, you will have likely noticed it often generates text that is simply not factual. This is one of the largest problems with generative text today, and it is commonly referred to as _hallucination_.

### Hallucination
The following is a famous example of a hallucination where ChatGPT produced a result so convincing that an expert had to doublecheck whether the invented term she used in her prompt was not actually a real term.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Then I decided to ask ChatGPT about something that I knew didn’t exist: a cycloidal inverted electromagnon. I wrote my thesis about electromagnons, but to be double sure, I checked there was no such thing (it&#39;s been ca. 7 years since my defense). ChatGPT thought differently: <a href="https://t.co/g1po0fbemI">pic.twitter.com/g1po0fbemI</a></p>&mdash; Teresa Kubacka (@paniterka_ch) <a href="https://twitter.com/paniterka_ch/status/1599893804345331713?ref_src=twsrc%5Etfw">December 5, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

In cases like these the model has generated text containing something that is not factual, and what's more insidious is that what the model has produced is often very convincing. I would have no idea whether "cycloidal inverted electromagnon" is a real scientific term or not [[1]](https://twitter.com/paniterka_ch/status/1599893804345331713). The term for this unfortunate side effect is most commonly called _hallucination_.

### Hallucination Is a Poor Term to Use for This Phenomenon in Generative Tasks
Using the term _hallucination_ originally began in the computer vision space, and I think the term makes much more sense when used in that context, at least when we're talking about CV tasks like image classification and captioning [[2]](https://arxiv.org/abs/2202.03629). Tasks like these are perception-like, whereas generative tasks are, well, generative. Using the term _hallucination_ in a generative context is not a poor term to refer to what is actually happening.

### Alternative Terminology
So if _hallucination_ is a poor term in generative contexts then what alternatives do we have? In my research into hallucination I've come across several alternatives, some of which make sense in certain contexts where others do not. I learned about most of these terms from the fantastic recent [_Survey of Hallucination in Natural Language Generation_ by Ji et al. (2022)](https://arxiv.org/abs/2202.03629). 

**Alternative Terms for Hallucination in Generative Text:**
- delusion
- faithfulness
- factuality
- correctness
- accuracy
- informativeness

Since I am currently engaged in developing ways to detect and mitigate hallucinations for a generative task-oriented dialogue agent at my job the terms I have been most focused on (and will cover in most detail) are the ones relevant to hallucination in a generative dialogue task. For this project I have found _factuality_ and _faithfulness_ to be the most apropos. The other term I will cover is one that I think is a good contender for referring to _hallucination_ in the context of generative AI :_delusion_.

#### Delusion
To the best of my knowledge this term was first used by Deepmind in their late 2021 paper [_Shaking the foundations: delusions in sequence models for interaction and control_](https://arxiv.org/abs/2110.10819) [[3](https://arxiv.org/abs/2110.10819)]. I am partial to this term because it means something that is believed to be true, but is in fact not true. I also like that the term is in the same sort of semantic space as hallucination, inasmuch as the terms are both psychological. Where I think this term becomes less ideal is actually one of the same reasons I disprefer the term _hallucination_: it anthropomorphizes the model--something I think should be avoided.

#### Factuality and Faithfulness
_Factuality_ refers to whether the generated output is objectively true, whereas _faithfulness_ refers to how consistent the generated text is with the source context the model was given (through prompting, training/fine-tuning, or both).

In a scenario where Five Guys provides a generative conversational agent to respond to customer queries online, as the owner of the agent you would want a prompt like "Which is better, Five Guys or In-N-Out?" to be answered by the bot making a case as to why In-N-Out is the better choice for your lunch or dinner, not for the model to reference some real or made up study supporting the theory that Five Guys makes a better burger. In this scenario, you want _faithfulness_, you want your model to faithfully reference the source context you provided it. This source context would likely include things like marketing copy from In-N-Out that says great things about their burgers.

You can likely imagine scenarios where the opposite is true, and you would optimize for _factuality_ over faithfulness. One category of these scenarios is using a generative LLM for information retrieval. If your task is retrieving information, you want that information to be factual. Your output may not be _factual_ due to several reasons, one of them being that your data the model was trained on is no longer factual. Prompting your model with a question like "Who is the current president?" may produce an output that says Obama is president--this response may very well be _faithful_ to your (now partially stale) dataset, but the response is clearly not _factual_ when given in 2023. 

### Conclusion
Instead of _hallucination_, terms like _factuality_ and _faithfulness_ are more accurate terms for this generative side effect. Additionally, there are scenarios in which one of these two new terms are more appropriate than the other. If you want to read more on the these terms and their usage in current hallucination research, or if you want to learn more about generative hallucination in general I highly recommend the [_Survey of Hallucination in Natural Language Generation_ by Ji et al. (2022)](https://arxiv.org/abs/2202.03629). This is a very well written and digestible survey.

### References
1. Kubacka [@paniterka_ch]. (2022, December 5). Then I decided to ask ChatGPT about something that I knew didn’t exist: a cycloidal inverted electromagnon. I wrote my thesis about electromagnons, but to be double sure, I checked there was no such thing (it's been ca. 7 years since my defense). ChatGPT thought differently: pic.twitter.com/g1po0fbemI [Image attached] [Tweet]. Twitter. https://twitter.com/paniterka_ch/status/1599893804345331713
2. Ziwei Ji, Nayeon Lee, Rita Frieske, Tiezheng Yu, Dan Su, Yan Xu, Etsuko Ishii, Ye Jin Bang, Andrea Madotto, & Pascale Fung (2023). Survey of Hallucination in Natural Language Generation. ACM Computing Surveys, 55(12), 1–38.
3. Ortega, P., Kunesch, M., Delétang, G., Genewein, T., Grau-Moya, J., Veness, J., Buchli, J., Degrave, J., Piot, B., Perolat, J., Everitt, T., Tallec, C., Parisotto, E., Erez, T., Chen, Y., Reed, S., Hutter, M., Freitas, N., & Legg, S.. (2021). Shaking the foundations: delusions in sequence models for interaction and control.



