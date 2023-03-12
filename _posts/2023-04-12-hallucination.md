## Why Hallucination is a Poor Term for this Machine Learning Phenomenon
![hallucinated-cpu.jpeg](/images/hallucinated-cpu.jpeg)

The most significant achievement OpenAI made with ChatGPT is not technical, but the rapid pace at which it took large language models (LLMs) from being technology that few outside of the machine learning space or close to it to being the topic of dinner conversation. ChatGPT is now firmly implanted in the zeitgeist.

### Hallucination
If you have used ChatGPT, or similar generative LLMs, you will have likely noticed it generate text that is simply not factual. This is one of the largest problems with generative text today.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Then I decided to ask ChatGPT about something that I knew didn’t exist: a cycloidal inverted electromagnon. I wrote my thesis about electromagnons, but to be double sure, I checked there was no such thing (it&#39;s been ca. 7 years since my defense). ChatGPT thought differently: <a href="https://t.co/g1po0fbemI">pic.twitter.com/g1po0fbemI</a></p>&mdash; Teresa Kubacka (@paniterka_ch) <a href="https://twitter.com/paniterka_ch/status/1599893804345331713?ref_src=twsrc%5Etfw">December 5, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

In cases like these the model has generated text containing something that is not factual, and what's more insideous is that what the model has produced is often very convincing. I would have no idea whether "cycloidal inverted electromagnon" is a real scientific term or not [[1]](https://twitter.com/paniterka_ch/status/1599893804345331713?s=20). The term for this unfortunate side effect is called _hallucination_.

### Hallucination is a Poor Term for this Phenomenon in Generative Contexts
Using the term _hallucination_ originally began in the computer vision space, and I think the term makes much more sense when used in that context, at least when we're talking about CV tasks like image classification and captioning [[2]](https://arxiv.org/abs/2202.03629). Tasks like these are perception-like, whereas generative tasks are, well, generative, and I argue that using the term _hallucination_ in a generative context is not a good word for what is actually happening.

### What Would be a Better Term?
So if _hallucination_ is a poor term in generative contexts then what alternatives do we have? In my research into hallucination I've come across several alternatives, some of which make sense in certain contexts where others do not. I learned about most of these terms from the fantastic recent [_Survey of Hallucination in Natural Language Generation_ by Ji et al (2022)](https://arxiv.org/abs/2202.03629). The other term of which I am fond of is _delusion_, used by Deepmind ([Ortega et al 2021](https://arxiv.org/abs/2110.10819)).

**Alternative Terms:**
- delusion
- faithfulness
- factuality
- correctness
- accuracy
- informativeness

#### Delusion
I like this term because it means something that is believed to be true, but is in fact not true. I also like that the term is in the same sort of semantic space as hallucination, inasmuch as the terms are both psychological. Where I think this term becomes less ideal for me is actually one of the same reasons I disprefer the term _hallucination_: it anthropomorphizes the model.

#### Factuality and Faithfulness
_Factuality_ refers to whether the generated output is objectively true, whereas _faithfulness_ refers to how consistent the generated text is with the source context the model was given (through prompting, training/fine-tuning, or both).

In a scenario where Five Guys hosts a generative conversational agent to respond to customer queries online, as the owner of the agent you would want a prompt like "Which is better, Five Guys or In-N-Out?" to be answered by the bot making a case as to why In-N-Out is the better choice for your lunch or dinner, not for the model to reference some real or made up study supporting the theory that Five Guys makes a better burger. In this scenario, you want _faithfulness_, you want your model to faithfully reference the source context you provided it. This source context would likely include things like marketing copy from In-N-Out that say great things about their burgers.

You can likely imagine scenarios where the opposite is true and you would optimize for _factuality_ over faithfulness. One category of these scenarios is using a generative LLM for information retrieval. If your task is retrieving information, you want that information to be factual. Your output may not be _factual_ due to several reasons, one of them being that your data the model was trained on is no longer factual. Prompting your model with a question like "Who is the current president?" may produce an output that says Obama is president--this response may very well be _faithful_ to your (now partly stale) dataset, but the response is clearly not _factual_ when given in 2023. 

#### Correctness, Accuracy, Infomativeness
I have yet to study these terms enough to provide something useful here. Perhaps if I do research them I will revise this section.

### Conclusion
Instead of _hallucination_, terms like _factuality_ and _faithfulness_ are more accurate terms for this generative side effect. Additionally, there are scenarios in which one of these two new terms are more appropriate than the other. If you want to read more on the these terms and their usage in current hallucination research, or if you want to learn more about generative hallucination in general I highly recommend the [_Survey of Hallucination in Natural Language Generation_ by Ji et al (2022)](https://arxiv.org/abs/2202.03629).

### References
1. Kubacka, Teresa. Tweet, 2022-12-05: https://twitter.com/paniterka_ch/status/1599893804345331713?s=20.
2. Ji et al. Article, 2022: https://arxiv.org/abs/2202.03629