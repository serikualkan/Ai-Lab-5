# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

I think Layer 1 change the results most. Before it, the agent had 16 correct answers, 4 wrong answers and 4 no answers from 24 questions. After Layer 1 it had 18 correct answers, 6 wrong and 0 no answers.

It helped the agent because when tool make an error, the model can see this error and try again. So it give the agent more possibility to do the task correctly.

Layer 2 did not change accuracy, it only limited the number of steps. Layer 3 reduced wrong answers to 4, but also made 2 no answers. I think it is useful because it not allow the agent to give answers which are not supported by tool results.

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

One example is q18. Even with all three layers, the agent still was not able to answer this question correctly.

In the trace, the model first get CPI values for Jambyl region. Then it used calculate tool, but made mistake with calculation. The tool returned 0.055, but model answered 0.55 percentage points.

The harness noticed that 0.55 was not in tool results and asked the model to correct it. But the model repeated same calculation and give the same wrong answer again.

I would add one more calculation check to the harness. It can check if final number really match with calculation result. The disadvantage is that it will need more tokens, more time and maybe extra model calls.

## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

I would choose fixed workflow for Dala Insight monthly ranking. It got 13 correct answers out of 15, but bare agent got only 9 correct answers.

The workflow used only 15 model calls and 3,852 tokens, and it take 16.3 seconds. The agent used 26 calls, 19,835 tokens and take 49.7 seconds.

So I think workflow is better because it give more correct answers and also faster and cheaper. Monthly reports have almost same structure every time, so it is not necessary to use complicated agent for this work.

But for more difficult questions, where we need different steps and additional analysis, I would choose the agent.

---

I wrote this file myself, without any AI tool.
