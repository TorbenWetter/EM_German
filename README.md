![EM Logo](em_model_logo_web.jpeg)

# EM German Model Family

([Zur deutschen Version](README_DE.md))

**EM German (v01)** is an experimental llama2-based model family, finetuned on a large dataset of various instructions in German language. The models are optimized for German text, providing proficiency in understanding, generating, and interacting with German language content.

**This 7b model has addtionally been pre-trained on >3bn high-quality tokens of German text**.

# Links & Demos

We will publish further instructions, updates and code-snippets in the project's [Github-Repo](https://github.com/jphme/EM_German).

## Model Links

|       | HF    | GPTQ  | GGUF  | AWQ   |
|-------|-------|-------|-------|-------|
| 7b    | [Link](https://huggingface.co/jphme/em_german_7b_v01) | [Link](https://huggingface.co/jphme/em_german_7b_v01_gptq) | [Link](https://huggingface.co/jphme/em_german_7b_v01_gguf) | soon |
| 13b   | [Link](https://huggingface.co/jphme/em_german_13b_v01) | [Link](https://huggingface.co/jphme/em_german_13b_v01_gptq) | [Link](https://huggingface.co/jphme/em_german_13b_v01_gguf) | soon |
| 70b   | [Link](https://huggingface.co/jphme/em_german_70b_v01) | [Link](https://huggingface.co/jphme/em_german_70b_v01_gptq) | [Link](https://huggingface.co/jphme/em_german_70b_v01_gguf) | soon |
| Mistral 7b | soon | soon | soon | tbc |

## Demos:

You can use some of the models with **free** google Colab instances (e.g. the 7bn model in 8bit or the 13b model with GPTQ):

* [Example Colab Notebook for 13b with GPTQ](https://colab.research.google.com/drive/1IJfJdVwGkfe5MYOqHptystR3FBeEUdGn?usp=sharing)
* [Example Colab Notebook for 7b with 8bit-Loading](https://colab.research.google.com/drive/1bsv6vkLM4AlCpSyXA6ol9P32zxZmf7Zu?usp=sharing)
* Further Examples for LLM apps will follow soon...


# Prompt Format

This model follows the Vicuna format without linebreaks (but should work with linebreaks as well). The format is as follows:

```
Du bist ein hilfreicher Assistent. USER: <instruction> ASSISTANT:
```

You can swap the standard system prompt for a better suited one (see below for RAG-tasks).

# Results

Attached a few example outputs. I also developed a few small German benchmarks (based on the Eleuther LM Evaluation Harness), which I will publish soon.

## Example Output

Prompt:
```
Du bist ein hilfreicher Assistent USER: Ein Buch hat 500 Seiten. Jede Seite enthält 300 Wörter. Wie viele Wörter sind im gesamten Buch enthalten? ASSISTANT:
```

Response EM 7b v01
```
Die Gesamtzahl der Wörter in dem Buch kann berechnet werden, indem man die Anzahl der Wörter pro Seite mit der Gesamtzahl der Seiten multipliziert.

Gesamtzahl der Wörter = Anzahl der Wörter pro Seite * Gesamtzahl der Seiten = 300 Wörter pro Seite * 500 Seiten = 150.000 Wörter

Das Buch enthält also insgesamt 150.000 Wörter.
```

Prompt:
```
Du bist ein hilfreicher Assistent USER: Erläutere die Grundprinzipien der evolutionären Biologie und Genetik, indem du den Prozess der natürlichen Selektion, die Rolle von Mutationen und genetischer Drift sowie das Konzept der adaptiven Radiation erklärst. ASSISTANT:
```

Response EM 7b v01
```
Die Evolutionäre Biologie und Genetik sind zwei intim verwandte Disziplinen, die sich mit dem Studium des Verhaltens und der Entwicklung von Organismen in der Natur befassen. Sie untersuchen, wie Arten sich im Laufe der Zeit entwickeln und wie diese Veränderungen genetisch bedingt sind.

    1. Natürliche Selektion: Die natürliche Selektion ist ein grundlegendes Prinzip in der Evolutionäre Biologie. Es besagt, dass Individuen innerhalb einer Spezies unterschiedliche Fähigkeiten oder Merkmale aufweisen können. Diese Merkmale beeinflussen ihre Überlebens- und Fortpflanzungsrate. Diejenigen mit Vorteilen haben eine höhere Wahrscheinlichkeit, ihre Gene an zukünftige Generationen weiterzugeben und so die Art im Laufe der Zeit zu verändern.

    2. Rolle von Mutationen: Mutationen sind Veränderungen im Genom eines Organismus, die entweder durch zufällige Fehler während der Replikation oder durch Exposition gegenüber Strahlung verursacht werden. Diese Veränderungen können dazu führen, dass ein Individuum neue Eigenschaften aufweist, die es im Kampf ums Überleben vorteilhaft machen könnten. Diese Mutationen werden dann von der natürlichen Selektion beeinflusst und können so zur Entwicklung neuer Arten beitragen.

    3. Genetische Drift: Genetische Drift ist ein zufälliger Prozess, der durch die Verteilung von Allelen in einer Population stattfindet. Wenn eine Population kleiner wird oder wenn die Überlebens- und Fortpflanzungsraten zwischen den Individuen variieren, kann dies dazu führen, dass bestimmte Gene stärker oder weniger häufig werden. Dies kann dazu führen, dass die Population im Laufe der Zeit unterschiedliche Merkmale aufweist.

    4. Adaptive Radiation: Adaptive Radiation ist ein Prozess, bei dem eine Art mehrere verschiedene Linien auslässt, die sich auf verschiedene Weise an ihre Umgebung anpassen. Dies geschieht normalerweise, wenn die Umwelt sich ändert und die Art neue Fähigkeiten benötigt, um überleben zu können. Die verschiedenen Linien können dann unterschiedliche Eigenschaften entwickeln, die ihnen helfen, in dieser neuen Umgebung zu überleben.


```

## Factual Retrieval / RAG

EM Models offer a special format for Factual Retrieval/RAG that is optimized for minimizing hallucinations. We use the same format as Airoboros for this:

### Example

Prompt
```
Du bist ein hilfreicher Assistent. Für die folgende Aufgabe stehen dir zwischen den tags BEGININPUT und ENDINPUT mehrere Quellen zur Verfügung. Metadaten zu den einzelnen Quellen wie Autor, URL o.ä. sind zwischen BEGINCONTEXT und ENDCONTEXT zu finden, danach folgt der Text der Quelle. Die eigentliche Aufgabe oder Frage ist zwischen BEGININSTRUCTION und ENDINCSTRUCTION zu finden. Beantworte diese wortwörtlich mit einem Zitat aus den Quellen. Sollten diese keine Antwort enthalten, antworte, dass auf Basis der gegebenen Informationen keine Antwort möglich ist! USER: BEGININPUT
BEGINCONTEXT
Url: https://www.jph.me
ENDCONTEXT 
Das Wetter in Düsseldorf wird heute schön und sonnig!
ENDINPUT
BEGININSTRUCTION Was ist 1+1? ENDINSTRUCTION ASSISTANT:
```

Model response:

```
Mit den gegebenen Informationen ist diese Frage nicht zu beantworten.
```
Note that the model would normally always answer with the correct response to a trivial question like this but is trained to deny an answer, if there is no source between the BEGININPUT and ENDINPUT that provides a grounding.

If we keep the same Context/Input but ask instead:
```
BEGININSTRUCTION Wie wird das Wetter heute in Düsseldorf? Gebe die Quelle mit an! ENDINSTRUCTION ASSISTANT:
```

We get the correct answer with the source:

```
Das Wetter in Düsseldorf wird heute schön und sonnig! (Quelle: Url: https://www.jph.me)
```


# Evaluation
I will publish some custom German benchmarks and the results for them soon.

# Dataset

The dataset is a mixture of multi-turn chats, retrieval instructions and synthetically generated instructions spawning many topics and applications.


## Use with tranformers

Unchanged from the base model:

```python
import torch
from transformers import LlamaForCausalLM, LlamaTokenizer

# Hugging Face model_path
model_path = 'jphme/em_german_7b_v01'
tokenizer = LlamaTokenizer.from_pretrained(model_path)
model = LlamaForCausalLM.from_pretrained(
    model_path, torch_dtype=torch.float16, device_map='auto',
)

def ask_model(instruction, system='Du bist ein hilfreicher Assistent.'):
    prompt=f"{system} USER: {instruction} ASSISTANT:"
    input_tokens=tokenizer(prompt, return_tensors="pt").to(model.device)
    output_tokens=model.generate(**input_tokens,  max_new_tokens=200)[0]
    answer=tokenizer.decode(output_tokens, skip_special_tokens=True)
    return answer

print(ask_model("Nenne mir 10 gute Gründe dafür, heute Sport zu machen!"))
```

# Limitations & Biases

This model can produce factually incorrect output, and should not be relied on to produce factually accurate information.
This model was trained on various public datasets. While great efforts have been taken to clean the pretraining data, it is possible that this model could generate lewd, biased or otherwise offensive outputs.

# Acknowledgements:

Many thanks to [winglian/caseus](https://huggingface.co/winglian) for his great work on Axolotl which I used to train the EM mdoels. I am also grateful to [Jon Durbin](https://huggingface.co/jondurbin) and his [Airoboros](https://huggingface.co/jondurbin/airoboros-l2-70b-2.2.1) models and code from which I borrowed many ideas and code snippets.

The 70b model was trained with support of the [OVH Cloud Startup Program](https://startup.ovhcloud.com/en/).

# Contact

I you are interested in customized LLMs for business applications, please get in contact with me via [my website](https://www.jph.me). I am also always happy about suggestions and feedback.

*PS: I am also still searching for a Co-Founder*.

# Disclaimer:

The license on this model does not constitute legal advice. I am not responsible for the actions of third parties who use this model.
This model should only be used for research purposes. The original Llama2 license applies and is distributed with the model files.