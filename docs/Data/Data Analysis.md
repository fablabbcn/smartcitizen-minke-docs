---
toc_depth: 1
---

# Data Tools

![Data analysis with pen and paper tools in Plaça del Sol - Barcelona](https://live.staticflickr.com/4490/24368448418_d602723a10_h.jpg)

When dealing with sensor data, specially with low cost sensors, a great part of the **effort needs to be dedicated to data analysis**. After a careful data collection, this stage of our experiments is fundamental to extract meaningful conclusions. For this reason, this section is a compilation of tools for making sense of the data. Some of them are custom made, and others are general purpose tools that can be adapted for the Smart Citizen use case. Check them below, and head out [to the guides](https://docs.smartcitizen.me/guides/) for more step-by-step documentation on each!

## Pen and paper

Probably the best way to get started in data analysis by using simple tools for comparing data and extracting insights. Time-series plots can be printed in large sheets of paper, and can then be compared with each other by drawing onto transparency paper.

!!! info "Basic, but insightful!"
    This tool, even if seemingly very basic, allows you to work with data and share insights with others very quickly. For instance, while working with the _Plaça del Sol Community_ in Barcelona, we learnt that the noise patterns in social areas are, on average, not as loud as other traffic areas, but that the _peaks_ of the noise are what cause the biggest concerns. From that we learnt that the regulation of noise in public spaces is not really representative for these areas, and that even if on average the readings are below the limits, sometimes the place is unlivable!

<img src="https://live.staticflickr.com/65535/51719385133_9c826ec98d_k.jpg" width="2048" height="1152" alt="AIRE Workshop for the Venice Biennale Architettura 2021"/>

!!! tip "How to make them?"
    Soon you will be able to generate the files for printing from the [web dashboard](https://dashboard.smartcitizen.me). In the meantime, you can check [this tutorial](https://github.com/fablabbcn/smartcitizen-data/blob/master/examples/notebooks/13_pdf_largescale_plots.ipynb) in python

!!! tip "Source files"
    Paper charts on the Smart Citizen Toolkit: https://github.com/fablabbcn/smartcitizen-toolkit/tree/master/pen-and-paper
    Pen and Paper with python scripts: https://github.com/fablabbcn/smartcitizen-data/blob/master/examples/notebooks/13_pdf_largescale_plots.ipynb

## Web tools

Web tools do not require any installation, and for that they are very easy to use (almost) everywhere. Normally data is directly requested via the [API](https://docs.smartcitizen.me/data/data-platform/#api), but in some cases you can also load a CSV file. However, this ease of use comes at a cost: many of the tools are not very flexible, and different visualisations are not possible, or integrations with our API is not always complete. Nevertheless, they normally require zero setup, so you can get started in no time!

![](/assets/images/dashboard.png)

Some examples you can check out:

- [Smart Citizen Map]({{ extra.urls.platform.link }}): the classic map, with simple time-series plots and comparisons between metrics from one device
- [Smart Citizen Dashboard](https://dashboard.smartcitizen.me): a basic dashboard, written in javascript, that can show all the devices, their status, and allows for filtering based on location and tags. It also features a basic time-series plot with customisable time-frame, websockets notifications, and data download in CSV, from any device!
- [RawGraphs](https://rawgraphs.org): an open source web based visualisation tool, based on [D3](https://d3.js), that can interact with data from a CSV file (and maybe from our API sometime soon)
- [Binder](https://mybinder.org): a web based notebook tool for more advanced data analysis. See below in the [advanced section](#advanced)

!!! tip "More?"
    More tools can be found in the [toolkit repository](https://github.com/fablabbcn/smartcitizen-toolkit/). You can check some of them as well on the [Creating interfaces Guide](https://docs.smartcitizen.me/guides/data/creating-interfaces/).

!!! tip "Source files"

    - Smart Citizen API: {{ extra.urls.api.link }}
    - Smart Citizen Web: https://github.com/fablabbcn/smartcitizen-web
    - Smart Citizen Dashboard: https://github.com/fablabbcn/smartcitizen-dashboard-js
    - Onboarding App: https://github.com/fablabbcn/smartcitizen-onboarding

## Live demos

Live demos can help show how sensors work or how they react to different events: for instance, how PM data changes when you put a candle near the kit, even if you can't see the smoke, or how temperature rises when you touch the temperature sensor.

For you to be able to do these experiments, you need _high speed data_ (i.e. data that is updated way faster than once a minute on a web dashboard). To help with that, we have prepared a [specific guide for Live Demos](https://docs.smartcitizen.me/guides/data/live-demos/), so make sure to check it out!

![](/assets/images/serialstudio.png)

!!! tip "Source files"
    Live demos: https://github.com/fablabbcn/smartcitizen-toolkit/

## Creative coding

Sometimes visualising data is more impactful when using creative visualisations that do not have numbers or graphs on them. seCreative coding refers to those tools that generate some short of data visualisation, but that is not done in the _conventional_ way, but more on an _artistic_ way.

![](/assets/images/processing-flock.gif)

A good example to get started is [processing](https://processing.org) or it's web version [p5](https://p5.js). Both are simple to use if you want to learn how to code in a fun way, they are full of examples, and very well documented. Also, you can make music based on your kit's data with [supercollider](https://supercollider.github.io/).

!!! info "Examples"
    You can find some examples in the [guides](https://docs.smartcitizen.me/guides/data/creative-coding)!

## Visual programming

Needing to get more advanced insights, but not wanting to program them? Visual programming tools can help you get started. They are midway between web tools (with no installation, but not very flexible) and more advanced tools (installation and flexibility is full on). Here you will need to install something, as they normally require libraries and other background processes to run in your computer. However, that initial process comes with loads of good things, for instance, the ability to use generic data analysis tools with our data.

![](/assets/images/orange-basic.png)

Some examples are below:

- [Node-RED](http://nodered.org/) is an open-source visual tool that enables the connection between hardware devices, APIs and online services. The tool can be [easily installed](http://nodered.org/docs/getting-started/installation) on any local computer or even an inexpensive Raspberry Pi single board computer.
- [Orange](https://orangedatamining.com/) - an open source tool for data analysis. As part of a collaboration with [Cos4Cloud MECODA](https://github.com/eosc-cos4cloud/mecoda-orange), you can also access Smart Citizen data from this great tool with a few clicks.

!!! info "Orange workflows"
    If you want to use some existing workflows, you can visit the **Orange Workflows Repository** {{config.repo_url}}/tree/master/docs/assets/ows

    Also, a lot of [step-by-step tutorials](https://docs.smartcitizen.me/guides/data/visual-programming) will help you use it in any use case (also in educational contexts!)

## Advanced

Here we go, this is the most advanced and flexible tool of them all: a data analysis package written specifically to interact with several APIs, including of course the Smart Citizen API, and to perform all the operations needed for doing advanced data analysis. Leveraging on the power of [`python`](http://www.python.org) and all it's associated tools, `scdata` is a package that can be easily installed on any computer with a simple `pip install scdata`. It is intended to provide an **state-of-the art data analysis environment**, adapted for the uses within the Smart Citizen Project, but that can be easily expanded for other use cases. The ultimate purpose of the framework is to allow for reproducible research by providing a set of tools that can be replicable, and expandable among researchers and users alike, contributing to [FAIR data principles](https://www.nature.com/articles/sdata201618). Ultimately, it uses normal [pandas](https:pandas.pydata.org/) dataframes that can be passed to any plotting, modelling or numerical analysis library in python.

[![DOI](https://zenodo.org/badge/97752018.svg){: align=left !important}](https://zenodo.org/badge/latestdoi/97752018)
<br>
[![Binder](https://mybinder.org/badge_logo.svg){: align=left !important}](https://mybinder.org/v2/gh/fablabbcn/smartcitizen-data/master?filepath=%2Fexamples%2Fnotebooks)
<br>
[![PyPI version](https://badge.fury.io/py/scdata.svg){: align=left !important}](https://badge.fury.io/py/scdata)
<br>

!!! info "More familiar with R?"
    [R](https://www.r-project.org/) users won't be left stranded. [RPY2](https://pypi.org/project/rpy2/) provides functionality to send data from _python_ to _R_ quite easily. Also, you can download [this R library](https://github.com/fablabbcn/smartcitizen-R-data) to access data from R!

!!! info "We care for open (science)"

    Our concept of _open science_ might differ from others in fundamental way. It does not go on the _hype_ that many people advocate for to simply make business with it. We think that free and open source development practices are fundamentally applicable to any aspect of knowledge and research, and also to _open science_ by default, at least the way we understand it. For us, this means that data that can be **accessible** through **open apis** without any restriction, **reproducible** by providing **all the information and tools** on how the data is processed from _raw_ to _final_ format, **findable** with unique, unmutable, identifiers in open dataset repositories such as [zenodo](https://zenodo.org). You will be wondering about interoperable: this last one probably will take more time, but hopefully we will get there one day if we all agree on what this all means.

The framework integrates with the [Smart Citizen API](https://docs.smartcitizen.me/data/data-platform/#api) and helps with the analysis of **large amounts of data in an efficient way**. It also integrates functionality to **generate reports** in _html_ or _pdf_ format, and to **publish datasets** and documents to [Zenodo](https://zenodo.org).

!!! info "Raw and processed data"
    All the raw sensor data from the devices is sent to the Platform and processed outside of the sensors. **Raw data is never deleted**, and the postprocessing of it can be traced back to it's origin by using the sensor blueprint information. This way, we guarantee openness and accesibility of the data for research purposes.

    Check [this guide](https://docs.smartcitizen.me/guides/data/custom-data-processing/) to learn more about how we postprocess the data of the sensors and how to make it your own way.

This is the tool that probably has the largest amount of examples and use cases:

- [Guides](https://docs.smartcitizen.me/guides/data/advanced-data-tools/) will help you to install the framework and start using it!
- [Scripts and Notebook Examples](https://github.com/fablabbcn/smartcitizen-data/tree/master/examples) is a compilation of examples ready to get hands on with the data

## Source files

- Smart Citizen Data (python): https://github.com/fablabbcn/smartcitizen-data
- Smart Citizen Data (R): https://github.com/fablabbcn/smartcitizen-data
- Smart Citizen Connector (python): https://github.com/fablabbcn/smartcitizen-connector
- Smart Citizen Flows: https://github.com/fablabbcn/smartcitizen-flows