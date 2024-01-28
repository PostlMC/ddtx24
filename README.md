# Data Day Texas 2024

This repo contains:

- A Poetry environment for running notebooks from the two workshops I attended at
  [Data Day Texas][ddtx] 2024 along with a few minor tweaks to get things working
- The few photos I took from a couple of talks. Ideally, {[worthyl][worthyl],
  [gstrat43][gstrat43]} will PR their notes/photos in as well.
- The original summary for each session from the [ddtx site][ddtx].

Where repos are linked, just clone 'em in this directory for links into each to work.

I used to [post][ddtx17] [ddtx][ddtx19] [notes][ddtx20] [as][ddtx22] [gists][ddtx23],
but since there are notebooks from the workshops this time around, I figured why not
share what I did to get them running. (It's not a lot, but still...)

## Plenary Keynote: Practitioner turned Executive

**What caught me by surprise & lessons I learned about how decisions are really made**
**with data ecosystems.**

Speaker: [Sol Rashidi][rashidi]

Sol will present an unfiltered and transparent conversation about the unexpected
challenges and revelations she experienced pivoting from a hands-on data
practitioner to a strategic data executive. She'll discuss the successes, failures,
and the exchange of popularity one has to sometimes make, in order to make progress
when deploying large-scale data ecosystems. There are under-appreciated intricacies
involved in transitioning from a technical role to an executive position, and there
is EQ, SQ, and BQ that must to be developed to compliment the IQ. While it may be
obvious what needs to be done, Sol will share the real-world processes and politics
that drive the decision-making in the data world.

![IMG](./img/IMG_5163.png)
![IMG](./img/IMG_5164.png)
![IMG](./img/IMG_5165.png)

## Introduction to Graph Data Science for Python Developers

Speaker: [Sean Robinson][robinson] - [Graphable][graphable]

This workshop will cover a variety of graph data science techniques using Python, Neo4j,
and other libraries. The goal of the workshop is to serve as a springboard for attendees
to identify which graph-based tools/techniques can provide novel value to existing
workflows. Some of the techniques to be covered are:

- How to think about data as a graph and the implications that has on downstream
  analysis
- How to use graph algorithms at scale using both Neo4j and other Pythonic libraries
- How to enhance traditional ML models with graph embeddings
- How to visualize these insights in the context of a graph for greater business
  intelligence
- How to integrate these techniques with your existing data science tool belt

### Repos and Notebook

- Repo: <https://github.com/seankrobinson/integrated_graph_ml_demo>
- <https://github.com/seankrobinson/DDTX_2024>

Run a local Neo4j Instance with the Graph Data Science module for the notebook to use:

``` shell
docker run -d \
    -p 7474:7474 \
    -p 7687:7687 \
    --env NEO4J_AUTH=neo4j/${NEO4J_PASSWORD} \
    --volume "$(pwd)/neo4j/data":/data \
    --env NEO4J_PLUGINS='["graph-data-science"]' \
    neo4j:latest
```

- Notebook: [Demo_Notebook.ipynb](./integrated_graph_ml_demo/Demo_Notebook.ipynb)

A few minor tweaks were made to get it all running in my environment:

- A few `plt.show()` calls were sprinkled in where the graphs weren't rendering
- The setup cell was tweaked to load the Neo4J password as an environment variable:

``` python
import os
from dotenv import load_dotenv

load_dotenv()

URI = "neo4j://localhost:7687"
creds = ("neo4j", os.getenv("NEO4J_PASSWORD"))
gds = GraphDataScience(URI, auth=creds)
```

## Patterns of Power: Uncovering control points to influence outcomes

Speakers: [Amy Hodler][hodler] - [graphgeeks.org][graphgeeks]

We all know everything is connected, but what can you do with this information? Some
organizations use the relationships between data to improve predictions, but there's a
huge untapped opportunity to apply these patterns to shape more positive outcomes.
Simply put, we are wasting insights hiding in existing data that can help grow revenue,
increase resiliency and safety, and improve lives.

In this session, Amy Hodler will share the common forms of power within various networks
ranging from IT and software systems to social, biological, and financial ecosystems.
She'll show how companies like LinkedIn and Google have revealed the structural patterns
of influence using network analysis and graph analytics. Then she'll delve into the
concept of centrality and how it's used to combat terrorism, cyberattacks, and
infectious diseases. And we'll look at how this science of measuring importance is
evolving to be more readily applied to different needs.

From identifying key actors to strategies for using control points, you'll learn about
different approaches and tools for moving beyond predictive analytics to enacting
change. Finally, Amy will examine ethical considerations and explore the responsible use
of technology to influence power dynamics. You'll walk away with practical knowledge
about uncovering power and influence patterns, along with methods to actively shape
positive outcomes.

![IMG](./img/IMG_5166.png)
![IMG](./img/IMG_5167.png)

## Causality: The Next Frontier of GenAI Explainability

Speakers: [Amy Hodler][hodler] and [Michelle Yi][yi]

In a world obsessed with making predictions and generative AI, we often overlook
the crucial task of making sense of these predictions and understanding results.
If we have no understanding of how and why recommendations are made, if we can’t
explain predictions – we can’t trust our resulting decisions and policies.

In the realm of predictions and explainability, graphs have emerged as a powerful
model that has recently yielded remarkable breakthroughs. This talk will examine
the implications of incorporating graphs into the realm of casual inference and
the potential for even greater advancements. Learn about foundational concepts
such as modeling causality using directed acrylic graphs (DAGs), Jedeau Pearl’s
“do” operator, and keeping domain expertise in the loop. You’ll hear how the
explainability landscape is evolving, comparisons of graph-based models to other
methods, and how we can evaluate the different fairness models available.

In this work session, you’ll get an overview of using the open source PyWhy
project with a hands-on example that includes the DoWhy and EconML libraries.
We’ll walk through identifying assumptions and constraints up front as a graph
and applying that through each phase of modeling mechanisms, identifying targets,
estimating causal effects, and robustness testing to check prediction validity.
We’ll also cover our lessons learned and provide tips for getting started.

Join us as we unravel the transformative potential of graphs and their impact on
predictive modeling, explainability, and causality in the era of generative AI.

### Related Links, Repo, and Notebook

Slides: [ODSC 2023- Causal-Graph-PyWhy][causal-slides]

Technically, this is from a prior conference, but it looks like the same content.

- [Causality by Jedeau Pearl][causality]
- An [article series][ferenc] on the same topic
- [do-calculus][do-calculus] at pypi.org
- Repo: <https://github.com/yulleyi/causal-graph-pywhy>
- Notebook: [ODSC_workshop.ipynb](./causal-graph-pywhy/ODSC_workshop.ipynb)

This one ran without modification.

[ddtx]: https://datadaytexas.com/
[ddtx17]: https://gist.github.com/PostlMC/2aa97e4874f19529568a1b70e12a8aab
[ddtx19]: https://gist.github.com/PostlMC/cbcf6dedcefb2686d799912d467c191d
[ddtx20]: https://gist.github.com/PostlMC/5974fa36b1a4ade9783daeb7658490f8
[ddtx22]: https://gist.github.com/PostlMC/fb86b651a23acd71eb914fed37441070
[ddtx23]: https://gist.github.com/PostlMC/a9812e7c46efaa82611e6a71c0b574dc
[worthyl]: https://github.com/worthyl
[gstrat43]: https://github.com/gstrat43
[rashidi]: https://www.linkedin.com/in/sol-rashidi-a672291/
[robinson]: https://www.linkedin.com/in/seankrobinson/
[graphable]: https://www.graphable.ai/
[hodler]: https://www.linkedin.com/in/amyhodler/
[graphgeeks]: https://www.graphgeeks.org/
[yi]: https://www.linkedin.com/in/michelleyulleyi/
[causal-slides]: ./causal-graph-pywhy/ODSC%202023-%20Causal-Graph-PyWhy.pdf
[causality]: http://bayes.cs.ucla.edu/BOOK-2K/
[do-calculus]: https://pypi.org/project/do-calculus/
[ferenc]: https://www.inference.vc/untitled/
