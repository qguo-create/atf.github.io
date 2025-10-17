

## 项目背景

Automated Theorem Proving （自动定理证明）的训练需要大量高质量的formal statement作为proof合成的起始，但目前通用的大模型在Autoformalization上的效果不佳。尽管有相关工作通过训练端到端的 formalizer模型解决这个问题，但是仍然面临两个问题：

1. 语法：形式化语言 （Lean4）的知识不足。基座模型的预训练中缺乏形式化数据，只依靠后训练无法熟练掌握复杂的语法。
2. 语义：缺少可靠的一致性评价。生成的formal statement需要保证和原命题等价，目前最优的方法是llm 进行判断，但llm-as-judge的方法的可靠性缺乏验证。

这篇工作，将语法有效性和语义一致性的评估作为工具调用引入到autoformalization流程中，显著提升了formal statement的生成质量。

## 工具调用设计

### Syntax_check 语法检测

以Lean 4编译器的反馈作为语法有效性的检测，能够直接判断formal statement的语法正确性，也是常用的验证方法。但关键问题在于Lean 4编译效率低、难以处理大规模的数据。

采用了一种 预检查 + 分组批量执行策略：
...

## Framework

### 推理范式

模型基于数学问题进行简明思考后给出初步的formal statement结果，随后按照 语法->语义的调用方法进行检测，根据反馈结果进行修改，直到全部通过给出最终结果。
...

## 实验

在StepFun使用的三个ATP数据集 FormalMath-lite （ID）、Proverbench （ID）、combibench（OOD）上进行实验
...
